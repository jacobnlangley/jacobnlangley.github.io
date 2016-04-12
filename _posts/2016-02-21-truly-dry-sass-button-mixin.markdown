---
layout: post
title: "Truly Dry Sass Button Mixin"
date: 2016-02-21 07:21:56 -0400
comments: true
categories: SASS
published: true
---

### The Truly Dry Mixin from [AListApart](http://alistapart.com/article/dry-ing-out-your-sass-mixins)


#### The four Sass features that are the building blocks of a truly DRY mixin

*   Placeholder Selectors
*   Map Data Types
*   The @-root directive
*   The unique-id() function


#### Placeholder Selectors

Placeholder selectors are a special type of selector used with the @extend directive. Class-like in look but the placeholder selector is preceded by a "%" instead of the "." used to indicate a class declaration.


    Class  = .foo
    Placeholder = %foo


Placeholders behave like a normal @extend but will not get printed to the compiled stylesheet unless extended. Like normal @extends the placeholder gets placed in the stylesheet where declared.


#### Map Data Types

Maps are a data type like strings, numbers, lists, that behave similarly to javascript objects. Maps are key / value pairs that can be any of Sass's data types ( numbers, strings, colors ). Keys are ALWAYS unique and can be retrieved by name. So with Sass maps we have a tool for unique storage.



    $properties: (
      color: white;
      background: black;
      font-size: 1em;
    );

    .foo {
      color: map-get($properties, color);
    }





#### The @root Directive

The @root directive places contained definitions at the root of the stylesheet removing the declaration from its current nested state.


#### The unique-id() Function

The unique-id() returns a unique identifier guaranteed to be unique to the current run of Sass.


### Creating the mixin

First determine what properties of our button will by dynamic ( user controlled ) and which will be static or just simply written out in plain CSS in out style declarations.


#### Sass
    .once-btn {
      background-color: $bg-color-default-var;
      border-radius: $border-radius-var;
      padding: $base-padding-var;

      &:hover {
        cursor: pointer;
        background-color: darken($bg-color-default-var, 15%);
      }
    }

#### Sass Button Mixin
    @mixin once-btn($bg-color-var) {
      background-color: $bg-color-var;
      border-radius: $border-radius-var;
      padding: $base-padding-var;

      &:hover {
        cursor: pointer;
        background-color: darken($bg-color-var, 15%);
      }
    }

    .button {
      @include once-btn($bg-color-default-var);
    }



The button mixin will work well but will output lots of duplicate properties in our compiled style sheet.


      .once-btn-look {
          @inlcude once-btn;
        }
        .once-btn-listen {
          @include once-btn;
        }


#### CSS
       .once-btn-look {
          background-color: #000000;
          border-radius: 6px;
          padding: .25em;
        }
        .once-btn-look:hover {
          cursor: pointer;
          background-color: #000000;
        }
        .once-btn-listen {
          background-color: #000000;
          border-radius: 6px;
          padding: .25em;
        }
        .once-btn-listen:hover {
          cursor: pointer;
          background-color: #000000;
        }


We can see how over time the mixin, while indispensible in creating an authoritative declaration of the styles associated with every instance of our once-btn, will begin to bloat our compiled CSS. The first step to reduce the code bloat is to separate the dynamic and static parts of our once-btn mixin.


### Drying Out Our Once Button Mixin

#### CSS
          @mixin once-btn($bg-color-var) {
              @include once-btn-static;

              background-color: $bg-color-var;

            &:hover {
              background-color: darken($bg-color-var, 15%);
            }
          }

          @mixin once-btn-static {
            border: 1px solid;
            border-radius: $border-radius-var;
            padding: $base-padding-var;

            &:hover {
              cursor: pointer;
            }
          }



Now that we have the dynamic and static styles separated for our button mixin, we will need to @extend the static styles so as to prevent duplication in our compiled style sheets.

If we used only used a placeholder selector instead of a mixin for our static button styles then these styles would be moved into the compiled style sheet. So what would work best is if we could create a dynamic placeholder on the fly. This appraoch will create the placeholde the first time the selector is needed and then will retain the source order expected.

We need to create a global variable to hold the names of our DYNAMIC selectors.


      $Placeholder-Selectors: ();


Next, in once-btn-static, we check to see if a key exists for our selector. The key we are looking for is "button". Using the map-get function, we will either get back the value of our key, or we will get back null if the key does not exist. If the key does not exist, we will set it to the value of a unique ID using map-merge. We use the !global flag, since we want to write to a global variable.


####  Sass

     $Placeholder-Selectors: ();
      // ...
      @mixin once-btn-static {
        $button-selector: map-get($Placeholder-Selectors, 'button');

        @if $button-selector == null {
          $button-selector: unique-id();
          $Placeholder-Selectors: map-merge($Placeholder-Selectors, ('button': $button-selector)) !global;
        }

        border: 1px solid;
        border-radius: $border-radius-var;
        padding: $base-padding-var;

        &:hover {
          cursor: pointer;
        }
      }


Once we have determined whether an ID for our placeholder already exists, we need to create our placeholder. We do so with the @at-root directive and interpolation #{} to create a placeholder selector at the root of our directory with the name of our unique ID. The contents of that placeholder selector will be a call to our static mixin (recursive mixins, oh my!). We then extend that same placeholder selector, activating it and writing the properties to our CSS.

By using a placeholder selector here instead of extending a full selector like a class, these contents will only be included if the selector gets extended, thus reducing our outputed CSS. By using an extension here instead of writing out the properties, we also avoid duplicating properties. This, in turn, reduces fragility in our outputed CSS: every time this once-btn mixin gets called, these shared properties are actually shared in the output CSS instead of being roughly tied together through the CSS preprocessing step.

### Sass Button Mixin

        $Placeholder-Selectors: ();
        // ...
        @mixin once-btn-static {
          $button-selector: map-get($Placeholder-Selectors, 'button');
          @if $button-selector == null {
            $button-selector: unique-id();
            $Placeholder-Selectors: map-merge($Placeholder-Selectors, ('button': $button-selector)) !global;

            @at-root %#{$button-selector} {
              @include once-btn-static;
            }
          }
          @extend %#{$button-selector};   

          border: 1px solid;
          border-radius: 5px;
          padding: .25em .5em;

          &:hover {
            cursor: pointer;
          }
        }


We've one last thing to do to make sure our mixin is truly DRY as we are still going to get duplicated outputn at this point, (and we also have a selector extending itself, which which is no bueno). To prevent this, we add an argument to butonce-btn-static to dictate whether to go through the extend process or not. We’ll add this to our dynamic mixin as well, and pass it through to our once-btn-static mixin.


###  Sass Button Mixin

      $Placeholder-Selectors: ();
      // ...
      @mixin once-btn-static {
        $button-selector: map-get($Placeholder-Selectors, 'button');

      	@if $extend == true {
        @if $button-selector == null {
          $button-selector: unique-id();
          $Placeholder-Selectors: map-merge($Placeholder-Selectors, ('button': $button-selector)) !global;

          @at-root %#{$button-selector} {
            @include once-btn-static;
          }
        }
        @extend %#{$button-selector};   

        border: 1px solid;
        border-radius: 5px;
        padding: .25em .5em;

          &:hover {
            cursor: pointer;
          }
        }
      }


Finally we have created a way to easily maintain our styling in Sass, provide a single selector in our HTML, and keep the total amount of CSS to a minimum. No matter how many times the once-btn mixin is included, the static styles will never be duplicated.

The first time we use our once-btn mixin is declared, our styles will be created in the CSS where the mixin was called, preserving our intended cascade and reducing fragility. And since this approach allows for multiple calls to the once-btn mixin we can easily maintain multiple variations is our Sass and HTML.

So this declaration of two variations of the once-btn mixin:

      .once-btn-twice {
        @inlcude once-btn;
      }
      .once-btn-twice-dry {
        @include once-btn;
      }

Now compiles and outputs the following CSS:

     .once-btn-twice {
        background-color: #333333;
      }
      .once-btn-twice,
      .once-btn-twice-dry {
        border: 1px solid;
        border-radius: 5px;
        padding: .5em;
      }
      .once-btn-twice:hover,
      .once-btn-twice-dry:hover {
        cursor: pointer;
      }
      .once-btn-twice:hover {
        background-color: #000000;
      }

      .once-btn-twice-dry {
        background-color: #dddddd;
      }
      .once-btn-twice-dry:hover {
        background-color: #eeeeee;
      }

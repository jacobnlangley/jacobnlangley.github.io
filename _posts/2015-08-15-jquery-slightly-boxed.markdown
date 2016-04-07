---
layout: post
title: "jQuery ~ Slightly Boxed"
date: 2015-08-15 14:39:59 -0400
comments: true
categories: jQuery
---

A simple simple jQuery lightbox of sorts. But semantic.

Markup

    <h1>Galleria</h1>
      <ul class="fancy-pants">
        <li><a href="http://placehold.it/500x500"><img src="http://placehold.it/500x500" width="100" alt="Placeholder Image 1"></a></li>
        <li><a href="http://placehold.it/500x500"><img src="http://placehold.it/500x500" width="100" alt="Placeholder Image 2"></a></li>
        <li><a href="http://placehold.it/500x500"><img src="http://placehold.it/500x500" width="100" alt="Placeholder Image 3"></a></li>
        <li><a href="http://placehold.it/500x500"><img src="http://placehold.it/500x500" width="100" alt="Placeholder Image 4"></a></li>
      </ul>

SCSS

    ul {

      li {
        list-style: none;
      }
    }

    .blackout {
        background:rgba(0,0,0,0.8);
        width:100%;
        height:100%;
        position:absolute;
        top:0;
        left:0;
        text-align:center;
        display:none;

        img {
          margin:5% 0 0 0;
        }

        p {
          color:#fff;
        }

      }

JS

    //Problem: When clicking image user taken to dead end
    //Solution: Create large image with overlay - slightbox


    var $overlay = $("<div class='blackout'></div>");
    var $img = $("<img>");
    var $caption = $("<p></p>");
    // Add an image to overlay
    $overlay.append($img);
    // Add caption to overlay
    $overlay.append($caption);
    //Add overlay
    $("body").append($overlay);

      // Capture click event on a link to an image
      $('.fancy-pants a').click(function(event) {
        event.preventDefault();

        var imgLoc = $(this).attr("href");
        // Update overlay with image linked in link
        $img.attr("src", imgLoc);
        // Show the overlay
            $overlay.fadeIn();
        // Get child's alt attr & set caption
        var captText = $(this).children("img").attr("alt");

          $caption.text(captText);

      });


      // When overlay is clicked
      $($overlay).click(function() {
         // Hide the overlay
        $overlay.fadeOut();

      });

Check out the [codepen](http://codepen.io/jacobnlangley/pen/azYjKJ){:target="_blank"}

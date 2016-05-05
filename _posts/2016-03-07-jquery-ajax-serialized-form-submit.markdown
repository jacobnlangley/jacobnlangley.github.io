---
layout: post
title: "jQuery AJAX serialized form submit"
date: 2016-03-07 03:14:56 -0400
comments: true
categories: Angular
published: true
---

Gotta have this one in your back pocket for quick reference.

### jQuery

    // Click handler on the .submit selector
    $( '.submit' ).on( 'click', function( event ){
          // Stop default form submission
          event.preventDefault();
          // Serialize the entire form, which includes the action
          // Assign it to a variable
          var serialized = $( '.form' ).serialize();
          // Get the form action that will submit form to server side script
          // that will handle writing data to database model
          var ajaxUrl = $('.form ').attr( "action" );
          $.ajax({
              url: ajaxUrl,
              method: 'POST',
              data: serialized, // Holds our serialized data from our form
          }).done( function( result ){
              $('.response .done').addClass( '.transition' );
          }).fail( function( result ){
              $('.response . fail').addClass( '.transition' );
      });

## HTML

        <form class="form" method="get" action="scripts/submit.php">
              <label>Company Name</label>
              <input type="text" name="CoName" id="CoName" class="textfield">
              <label>Company Address</label>
              <input type="text" name="CoAddress" id="CoAddress" class="textfield">
              <input class="submit" type="submit" value="Register Company">
        </form>
        <div class="response">
          <div class="done">Thank you for your submission</div>
          <div class="fail">Something went wrong. Please try again later.</div>
        </div>

## SCSS

    .response {

        max-height: 0;
        transition: max-height 0.15s ease-out;
        overflow: hidden;

        .done,
        .fail {

          max-height: 500px;
          transition: max-height 0.25s ease-in;

        }

    }

Gist [here](https://gist.github.com/jacobnlangley/778c264e394949382d8a04630ec27abe){:target="_blank"}.

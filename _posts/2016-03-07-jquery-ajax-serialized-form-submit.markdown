---
layout: post
title: "jQuery AJAX serialized form submit"
date: 2016-03-07 03:14:56 -0400
comments: true
categories: Angular
published: false
---

Gotta have this one in your back pocket for quick reference.

jQuery AJAX Serialized Form submit
    // Click handler on the .submit selector
    $( '.submit' ).on( 'click', function( event ) {
          // Stop default form submission
          event.preventDefault();
          // Serialize the entire form, which includes the action
          // Assign it to a variable
          var serialized = $( '.form' ).serialize();
          // Get the form action that will submit form to server side script
          // that will handle writing data to database model
          var ajaxUrl = $('.form.attr("action"));
          $.ajax( {
              url: ajaxUrl,
              method: 'POST',
              data: serialized, // Holds our serialized data from our form
          } ).done( function( result ){
              $('#response').show();
          } );
      } );

      <form class="form" method="get" action="submit.php">
            <label>Name of Organization</label>
            <input type="text" name="OrgName" id="OrgName" class="textfield">
            <label>Address of Organization</label>
            <input type="text" name="OrgAddress" id="OrgAddress" class="textfield">
            <input class="submit" type="submit" value="Register Organization">
      </form>
      <div id="response">Thank you for your submission</div>
      <div id="error">Something went wrong. Please try again later.</div>

App is [here](http://jacobnlangley.bitbucket.org/ng-crud-app){:target="_blank"}.

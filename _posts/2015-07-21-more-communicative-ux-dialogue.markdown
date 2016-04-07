---
layout: post
title: "Clearer UX Dialogue"
date: 2015-07-21 21:45:41 -0400
comments: true
categories: UX
---

Web forms are historically a passive aggressive breed.

They don't really give much to the conversation.

I really dig this approach. Simple & straightforward. Clearly communicative.

Markup

    <button type="Submit" class="button postfix ">
    	<span class="button-content">Submit</span>
    </button>


CSS

	button:active,
	button.is-submitted,
	button.is-submitted:hover,
	button.is-submitted:active {
	  background: #27ae60;
	  outline: 0;
	}

	.button {
	  height: 6rem;
	  width:20rem;
	  font-size:2rem;
	}

JS


	$('button').on('click', function(event){

	  event.preventDefault();

	  $(this)
	    .blur()
	    .addClass('is-submitted')
	    .find('.button-content')
	      .text('Got it, thanks!');
	});


Check out the [codepen](http://codepen.io/jacobnlangley/pen/clKGt){:target="_blank"}

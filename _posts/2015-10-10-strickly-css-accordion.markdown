---
layout: post
title: "Strickly CSS Accordion"
date: 2015-10-10 14:38:11 -0400
comments: true
categories: CSS
---
I began resourcing approaches to building an FAQ accordion that would be compatible with IE8. I mucked around with several jQuery approaches, a couple of which I’m still refining for other use cases..

Came across a few CSS approaches and married a couple and I think the results are solid.

There is room for UI discourse on this approach however, as the functionality does not allow for the user to reselect the “active” FAQ to hide the “answer”. The selected FAQ will collapse once another selection has been made.

From a UX perspective I think this makes much sense as it provides a clearer visual division or distinction between collapsed FAQs and expanded answers. Reduces the likelihood of reselecting a FAQ just selected.

All markup and CSS, selectors are IE8+ compatible.

Checkout the Samuel L. Ipsum for the accordions [here](http://slipsum.com/){:target="_blank"}.

Check out the [codepen](http://codepen.io/jacobnlangley/pen/RNGwBm){:target="_blank"}

---
layout: post
title: "Treehouse Badges JSON Widget"
date: 2016-02-14 10:16:56 -0400
comments: true
categories: JSON
published: true
---

My favorite online technology training is [Team Treehouse](http://teamtreehouse.com){:target="_blank"}.

I've been a member for a few years now.

Member account data is exposed as JSON

      {  
      "name":"Jacob Langley",
      "profile_name":"jacoblangley",
      "profile_url":"https://teamtreehouse.com/jacoblangley",
      "gravatar_url":"https://secure.gravatar.com/avatar/ada2bb59f7e55c827a852b267f257621?s=400\u0026d=https%3A%2F%2Fstatic.teamtreehouse.com%2Fassets%2Fcontent%2Fdefault_avatar-1194852ae95df3501aed27c0a96da653.png\u0026r=pg",
      "gravatar_hash":"ada2bb59f7e55c827a852b267f257621",
      "badges":[  
        {  
           "id":49,
           "name":"Newbie",
           "url":"https://teamtreehouse.com/jacoblangley",
           "icon_url":"https://achievement-images.teamtreehouse.com/Generic_Newbie.png",
           "earned_date":"2013-07-25T18:59:03.000Z",
           "courses":[  

           ]
        },
        {  
           "id":163,
           "name":"Getting Started With Rails",
           "url":"https://teamtreehouse.com/library/build-a-simple-ruby-on-rails-application/getting-started-with-rails",
           "icon_url":"https://achievement-images.teamtreehouse.com/badges_SimpleFacebook_Stage1.png",
           "earned_date":"2013-07-25T23:12:07.000Z",
           "courses":[  
              {  
                 "title":"Build a Simple Ruby on Rails Application",
                 "url":"https://teamtreehouse.com/library/build-a-simple-ruby-on-rails-application",
                 "badge_count":1
              },
              {  
                 "title":"Getting Started with Rails",
                 "url":"https://teamtreehouse.com/library/build-a-simple-ruby-on-rails-application/getting-started-with-rails",
                 "badge_count":1
              }
           ]
         }
      ]  
    }

Here's a little widget that shows badge names, badge icons and date earned.

Thinking about creating a jekyll version..

Codepen [here](http://codepen.io/jacobnlangley/pen/WrPpjE){:target="_blank"}

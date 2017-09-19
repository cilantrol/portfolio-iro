---
layout: post
title: Bloc Chat
feature-img: "img/sample_feature_img.png"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030974/bloctalk_1x.png"
short-description: BlocJams for iOS is awesome!

---
This is an example of a post which includes a feature image specified in the front matter of the post. The feature image spans the full-width of the page, and is shown with the title on permalink pages.


# A summary
---
To create an application that allows different users to create a room stored on Firebase and engage in primitive communication. The app allows users to change their username at any given time, which is stored locally as a cookie.


# An explanation
---
This application will be my first mostly unguided project. The work done here is mostly researched via online and later reinforced by my mentor, Junior.
I followed no templates and created the styling  `CSS`, purely based on what I feel is correct. This explains the overuse of `position: fixed` and the non-uniform use of units such as - 'vh, rem, px, %'.

The project is done on Angular 1.6.4 and bootstrap 3.3.7. The goal was to use angular as much as possible and use bootstrap as much as possible for styling. This will be the first release version.

(angularJS)	(bootstrap)
![alt text](https://avatars2.githubusercontent.com/u/139426?v=4&s=400 "angular logo")
![alt text](https://i0.wp.com/webmuch.com/wp-content/uploads/2015/02/bootstrap.png?resize=200%2C200 "bootstrap logo")

# Problem
---
The original objective was to create a functioning chatroom application void of all. There were only 3 objectives in mind.
1. Create an User
2. Create a common gathering for users to interact
3. Assemble and store 3 things to Firebase - {username, time stamp, and content of message} 

Problems that occurred during the development stages included - 
* Improper set up of Firebase arrays 
* Improper validation techniques resulting in veribose javaScript 
* Injecting dependencies in the wrong order, adding broken libraries that result in causing other directives to fail
* Misunderstanding of how the css inherited from bootstrap worked
* Misunderstanding of controllers and their function

# Solution
---


# Results
---

Quality of life changes have been added to improve the user experience. They include -
1. Chat room automatically scrolls to the bottom to view most recent message immediately after input into the chat message bar.
2. Chat message bar automatically empties after each message is sent to avoid sending of duplicate messages.
3. Restricting the use of no-name empty string usernames and chat room names.
4. Upon entering valid state of username or chat room, box transitions from red to green.

# Conclusion
---
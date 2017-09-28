---
layout: post
title: Bloc Chat
feature-img: "img/sample_feature_img.png"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030974/bloctalk_1x.png"
short-description: real time chatting application
---

{:#header-one}
### Summary
---
To create an application that allows different users to create a room stored on Firebase and engage in primitive communication via keyboard. The app allows users to change their username at any given time, which is stored locally as a cookie.

{:#header-two}
### Explanation
---
This application will be my first mostly unguided project. The work done here is mostly researched via online and later reinforced by my mentor, Junior.
I followed no templates and created the styling  `CSS`, purely based on what I feel is correct. This explains the overuse of `position: fixed` and the non-uniform use of units such as - 'vh, rem, px, %'.

The project is done on Angular 1.6.4, Firebase 3.9.0, and Bootstrap 3.3.7. The goal was to use angular as much as possible and use bootstrap as much as possible for styling. This will be the first release version.

The frameworks used for this project were Google fonts and Ionic.

{:align="center"}
##### Technologies Used

{:.techs align="center"}
  ![program](https://avatars2.githubusercontent.com/u/139426?v=4&s=400 "angular logo")
  ![program](https://i0.wp.com/webmuch.com/wp-content/uploads/2015/02/bootstrap.png?resize=200%2C200 "bootstrap logo")
  ![program](https://avatars2.githubusercontent.com/u/1335026?v=4&s=200 "firebase logo")
  ![program](https://qph.ec.quoracdn.net/main-thumb-t-1406102-200-trchoddaujrpnfgqxuxoiyffsclbbuvb.jpeg "ionic logo")
  ![program](https://avatars1.githubusercontent.com/u/6466306?v=4&s=200 "google font api logo")

{:#header-three}
### Problem
---
The original objective was to create a functioning chatroom application void of all superflous functions. There were only 3 objectives in mind.
1. Create an User
2. Create a common gathering for users to interact
3. Assemble and store 3 things to Firebase - {username, time stamp, and content of message}

Problems that occurred during the development stages included -
* Improper set up of Firebase arrays
* Improper validation techniques resulting in veribose javaScript
* Injecting dependencies in the wrong order, adding broken libraries that result in causing other directives to fail
* Misunderstanding of how the css inherited from bootstrap worked
* Misunderstanding of controllers and their function

{:#header-four}
### Development
My previous experience with building an application included using a preset templates with some preset css. The **end in mind** was to create a template that was easy on the eyes which include soft tones of colors and nothing too vibrant or conflicting. In this case, a shade of teal was chose as the background color.
![development](https://i.imgur.com/hVyh14m.png)
As seen in the image above, the current view lacks meaningful structure besides a navigation bar on the left that can be populated with room objects, in the HTML a simple table containing was used to display an array of room objects.
```
<table>
  <tr>
    <td>
  </tr>
</table>
```
but the **first problem** is encountered here...

 And in our code `Room.js` the left example cause inproper passing from key to value which resulted in sending empty value strings to Firebase. A later commit fixes this problem seen on the right example. The takeway here is that the object argument passed in should be the `value` rather than the `$id` or `key`.

{:#roomJS}
{% highlight javascript %}
Room.add = function(room) {    
  rooms.$add({room: value});
};
{% endhighlight %}
{:#roomJS}
{% highlight javascript %}
Room.add = function(room) {
  rooms.$add( { roomName: room} );
};
{% endhighlight %}

To add rooms, we need to also create a button that opens a modal template via bootstrap. At this point I was confused about all the preloaded stylings that came with bootstrap, but I quickly realized they are in fact a very powerful resource.

Bootstrap modals work like elements that float ontop of the current page. I first thought this was a nested controller inside the `HomeCtrl.js` but this is just a method that opens a modal which is controlled by `ModalCtrl`.
{% highlight javascript %}
this.open = function() {
  $uibModal.open({
    animation: true,
    templateUrl: '/templates/modal.html',
    controller: 'ModalCtrl as modal',
    backdrop: 'static'
  });
};
{% endhighlight %}
![development](https://i.imgur.com/oXCFLrH.png)

The **second problem** occurred here when the modal allows the user to submit empty strings as room names.
Validation can be a simple effortless task or it can be a nightmare depending on what resource you follow.
Validation in its simplest form would be simply adding a required directive inside the input tag. This would  automatically set the input to an invalid state.

However for some reason, I wanted the user to be able to click on the submit/add button and removed `ng-disable`. This caused the ability to send empty string room names because I was overzealously adamant about just using angular to achieve this. This however was a **mistake and crucial learning experience** on my part. I spent countless hours trying to do things the _angular way_ which could be adding `this.submitted` inside my method in the controller. Or even better yet, inside the method, the text input field only submits when it exists for example...

{:#roomJS}
{% highlight javascript %}
function ModalCtrl() {
  this.addRoom = function(arg) {
    if(arg) {
      Room.add(arg)
    }
  };
}
{% endhighlight %}

{:#roomJS}
{% highlight javascript %}
function ModalCtrl() {
  this.addRoom = function(arg) {
    this.roomName = arg;
    this.roomName.submitted = true;
    Room.add(this.roomName)
  };
}
{% endhighlight %}

The moral of the story here is just use a few lines of javaScript to save yourself a lot of trouble when the function in the end is the same. The second method will also need `ng-class` and `ng-show` to show error only when the submitted status is achieved along with `ng-minimum`. While this leaves less logic for the controller to handle, the view does become quite polluted. Which method is better? - depends on the project really. For my own personal development, I will use the second method because there's more work involved with angular not because it is necessarily better, it is the method that will give me more practice to the framework as a whole.

One thing I find whimsical when working through this is that for every one problem you solve - another one arises as quickly as you solved the previous. The **third problem** was setting a locally stored username.

{% highlight javascript %}
this is the current default message object
Messages =  {
  message#1 = {
    userName: foo
    content:  bar
    timeStamp: 123
    roomName:  324454526
    }
  message#2 = {
    userName: foo
    content:  bar
    timeStamp: 123
    roomName:  324454526
    }
  }
}
{% endhighlight %}

It was time to populate the Message object with dynamic elements rather than static. The first step was figuring out how to prompt the user to make an username. This is simple, if it doesnt exist then prompt the user!

{:#cookies}
{% highlight javascript %}
var currentUser = $cookies.get('blocChatCurrentUser');
if (!currentUser || currentUser === '') {
  // Do something to allow users to set their username
  $uibModal.open({
    animation: true,
    templateUrl: '/templates/user.html',
    controller: 'ModalCtrl as modal',
    backdrop: 'static'
  });
}
{% endhighlight %}
{:#cookies}
{% highlight javascript %}
this.setUser = function(val)  {
  $cookies.put('blocChatCurrentUser', val);
  $uibModalInstance.dismiss();
};
{% endhighlight %}

A simple if statement block gets the job done here.

The `.put` method always the user to set a value to the cookie and the `.get method` allows the user to retrieve the cookie value. At this point of development, I had misunderstood the concept or the ultitilzation of controllers. While there is no rule of how many controllers to use, it is easy to follow 1 controller per page and additional controllers such as a when we bootstrapped modal. There is no need for a message controller or a cookie controller because they all display in one page.

**What is happening below?** __fourth problem__ User1 is sending empty string messages even though the chat bar was filled. Why is this happening?
![development](https://i.imgur.com/DdBpeXu.png)

To understand the why this occurs, we have to understand how the Firebase `$add` method works. In the view there will be a text input that will be assigned to a `ng-model`. This `ng-model="content"` which will store the user input. This user input is then passed into the form submit. In the controller, we will have a method, our case `addMessage`, which will call the `Message.js` service to then add this value `content` to Firebase. Thats the correct action of steps to execute that action, but in development I had `content` set to a default `''` or null as a starting state. But since I never passed in `content` into the form submit, `content` was doomed to stay null or blank.


{:#message}
{% highlight javascript %}
<form name="addContent"
ng-show="home.activeRoom">
  <input type="text" id="chatMessage"
  ng-model="content"
  placeholder="type here...">
  <span class="input-group-btn">
    <button class="btn btn-success"
    type="submit"
    ng-click=
    "home.addMessage(content)">
    Send
    </button>
  </span>
</form>
{% endhighlight %}
{:#message}
{% highlight javascript %}
Message.send = function(message){
  messages.$add( message );
};
{% endhighlight %}
{:#message}
{% highlight javascript %}
this.addMessage = function(content) {
  this.chatInput.user =
  this.chatInput.sentAt = TIMESTAMP;
  this.chatInput.roomId = this.activeRoom.$id;
  this.chatInput.content = content;
  Message.send(this.chatInput);
{% endhighlight %}

The first example showcases improper submit. vs setting `chatInput.content = content` where `content` is passed in as the argument.

{:#message}
{% highlight javascript %}
<form name="addContent"
  ng-show="home.activeRoom">
    <label for="chatMessage"></label>
    <input type="text" id="chatMessage"
    ng-model="content"
    placeholder="type here...">
    <span class="input-group-btn">
      <button class="btn btn-success" type="submit"
      ng-click="content">Send
      </button>
    </span>
</form>
{% endhighlight %}
{:#message}
{% highlight javascript %}
Message.send = function(message) {
  messages.$add( message );
};
{% endhighlight %}
{:#message}
{% highlight javascript %}
this.addMessage = function(content) {
  this.chatInput.user = $cookies.get('blocChatCurrentUser');
  this.chatInput.sentAt = TIMESTAMP;
  this.chatInput.roomId = this.activeRoom.$id;
  this.chatInput.content = content;
  Message.send(this.chatInput);
{% endhighlight %}

The **fifth problem** I encountered can be summed up very easily in the gif below.
![development](https://i.imgur.com/gwiLmBh.gif)

Because the container is set to a height of 100% and the position is fixed, consquently, after a certain threshold of messages reached push contents out of the container and become un-viewable. The easiest way to combat this is to introduce a scroll property to that container. We use scroll-y because we are dealing with height only. Messages that exceed a certain length horizontally are pushed into a new line by default.

The chat input bar is then set to a fixed position so it always appears in the footer of the view regardless of what happens.

From a functionality stand point, the project is finished.


{:#header-five}
### Solution
---
Provided as a TLDR; of diffcult encounters I've experienced while working on this.

Problem       | Solution
------------- | -------------
firebase $add  | passing in the proper object to associate it with the `value`
angular validation | required & ng-disable
angular $cookies .get/.put  | $cookies are a dependency
angular form submit  | passing in ng-model as the argument of the form
css container height  | scroll y


{:#header-six}
### Results
---

Quality of life changes have been added to improve the user experience. They include -
1. Chat room automatically scrolls to the bottom to view most recent message immediately after input into the chat message bar.
2. Chat message bar automatically empties after each message is sent to avoid sending of duplicate messages.
3. Restricting the use of no-name empty string usernames and chat room names.
4. Upon entering valid state of username or chat room, box transitions from red to green.
![development](https://i.imgur.com/2Wdv8eY.gif)
5. Cover page when no chatroom is selected

Planned Additions:
1. Bootstrap icons
2. Google+ or facebook integration to access chatroom
3. Username will be tied into google+ or facebook real name
4. Change user will be reformmated to create user in the case user does not want to use facebook or google+
5. Have a right <aside> column that that showcases user profile
6. User profile can include picture, some quick facts, and interests.
7. Further styling changes!

{:#header-seven}
### Conclusion
---
![development](https://i.imgur.com/4vcDd89.png "first release")

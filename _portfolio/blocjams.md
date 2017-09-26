---
layout: post
title: BlocJams
feature-img: "img/sample_feature_img.png"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030966/blocjams_1x.png"
short-description: BlocJams for iOS is awesome!

---
{:#header-one}
# Summary
To create a music page for band "Bloc Jams". This page must be able to display band albums. Clicking on albums will show collection of songs in that album. The app has a fullly functional music player in real time.

{:#header-two}
# Explanation
This is the second iteration of the project. The project originally started using javaScript + jQuery. This iteration features Angular 1.6.4 and jQuery lite that comes bundled with it. This project is my first interaction with the Angular framework.

CSS and templates were given in this project. Very minimal styling edits were done.

{:align="center"}
#### Technologies Used

{:.techs align="center"}
![program](https://avatars2.githubusercontent.com/u/139426?v=4&s=400 "angular logo")
![program](https://qph.ec.quoracdn.net/main-thumb-t-1406102-200-trchoddaujrpnfgqxuxoiyffsclbbuvb.jpeg "ionic logo")
![program](https://avatars1.githubusercontent.com/u/6466306?v=4&s=200 "google font api logo")

{:#header-three}
# Problem

Node.js was required to deploy angular. THe first challenge was actually getting Node.js to work. It didn't work because of some issue related to Windows permission control. My failure to see that resulted in installing and reinstalling Node.js several times which led to the corruption of my OS.

Below are questions I encountered while working on the project:
* What is a controller?
* What is a service?
* What is the view?
* Should this go in the controller or the directive?
* How to display an array in angular?
* Why is everything in the Angular documentation written different than the method we use?

i.e.
{:#roomJS}
{% highlight javascript %}
var myApp = angular.module('myApp',[]);

myApp.controller('GreetingController', ['$scope', function($scope) {
  $scope.greeting = 'Hola!';
}]);
{% endhighlight %}
{:#roomJS}
{% highlight javascript %}
var myApp = angular.module('myApp',[]);

function()  {
  function GreetingController($scope) {
    $scope.greeting = 'Hola!';

    .module('myApp',[])
    .controller([$scope, ['GreetingController']);
  }
}();
}]);
{% endhighlight %}

{:#header-four}
# Solution
Created 1 controller per view
Created 1 service per controller

Understood the difference between public and private

Learned how to use JSON comments

Learned how to use `ng-repeat` which uses the same structure as a `for in` loop.

`ng-hide` and `ng-show` behave like on and off methods.

Used the buzz library to play, pause, and resume our audio.

Used jQuery to bind and seek the the playerBar element in the doomed

Used a filter code to display seconds into real time.

{:#header-five}
# Results
The result was roughly 400 lines of javascript being compressed into 150-200 lines.

The end in mind with Angular is to create something that is much easier to re-use and maintain.

Why and when do we use Angular? - When we are building an application that sticks with a single page view rather than having hundreds of new DOM objects on every single page.

Projected changes to come:
1. Enable account creation
2. Enable user rating
3. Dynamic albums vs current static
4. Dynamic volume rather than static @ 80%
5. Bio/about page
6. Bootstrap to a spoof buy album modal

{:#header-six}
# Conclusion

![development](/img/blocJamsAngular/landing.png)
![development](/img/blocJamsAngular/collection.png)
![development](/img/blocJamsAngular/player.png)

# Promise module
Promise is an AngularJS module. This module provides a simple factory that acts as an wrapper around the $http service that returns a promise. It has two methods 'me' and 'us' which can be used to perform a single or multiple ajax request(s).
The multiple requests will be completed or failed at once.

# Example markup
      <!DOCTYPE html>
      <!--[if lt IE 7]>      <html lang="en" ng-app="myApp" class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]-->
      <!--[if IE 7]>         <html lang="en" ng-app="myApp" class="no-js lt-ie9 lt-ie8"> <![endif]-->
      <!--[if IE 8]>         <html lang="en" ng-app="myApp" class="no-js lt-ie9"> <![endif]-->
      <!--[if gt IE 8]><!--> <html lang="en" ng-app="myApp" class="no-js"> <!--<![endif]-->
      <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>My AngularJS App</title>
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="app.css">
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-route.min.js"></script>
      </head>
      <body ng-controller="rootCtrl">
      
        <div ng-view></div>
      
        <script src="app.js"></script>
        <script src="codefabriek.promise.js"></script>
      
      </body>
      </html>


# Example app
      angular.module('myApp', ['codefabriek.promise'])
      .controller("rootCtrl", ["Promise", function (Promise) {

          /**
           * Use this version to perform a single ajax request.
           */
          Promise.me({
              url: "http://ip.jsontest.com",
              method: "GET"
          }).then(function (response) {
              console.log(response);
          }, function (reason) {
              alert(reason);
          });
  
          /**
           * Use this version to perform multiple ajax request that will complete/fail at once.
           */
          Promise.us([
              {url: "http://ip.jsontest.com", method: "GET"},
              {url: "http://date.jsontest.com/", method: "GET"}
          ]).then(function (responses) {
              console.log(responses[0]);
              console.log(responses[1]);
          }, function (reason) {
              alert(reason);
          });
    }]);

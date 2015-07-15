# Introduction

*Thanks to AngularJS community!*

The goal of this style guide is to present a set of best practices and style guidelines for one AngularJS application.
These best practices are collected from:

0. AngularJS source code
0. Source code or articles I've read
0. My own experience

**Note 1**: this is still a draft of the style guide, its main goal is to be community-driven so filling the gaps will be greatly appreciated by the whole community.

**Note 2**: before following any of the guidelines in the translations of the English document, make sure they are up-to date. The latest version of the AngularJS style guide is in the current document.

In this style guide you won't find common guidelines for JavaScript development. Such can be found at:

0. [Google's JavaScript style guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
0. [Mozilla's JavaScript style guide](https://developer.mozilla.org/en-US/docs/Developer_Guide/Coding_Style)
0. [GitHub's JavaScript style guide](https://github.com/styleguide/javascript)
0. [Douglas Crockford's JavaScript style guide](http://javascript.crockford.com/code.html)
0. [Airbnb JavaScript style guide](https://github.com/airbnb/javascript)

For AngularJS development recommended is the [Google's JavaScript style guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml).

In AngularJS's GitHub wiki there is a similar section by [ProLoser](https://github.com/ProLoser), you can check it [here](https://github.com/angular/angular.js/wiki).

# Translations

- [German](https://github.com/mgechev/angularjs-style-guide/blob/master/README-de-de.md)
- [Spanish](https://github.com/mgechev/angularjs-style-guide/blob/master/README-es-es.md)
- [French](https://github.com/mgechev/angularjs-style-guide/blob/master/README-fr-fr.md)
- [Indonesian](https://github.com/mgechev/angularjs-style-guide/blob/master/README-id-id.md)
- [Italian](https://github.com/mgechev/angularjs-style-guide/blob/master/README-it-it.md)
- [Japanese](https://github.com/mgechev/angularjs-style-guide/blob/master/README-ja-jp.md)
- [Korean](https://github.com/mgechev/angularjs-style-guide/blob/master/README-ko-kr.md)
- [Polish](https://github.com/mgechev/angularjs-style-guide/blob/master/README-pl-pl.md)
- [Portuguese](https://github.com/mgechev/angularjs-style-guide/blob/master/README-pt-br.md)
- [Russian](https://github.com/mgechev/angularjs-style-guide/blob/master/README-ru-ru.md)
- [Serbian](https://github.com/mgechev/angularjs-style-guide/blob/master/README-sr.md)
- [Serbian lat](https://github.com/mgechev/angularjs-style-guide/blob/master/README-sr-lat.md)
- [Chinese](https://github.com/mgechev/angularjs-style-guide/blob/master/README-zh-cn.md)
- [Turkish](https://github.com/mgechev/angularjs-style-guide/blob/master/README-tr-tr.md)

# Table of content
* [General](#general)
    * [Directory structure](#directory-structure)
    * [Markup](#markup)
    * [Others](#others)
* [Modules](#modules)
* [Controllers](#controllers)
* [Directives](#directives)
* [Filters](#filters)
* [Services](#services)
* [Templates](#templates)
* [Routing](#routing)
* [i18n](#i18n)
* [Performance](#performance)
* [Contribution](#contribution)
* [Contributors](#contributors)

# General

## Directory structure

Since a large AngularJS application has many components it's best to structure it in a directory hierarchy.
There are two main approaches:

* Creating high-level divisions by component types and lower-level divisions by functionality.

In this way the directory structure will look like:

```
.
├── app
│   ├── app.js
│   ├── controllers
│   │   ├── home
│   │   │   ├── FirstCtrl.js
│   │   │   └── SecondCtrl.js
│   │   └── about
│   │       └── ThirdCtrl.js
│   ├── directives
│   │   ├── home
│   │   │   └── directive1.js
│   │   └── about
│   │       ├── directive2.js
│   │       └── directive3.js
│   ├── filters
│   │   ├── home
│   │   └── about
│   └── services
│       ├── CommonService.js
│       ├── cache
│       │   ├── Cache1.js
│       │   └── Cache2.js
│       └── models
│           ├── Model1.js
│           └── Model2.js
├── partials
├── lib
└── test
```

* Creating high-level divisions by functionality and lower-level divisions by component types.

Here is its layout:

```
.
├── app
│   ├── app.js
│   ├── common
│   │   ├── controllers
│   │   ├── directives
│   │   ├── filters
│   │   └── services
│   ├── home
│   │   ├── controllers
│   │   │   ├── FirstCtrl.js
│   │   │   └── SecondCtrl.js
│   │   ├── directives
│   │   │   └── directive1.js
│   │   ├── filters
│   │   │   ├── filter1.js
│   │   │   └── filter2.js
│   │   └── services
│   │       ├── service1.js
│   │       └── service2.js
│   └── about
│       ├── controllers
│       │   └── ThirdCtrl.js
│       ├── directives
│       │   ├── directive2.js
│       │   └── directive3.js
│       ├── filters
│       │   └── filter3.js
│       └── services
│           └── service3.js
├── partials
├── lib
└── test
```

* In case the directory name contains multiple words, use lisp-case syntax:

```
app
 ├── app.js
 └── my-complex-module
     ├── controllers
     ├── directives
     ├── filters
     └── services
```

* Put all the files associated with the given directive (i.e. templates, CSS/SASS files, JavaScript) in a single folder. If you choose to use this style be consistent and use it everywhere along your project.

```
app
└── directives
    ├── directive1
    │   ├── directive1.html
    │   ├── directive1.js
    │   └── directive1.sass
    └── directive2
        ├── directive2.html
        ├── directive2.js
        └── directive2.sass
```

This approach can be combined with both directory structures above.
* The unit tests for a given component should be located in the directory where the component is. This way when you make changes to a given component finding its test is easy. The tests also act as documentation and show use cases.

```
services
├── cache
│   ├── cache1.js
│   └── cache1.spec.js
└── models
    ├── model1.js
    └── model1.spec.js
```

* The `app.js` file should contains route definitions, configuration and/or manual bootstrap (if required).
* Each JavaScript file should only hold **a single component**. The file should be named with the component's name.
* Use AngularJS project structure template like [Yeoman](http://yeoman.io), [ng-boilerplate](http://joshdmiller.github.io/ng-boilerplate/#/home).

Conventions about component naming can be found in each component section.

## Markup

[TLDR;](http://developer.yahoo.com/blogs/ydn/high-performance-sites-rule-6-move-scripts-bottom-7200.html) Put the scripts at the bottom.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>MyApp</title>
</head>
<body>
  <div ng-app="myApp">
    <div ng-view></div>
  </div>
  <script src="angular.js"></script>
  <script src="app.js"></script>
</body>
</html>
```

Keep things simple and put AngularJS specific directives later. This way is easy to look to the code and find enhanced HTML by the framework (what improve the maintainibility).

```
<form class="frm" ng-submit="login.authenticate()">
  <div>
    <input class="ipt" type="text" placeholder="name" require ng-model="user.name">
  </div>
</form>
```

Other HTML atributes should follow the Code Guide's [recommendation](http://mdo.github.io/code-guide/#html-attribute-order)

## Others

* Use:
    * `$timeout` instead of `setTimeout`
    * `$interval` instead of `setInterval`
    * `$window` instead of `window`
    * `$document` instead of `document`
    * `$http` instead of `$.ajax`

This will make your testing easier and in some cases prevent unexpected behaviour (for example, if you missed `$scope.$apply` in `setTimeout`).

* Automate your workflow using tools like:
    * [Yeoman](http://yeoman.io)
    * [Gulp](http://gulpjs.com)
    * [Grunt](http://gruntjs.com)
    * [Bower](http://bower.io)

* Use promises (`$q`) instead of callbacks. It will make your code look more elegant and clean, and save you from callback hell.
* Use `$resource` instead of `$http` when possible. The higher level of abstraction will save you from redundancy.
* Use an AngularJS pre-minifier ([ng-annotate](https://github.com/olov/ng-annotate)) for preventing problems after minification.
* Don't use globals. Resolve all dependencies using Dependency Injection, this will prevent bugs and monkey patching when testing.
* Avoid globals by using Grunt/Gulp to wrap your code in Immediately Invoked Function Expression (IIFE). You can use plugins like [grunt-wrap](https://www.npmjs.com/package/grunt-wrap) or [gulp-wrap](https://www.npmjs.com/package/gulp-wrap/) for this purpose. Example (using Gulp)

	```Javascript
	gulp.src("./src/*.js")
    .pipe(wrap('(function(){\n"use strict";\n<%= contents %>\n})();'))
    .pipe(gulp.dest("./dist"));
    ```
* Do not pollute your `$scope`. Only add functions and variables that are being used in the templates.
* Prefer the usage of [controllers instead of `ngInit`](https://github.com/angular/angular.js/pull/4366/files). The only appropriate use of `ngInit` is for aliasing special properties of `ngRepeat`. Besides this case, you should use controllers rather than `ngInit` to initialize values on a scope. The expression passed to `ngInit` should go through lexing, parsing and evaluation by the Angular interpreter implemented inside the `$parse` service. This leads to:
    - Performance impact, because the interpreter is implemented in JavaScript
    - The caching of the parsed expressions inside the `$parse` service doesn't make a lot of sense in most cases, since `ngInit` expressions are often evaluated only once
    - Is error-prone, since you're writing strings inside your templates, there's no syntax highlighting and further support by your editor
    - No run-time errors are thrown
* Do not use `$` prefix for the names of variables, properties and methods. This prefix is reserved for AngularJS usage.
* When resolving dependencies through the DI mechanism of AngularJS, sort the dependencies by their type - the built-in AngularJS dependencies should be first, followed by your custom ones:

```javascript
module.factory('Service', function ($rootScope, $timeout, MyCustomDependency1, MyCustomDependency2) {
  return {
    //Something
  };
});
```

# Modules

* Modules should be named with lowerCamelCase. For indicating that module `b` is submodule of module `a` you can nest them by using namespacing like: `a.b`.

	There are two common ways for structuring the modules:

	0. By functionality
	0. By component type

	Currently there's not a big difference, but the first way looks cleaner. Also, if lazy-loading modules is implemented (currently not in the AngularJS roadmap), it will improve the app's performance.

# Controllers

* Do not manipulate DOM in your controllers, this will make your controllers harder for testing and will violate the [Separation of Concerns principle](https://en.wikipedia.org/wiki/Separation_of_concerns). Use directives instead.
* The naming of the controller is done using the controller's functionality (for example shopping cart, homepage, admin panel) and the substring `Ctrl` in the end.
* Controllers are plain javascript [constructors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor), so they will be named UpperCamelCase (`HomePageCtrl`, `ShoppingCartCtrl`, `AdminPanelCtrl`, etc.).
* The controllers should not be defined as globals (even though AngularJS allows this, it is a bad practice to pollute the global namespace).
* Use the following syntax for defining controllers:

  ```JavaScript
  function MyCtrl(dependency1, dependency2, ..., dependencyn) {
    // ...
  }
  module.controller('MyCtrl', MyCtrl);
  ```

   In order to prevent problems with minification, you can automatically generate the array definition syntax from    the standard one using tools like [ng-annotate](https://github.com/olov/ng-annotate) (and grunt task          [grunt-ng-annotate](https://github.com/mzgol/grunt-ng-annotate)).
* Prefer using `controller as` syntax:

  ```
  <div ng-controller="MainCtrl as main">
     {{ main.title }}
  </div>
  ```

  ```JavaScript
  app.controller('MainCtrl', MainCtrl);

  function MainCtrl () {
    this.title = 'Some title';
  }
  ```

   The main benefits of using this syntax:
   * Creates an 'isolated' component - binded properties are not part of `$scope` prototype chain. This is good practice since `$scope` prototype inheritance has some major drawbacks (this is probably the reason it was removed on Angular 2):
      * It is hard to track where data is coming from.
      * Scope's value changes can affect places you did not intend to affect.
      * Harder to refactor.
      * The '[dot rule](http://jimhoskins.com/2012/12/14/nested-scopes-in-angularjs.html)'.
   * Removes the use of `$scope` when no need for special operations (like `$scope.$broadcast`). This is a good preparation for AngularJS V2.
   * Syntax is closer to that of a 'vanilla' JavaScript constructor

   Digging more into `controller as`: [digging-into-angulars-controller-as-syntax](http://toddmotto.com/digging-into-angulars-controller-as-syntax/)
* If using array definition syntax, use the original names of the controller's dependencies. This will help you produce more readable code:

  ```JavaScript
  function MyCtrl(s) {
    // ...
  }

  module.controller('MyCtrl', ['$scope', MyCtrl]);
  ```

   which is less readable than:

  ```JavaScript
  function MyCtrl($scope) {
    // ...
  }
  module.controller('MyCtrl', ['$scope', MyCtrl]);
  ```

   This especially applies to a file that has so much code that you'd need to scroll through. This would possibly cause you to forget which variable is tied to which dependency.

* Make the controllers as lean as possible. Abstract commonly used functions into a service.
* Avoid writing business logic inside controllers. Delegate business logic to a `model`, using a service.
  For example:

  ```Javascript
  //This is a common behaviour (bad example) of using business logic inside a controller.
  angular.module('Store', [])
  .controller('OrderCtrl', function ($scope) {

    $scope.items = [];

    $scope.addToOrder = function (item) {
      $scope.items.push(item);//-->Business logic inside controller
    };

    $scope.removeFromOrder = function (item) {
      $scope.items.splice($scope.items.indexOf(item), 1);//-->Business logic inside controller
    };

    $scope.totalPrice = function () {
      return $scope.items.reduce(function (memo, item) {
        return memo + (item.qty * item.price);//-->Business logic inside controller
      }, 0);
    };
  });
  ```

  When delegating business logic into a 'model' service, controller will look like this (see 'use services as your Model' for service-model implementation):

  ```Javascript
  //Order is used as a 'model'
  angular.module('Store', [])
  .controller('OrderCtrl', function (Order) {

    $scope.items = Order.items;

    $scope.addToOrder = function (item) {
      Order.addToOrder(item);
    };

    $scope.removeFromOrder = function (item) {
      Order.removeFromOrder(item);
    };

    $scope.totalPrice = function () {
      return Order.total();
    };
  });
  ```

  Why business logic / app state inside controllers is bad?
  * Controllers instantiated for each view and dies when the view unloads
  * Controllers are not reusable - they are coupled with the view
  * Controllers are not meant to be injected


* Communicate within different controllers using method invocation (possible when a child wants to communicate with its parent) or `$emit`, `$broadcast` and `$on` methods. The emitted and broadcasted messages should be kept to a minimum.
* Make a list of all messages which are passed using `$emit`, `$broadcast` and manage it carefully because of name collisions and possible bugs.

   Example:

   ```JavaScript
   // app.js
   /* * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
   Custom events:
     - 'authorization-message' - description of the message
       - { user, role, action } - data format
         - user - a string, which contains the username
         - role - an ID of the role the user has
         - action - specific ation the user tries to perform
   * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */
   ```

* When you need to format data encapsulate the formatting logic into a [filter](#filters) and declare it as dependency:

   ```JavaScript
   function myFormat() {
     return function () {
       // ...
     };
   }
   module.filter('myFormat', myFormat);

   function MyCtrl($scope, myFormatFilter) {
     // ...
   }

   module.controller('MyCtrl', MyCtrl);
   ```
* In case of nested controllers use "nested scoping" (the `controllerAs` syntax):

   **app.js**
   ```javascript
   module.config(function ($routeProvider) {
     $routeProvider
       .when('/route', {
         templateUrl: 'partials/template.html',
         controller: 'HomeCtrl',
         controllerAs: 'home'
       });
   });
   ```
   **HomeCtrl**
   ```javascript
   function HomeCtrl() {
     this.bindingValue = 42;
   }
   ```
   **template.html**
   ```
   <div ng-bind="home.bindingValue"></div>
   ```

# Directives

* Name your directives with lowerCamelCase.
* Use `scope` instead of `$scope` in your link function. In the compile, post/pre link functions you have already defined arguments which will be passed when the function is invoked, you won't be able to change them using DI. This style is also used in AngularJS's source code.
* Use custom prefixes for your directives to prevent name collisions with third-party libraries.
* Do not use `ng` or `ui` prefixes since they are reserved for AngularJS and AngularJS UI usage.
* DOM manipulations must be done only through directives.
* Create an isolated scope when you develop reusable components.
* Use directives as attributes or elements instead of comments or classes, this will make your code more readable.
* Use `scope.$on('$destroy', fn)` for cleaning up. This is especially useful when you're wrapping third-party plugins as directives.
* Do not forget to use `$sce` when you should deal with untrusted content.

# Filters

* Name your filters with lowerCamelCase.
* Make your filters as light as possible. They are called often during the `$digest` loop so creating a slow filter will slow down your app.
* Do a single thing in your filters, keep them coherent. More complex manipulations can be achieved by piping existing filters.

# Services

This section includes information about the service component in AngularJS. It is not dependent of the way of definition (i.e. as provider, `.factory`, `.service`), except if explicitly mentioned.

* Use camelCase to name your services.
  * UpperCamelCase (PascalCase) for naming your services, used as constructor functions i.e.:

    ```JavaScript
    function MainCtrl($scope, User) {
      $scope.user = new User('foo', 42);
    }

    module.controller('MainCtrl', MainCtrl);

    function User(name, age) {
      this.name = name;
      this.age = age;
    }

    module.factory('User', function () {
      return User;
    });
    ```

  * lowerCamelCase for all other services.

* Encapsulate all the business logic in services. Prefer using it as your `model`. For example:
  ```Javascript
  //Order is the 'model'
  angular.module('Store')
  .factory('Order', function () {
      var add = function (item) {
        this.items.push (item);
      };

      var remove = function (item) {
        if (this.items.indexOf(item) > -1) {
          this.items.splice(this.items.indexOf(item), 1);
        }
      };

      var total = function () {
        return this.items.reduce(function (memo, item) {
          return memo + (item.qty * item.price);
        }, 0);
      };

      return {
        items: [],
        addToOrder: add,
        removeFromOrder: remove,
        totalPrice: total
      };
  });
  ```

  See 'Avoid writing business logic inside controllers' for an example of a controller consuming this service.
* Services representing the domain preferably a `service` instead of a `factory`. In this way we can take advantage of the "klassical" inheritance easier:

	```JavaScript
	function Human() {
	  //body
	}
	Human.prototype.talk = function () {
	  return "I'm talking";
	};

	function Developer() {
	  //body
	}
	Developer.prototype = Object.create(Human.prototype);
	Developer.prototype.code = function () {
	  return "I'm coding";
	};

	myModule.service('Human', Human);
	myModule.service('Developer', Developer);

	```

* For session-level cache you can use `$cacheFactory`. This should be used to cache results from requests or heavy computations.
* If given service requires configuration define the service as provider and configure it in the `config` callback like:

	```JavaScript
	angular.module('demo', [])
	.config(function ($provide) {
	  $provide.provider('sample', function () {
	    var foo = 42;
	    return {
	      setFoo: function (f) {
	        foo = f;
	      },
	      $get: function () {
	        return {
	          foo: foo
	        };
	      }
	    };
	  });
	});

	var demo = angular.module('demo');

	demo.config(function (sampleProvider) {
	  sampleProvider.setFoo(41);
	});
	```

# Templates

* Use `ng-bind` or `ng-cloak` instead of simple `{{ }}` to prevent flashing content.
* Avoid writing complex expressions in the templates.
* When you need to set the `src` of an image dynamically use `ng-src` instead of `src` with `{{ }}` template.
* When you need to set the `href` of an anchor tag dynamically use `ng-href` instead of `href` with `{{ }}` template.
* Instead of using scope variable as string and using it with `style` attribute with `{{ }}`, use the directive `ng-style` with object-like parameters and scope variables as values:

```HTML
<script>
...
$scope.divStyle = {
  width: 200,
  position: 'relative'
};
...
</script>

<div ng-style="divStyle">my beautifully styled div which will work in IE</div>;
```

# Routing

* Use `resolve` to resolve dependencies before the view is shown.
* Do not place explicit RESTful calls inside the `resolve` callback. Isolate all the requests inside appropriate services. This way you can enable caching and follow the separation of concerns principle.

# i18n

* For newer versions of the framework (>=1.4.0) use the built-in i18n tools, when using older versions (<1.4.0) use [`angular-translate`](https://github.com/angular-translate/angular-translate).

# Performance

* Optimize the digest cycle

	* Watch only the most vital variables. When required to invoke the `$digest` loop explicitly (it should happen only in exceptional cases), invoke it only when required (for example: when using real-time communication, don't cause a `$digest` loop in each received message).
	* For content that is initialized only once and then never changed, use single-time watchers like [`bindonce`](https://github.com/Pasvaz/bindonce) for older versions of AngularJS or one-time bindings in AngularJS >=1.3.0.
	* Make the computations in `$watch` as simple as possible. Making heavy and slow computations in a single `$watch` will slow down the whole application (the `$digest` loop is done in a single thread because of the single-threaded nature of JavaScript).
	* When watching collections, do not watch them deeply when not strongly required. Better use `$watchCollection`, which performs a shallow check for equility of the result of the watched expression and the previous value of the expression's evaluation.
	* Set third parameter in `$timeout` function to false to skip the `$digest` loop when no watched variables are impacted by the invocation of the `$timeout` callback function.
	* When dealing with big collections, which change rarely, [use immutable data structures](http://blog.mgechev.com/2015/03/02/immutability-in-angularjs-immutablejs/).


* Consider decreasing number of network requests by bundling/caching html template files into your main javascript file, using [grunt-html2js](https://github.com/karlgoldstein/grunt-html2js) / [gulp-html2js](https://github.com/fraserxu/gulp-html2js). See [here](http://ng-learn.org/2014/08/Populating_template_cache_with_html2js/) and [here](http://slides.com/yanivefraim-1/real-world-angularjs#/34) for details. This is particularly useful when the project has a lot of small html templates that can be a part of the main (minified and gzipped) javascript file.

# Contribution

Since the goal of this style guide is to be community-driven, contributions are greatly appreciated.
For example, you can contribute by extending the Testing section or by translating the style guide to your language.

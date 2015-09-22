# ion-drawer-vertical

A vertical drawer for Ionic

## Danger, here be dragons

Do note that this is an early release of `ion-drawer-vertical`. Whilst the basics work, many things are still missing _(Enforce the proper elements being present, autoclose when scrolling in a list, etc. to name a few)_. 

As with all pre-release software: Things might change in the future. Or they might remain the same. Or they could change after all. This plugin works for me. Your mileage may vary.

## Installation

Add the `ionic.contrib.drawer.vertical.js` and `ionic.contrib.drawer.vertical.css` files to your index file

```
<link href="ion-drawer-vertical/ionic.contrib.drawer.vertical.css" rel="stylesheet">
<script src="ion-drawer-vertical/ionic.contrib.drawer.vertical.js"></script>
```

Add `ionic.contrib.drawer.vertical` to your Angular app:

```
angular.module('app', [
	'ionic',
	'ionic.contrib.drawer.vertical'
])
```

## Usage

Add a `<ion-drawer-vertical-wrapper>` element to your document. Inside it, put a `<ion-drawer-vertical-content>` and an optional `<ion-drawer-vertical-handle>` element.

### Configuration

Adjust the `direction` _(possible values: `down` [default] and `up`)_ and `state` _(possible values: `opened` [default] and `closed`)_ attributes of the `<ion-drawer-vertical-wrapper>` element if need.

Set the proper `has-*` classes _(such as `has-header` or `has-footer`)_ on the `<ion-drawer-vertical-wrapper>` element if any headers and/or footers are present.

### Example

```
<ion-drawer-vertical-wrapper class="has-header has-footer" direction="down" state="closed">
	<ion-drawer-vertical-content>
		<img src="http://lorempixel.com/g/400/200/animals/4/horizontal-giraffe/" alt="Horizontal Giraffe" title="Horizontal Giraffe" />
	</ion-drawer-vertical-content>
	<ion-drawer-vertical-handle />
</ion-drawer-vertical-wrapper>
```

### Events and Functions

`ion-drawer-vertical` automatically binds `drag` events to the `<ion-drawer-vertical-handle>` element if it's present. Dragging said element up/down will make the drawer respond to that state. Upon releasing the drawer will either revert to its original state, or to the opposite one (viz. open will become closed) when having dragged far enough (over 33% of the height of the panel).


`ion-drawer-vertical` also ships with a delegate `$ionDrawerVerticalDelegate`. The methods `openDrawer()`, `closeDrawer()`, `toggleDrawer()`, and `isOpen()` are exposed via this delegate. Calling them will control all `ion-drawer-vertical` instances:

```
angular
.module('app', ['ionic.contrib.drawer.vertical', 'ionic'])
.controller('demo', function($scope, $ionDrawerVerticalDelegate) {

	$scope.toggleDrawer = function() {
		$ionDrawerVerticalDelegate.toggleDrawer();
	}

});
```

```
<body ng-app="app" ng-controller="demo">
	<ion-header-bar class="bar-positive">
		<h1 class="title">ion-drawer-vertical</h1>
		<button class="button" ng-click="toggleDrawer()">Toggle Drawer</button>
	</ion-header-bar>
	<ion-drawer-vertical-wrapper class="has-header" direction="down" state="closed">
		<ion-drawer-vertical-content>[...]</ion-drawer-vertical-content>
		<ion-drawer-vertical-handle />
	</ion-drawer-vertical-wrapper>
	<ion-content>
		[...]
	</ion-content>
</body>
```

When having multiple instances of `ion-drawer-vertical`, use the `$getByHandle` method along with the `delegate-handle` attribute to control a specific/single instance of `ion-drawer-vertical`:
```
<body ng-app="app" ng-controller="demo">
	<ion-header-bar class="bar-positive">
		<button class="button" ng-click="toggleDrawer('first')">Toggle First</button>
		<h1 class="title">ion-drawer-vertical</h1>
		<button class="button" ng-click="toggleDrawer('second')">Toggle Second</button>
	</ion-header-bar>
	<ion-drawer-vertical-wrapper class="has-header" direction="down" state="closed" delegate-handle="first">
		<ion-drawer-vertical-content>[...]</ion-drawer-vertical-content>
		<ion-drawer-vertical-handle />
	</ion-drawer-vertical-wrapper>
	<ion-drawer-vertical-wrapper class="has-footer" direction="up" state="closed" delegate-handle="second">
		<ion-drawer-vertical-content>[...]</ion-drawer-vertical-content>
		<ion-drawer-vertical-handle />
	</ion-drawer-vertical-wrapper>
	<ion-content>
		[...]
	</ion-content>
	<ion-footer-bar class="bar-positive">
	</ion-footer-bar>
</body>
```
```
angular
.module('app', ['ionic.contrib.drawer.vertical', 'ionic'])
.controller('demo', function($scope, $ionDrawerVerticalDelegate) {

	$scope.toggleDrawer = function(handle) {
		$ionDrawerVerticalDelegate.$getByHandle(handle).toggleDrawer();
	}

});
```


## Acknowledgements

[`ionic-contrib-drawer`](https://github.com/driftyco/ionic-ion-drawer) has been a source of inspiration / a starting point for `ion-drawer-vertical`.

## License

`ion-drawer-vertical` is released under the MIT public license. See the enclosed `LICENSE` for details.
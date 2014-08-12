Backbone.NativeView
===================

A drop-in replacement for Backbone.View that uses only native DOM methods for
element selection and event delegation. It has no dependency on jQuery.


To Use:
-------
Load Backbone.NativeView with your favorite module loader or add as a script
tag after you have loaded Backbone in the page. Wherever you had previously
inherited from Backbone.View, you will now inherit from Backbone.NativeView.

```js
var MyView = Backbone.NativeView.extend({
  initialize: function(options) {
    // ...
  }
});
```

As an alternative, you may extend an existing View's prototype to use native
methods, or even Backbone.View itself:

```js
var Backbone.View = Backbone.View.extend(Backbone.NativeViewMixin);

var MyView = Backbone.View.extend({
  initialize: function(options) {
    // ...
  }
});
```

Features:
---------
Delegation:
```js
var view = new MyView({el: '#my-element'});
view.delegate('click', view.clickHandler);
```

Undelegation with event names or listeners,
```js
view.undelegate('click', view.clickHandler);
view.undelegate('click');
```

View-scoped element finding:
```js
// for one matched element
_.first(view.$('.box')).focus();

// for multiple matched elements
_.each(view.$('.item'), function(el) {
  el.classList.remove('active')
});
var fields = _.invoke(view.$('.field'), 'innerHTML');
```

Requirements:
-------------
NativeView makes use of a few ES5/HTML5 features. For IE7 and below you must
include a polyfill like [eS5-shim](https://github.com/es-shims/es5-shim).
Specifically we use:

* `querySelector`/`querySelectorAll`
* `Array.prototype.indexOf`
* `Function.prototype.bind`

Notes:
------
* The `$el` property no longer exists on Views. Use `el` instead.
* The `$` method returns a NodeList instead of a jQuery context. You can
  iterate over either using `_.each`.


With many thanks to @wyuenho for his initial code.


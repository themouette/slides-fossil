Introducing Fossil
==================

### Stop repeating yourself

---

## Fossil.Application

Responsible for **boot** sequence and modules **orchestration**

---

### Example

``` javascript
var myApp = new Fossil.Application({
    routes: {
        '': function () {
            this.routing.navigate('search', {replace: false});
    },
    fragments: {
        'topmenu': TopmenuFragment
    }
});

myApp // declare services
    .use('routing', Fossil.Services.Routing)
    .use('session', Fossil.Services.Session);
myApp // connect modules
    .connect('search', SearchModule)
    .connect('configure/:model', ConfigureModule)
myApp.start();
```

---

### And also

* Event dispatcher
* Promise API
* Main layout
* ...

---

## Module

Consistent package of **UI**, **business** and **data**.

---

### Example module

``` javascript
var SearchModule = Fossil.Module.extend({
    routing: {
        ':query': 'onquery'
    },
    fragments: {
        'sidebar': SidebarFragment,
        'content': ContentFragment
    },
    onqueryRoute: function (query) {
        this
            .abort() // abort previous calls
            .waitFor(this.ensureCollection().fetch({query: query}))
            .thenWith(this, this.renderResults, this.displayError);
    },
    renderResults: function () {
        this.trigger('search:query:render'); }
});
```

---

### And also

* Event dispatcher
* Bridge to application
* Promise API
* Contextualized layout
* Start/Standby/Stop
* ...

---

## Fossil.Fragment

Standalone set of views, with its own logic.

<p style="margin:40px 0;">
Can be included in **Application**, **Modules** and **Fragments**.
</p>

> Never manage UI in **Modules** or **Application**, send events to **Fragments**.

---

### Example fragment

``` javascript
var SidebarFragment = Fossil.Fragment.extend({
    ancestorEvents: {
        'search:query:render': function (results) {
            this.setView(new Fossil.View.Collection({
                ItemView: ResultRowView,
                collection: results
            }));
        }
    }
});
```

---

### And also

* Event dispatcher
* Bridge to ancestor
* View manager
* Follow ancestor lifecycle
* Start/Standby/Stop
* ...

---

## Fossil.Service

* Available application wide
* Provide interceptors in every component lifecycle
* Provide commands
* Be imaginative !

---

## Coming soon

1. Enhanced view manager
2. Scaffolding
3. Gruntfile automation
4. More examples

---

## Early alpha available on GitHub

* [sources](https://github.com/themouette/fossil-core)
* [doc](https://github.com/themouette/fossil-core/tree/master/doc)
* [tests](https://github.com/themouette/fossil-core/tree/master/tests)

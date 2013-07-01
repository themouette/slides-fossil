Remain testable
===============

---

### Application

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
myApp // connect modules
    .connect('search', SearchModule)
    .connect('configure/:model', ConfigureModule)
myApp.start();
```

> No **unit** tests needed, it is just configuration

---

### Module

``` javascript
var SearchModule = Fossil.Module.extend({
    routing: {
        ':query': 'onquery' },
    onqueryRoute: function (query) {
        this
            .abort() // abort previous calls
            .waitFor(this.ensureCollection().fetch({query: query}))
            .thenWith(this, this.renderResults, this.displayError);
    },
    renderResults: function () {
        this.trigger('search:query:render');
    }
});
```

* **renderResults** should trigger 'search:query:render'
* **onqueryRoute** should call `renderResults` on success
* **onqueryRoute** should call `displayError` on error

---

### Fragment

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

* should call **setView** on 'search:query:render'

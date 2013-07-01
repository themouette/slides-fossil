Best practices
==============

### Be ready for next level

---

## Isolate your UI components

<p style="padding: 20px 0;">
    A component's responsability is to provide meaningful user experience.
</p>

* Use **sandboxed context**
* Communicate through **events**

---

## Cover your tracks

* Keep an eye on memory
* Setup only what is needed
* Cleanup when leaving

---

## UI is fragile

### Ensure you have tests!

* Unit: [mocha](http://visionmedia.github.io/mocha/) /
  [jasmine](http://pivotal.github.io/jasmine/) /
  [qunit](http://qunitjs.com/)
* Mocking: [sinonjs](http://sinonjs.org/)
* Fonctional: [CasperJS](http://casperjs.org/)

---

## Industrialize your process

* Task manager: [Grunt](http://gruntjs.com)
* Frontend dependency management: [bower](http://bower.io)
* Command line dependency management: [npm](http://npmjs.org)


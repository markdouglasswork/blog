# Comparing 'Moment' objects properly in Jasmine

So, have you ever tried to write an automated test involving Moment comparison in Jasmine?
If so, you've probably seen error messages that look like this:
```
Expected { _isAMomentObject : true, _i : '2015-11-01 00:00:00', _f : 'YYYY-MM-DD HH:mm:ss', _l : undefined, _strict : undefined, _isUTC : false, _pf : { empty : false, unusedTokens : [ ], unusedInput : [ ], overflow : -1, charsLeftOver : 0, nullInput : false, invalidMonth : null, invalidFormat : false, userInvalidated : false, iso : true }, _a : [ 2015, 10, 1, 0, 0, 0, 0 ], _d : Date(Sun Nov 01 2015 00:00:00 GMT-0600 (Mountain Daylight Time)) } to equal { _isAMomentObject : true, _i : '2015-11-01T00:00:00', _f : 'YYYY-MM-DDTHH:mm:ss', _l : undefined, _strict : undefined, _isUTC : false, _pf : { empty : false, unusedTokens : [ ], unusedInput : [ ], overflow : -1, charsLeftOver : 0, nullInput : false, invalidMonth : null, invalidFormat : false, userInvalidated : false, iso : true }, _a : [ 2015, 10, 1, 0, 0, 0, 0 ], _d : Date(Sun Nov 01 2015 00:00:00 GMT-0600 (Mountain Daylight Time)) }.
```

Yikes, it's pretty difficult to read that, but it clearly thinks that the objects being compared are different.
However, let's take a closer look at the message. The first moment object under comparison represents this moment in time:
```
Date(Sun Nov 01 2015 00:00:00 GMT-0600 (Mountain Daylight Time))
```
The scond moment represents this moment in time:
```
Date(Sun Nov 01 2015 00:00:00 GMT-0600 (Mountain Daylight Time))
```
So why does Jasmine think they're different?
It turns out that this is expected behavior when comparing complex objects,
because Jasmine looks at every single field in the object, and expects them to be identical.

Moment has a built in comparison function that you can use called `isSame()`,
and they are kind enough to provide an example of how to use that function as a [custom comparator](https://jasmine.github.io/tutorials/custom_equality).
This is great if all your tests pertaining to Moment objects reside in a single spec file, but what if they are spread throughout a codebase?
In that case, you'll want to configure Jasmine to always load the custom comparator.

If you are using Jasmine directly, this is fairly straightforward.
[This](https://jasmine.github.io/setup/nodejs.html) writeup covers some information on globally configuring Jasmine.
Specifically, note the `helpers` array in the sample `jasmine.json` file in the link above.
This array allows you to define files that will be read before any specs are executed.
Additionally, a `beforeEach()` or `beforeAll()` function outside of any `describe()` blocks will be executed for all tests in the suite.
Combining these two pieces of information, we can first create a file called `spec-helpers.js`, and paste the following code in it:
```javascript

```

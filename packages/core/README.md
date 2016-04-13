# meteor-messageformat [![Build Status](https://api.travis-ci.org/gadicc/meteor-messageformat.svg?branch=v2)](https://travis-ci.org/gadicc/meteor-messageformat)

MessageFormat i18n support, the Meteor way.

Easy reactive use of complicated strings (gender, plural, etc) with insanely
easy translation into other languages (through a web UI).

For full info, docs and examples, see the
[Meteor MessageFormat home page](http://messageformat.meteor.com/)
(or install/clone the smart package and run `meteor` in its `website` directory).

In short, you'll get to use the `{{mf}}` helper.  Simple example:

```html
<p>{{mf 'trans_string' 'This string is translatable'}}</p>
```

but much more complex strings are possible, and are useful even if your
website is only available in one language, e.g.:

```html
{{#mf KEY='gender_plural' GENDER=getGender NUM_RESULTS=getNum NUM_CATS=getNum2}}
{GENDER, select,
       male {He}
     female {She}
      other {They}
 } found {NUM_RESULTS, plural,
         =0 {no results}
        one {1 result}
      other {# results}
 } in {NUM_CATS, plural,
        one {1 category}
      other {# categories}
 }.
 {{/mf}}
 ```

 Possible outputs:

 ```html
 He found 2 results in 1 category.
 She found 1 result in 2 categories.
 etc
 ```

 Besides gender, there is support for offsets too, e.g.:

 ```html
 You and one other person added this to their profile.
 ```

For full info, docs and examples, see the
[Meteor MessageFormat home page](http://messageformat.meteor.com/)
(or install/clone the smart package and run `mrt` in its `website` directory).

## Initial loading

* The initial HTML page is injected with lastUpdate times for all locales,
  and best locale match for user's client based on `accept-language` header.

* During msgfmt:core loading (early in the main minified script), we use
  any previously saved locale (in localStorage) or otherwise the headerLocale,
  compare the lastSync time (if cached previously) to what's available now,
  and if there is new data available, we initiate a parallel HTTP request to
  fetch it.

* If unsafe-eval is disallowed, we retrieve all the scripts precompiled from
  the server.

## Offline Support

TODO, manifest, buildcompiler, cordova

# react-intl-loader

Async [react-intl](https://github.com/yahoo/react-intl) locale data loader for
[webpack](https://github.com/webpack/webpack).

## Motivation

Instead of needing a [long utility function](https://github.com/gpbl/isomorphic500/blob/a310365a1d4f4fc53e2c9cf11e050bc59ef935b4/src/utils/IntlUtils.js)
with a `require.ensure` for every locale, you can write something like this:

```javascript
// ES6 syntax

const locales = {
  en: () => require('react-intl?locale=en!./en.json'),
  de: () => require('react-intl?locale=de!./de.json')
}

function loadLocaleData (locale) {
  return new Promise((resolve) => {
    locales[locale]()(resolve)
  })
}

loadLocaleData(someLocale).then((messages) => {
  // do something with messages
})
```

## Installation

```console
$ npm install --save intl intl-locales-supported react-intl
$ npm install --save-dev react-intl-loader
```

## Usage

[Documentation: Using loaders](http://webpack.github.io/docs/using-loaders.html)

To asynchronously load your locale data from `./en.json` with the locale `en`, use:

```javascript
require('react-intl?locale=en!./en.json')(function (messages) {
  // messages contains the require of ./en.json
});
```

This will asynchronously require (via webpack's `require.ensure`) the following modules:

```javascript
'intl/locale-data/jsonp/en' // Optional: only if Intl does not support this locale
'react-intl/locale-data/en'
'./en.json'
```

You can use any file and file type for your locale data as long as you have
the appropriate webpack loader installed and configured.

## What?
Reloads all unpacked extensions whenever a file is changed in an extension that is currently under development.
You'll never need to go to `chrome://extensions` and smash reload again.

## How
Extension tries to connect to socket.io server on `http://localhost:8890` (yes, that port is random) and waits for `file.change` events to flow in.
When an event is incoming, the extension reloads `chrome://extensions` automatically, which causes all unpacked extensions to reload and update (e.g. content scripts).
If there is no open tab, currently opened at `chrome://extensions`, the extension creates and reloads one.

An example on how to send file change events to the extension can be found here:
[robin-drexler/chrome-extension-auto-reload-watcher](https://github.com/robin-drexler/chrome-extension-auto-reload-watcher)

## Installation

Download [from the webstore](https://chrome.google.com/webstore/detail/chrome-unpacked-extension/fddfkmklefkhanofhlohnkemejcbamln) or:

 - Clone the repo
 - load `app` folder as unpacked extension in Chrome
 - start developing an unpacked extension
  - don't forget to emit events when a file changes 

## Why...

...reloading the entire tab instead of just using the extensions management api too reload/re-enable extensions?
Currently disabling and enabling extensions again causes any open inspection window (console log etc.) to close, which I found to be too annoying.


## Development

```
npm install
```

`app/js` is created from `src/js` by:

```
browserify src/js/background.js -o app/js/background.js
```

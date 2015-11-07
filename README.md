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

Install [from the webstore](https://chrome.google.com/webstore/detail/chrome-unpacked-extension/fddfkmklefkhanofhlohnkemejcbamln) or:

 - Clone the repo
 - load `app` folder as unpacked extension in Chrome
 - start developing an unpacked extension
  - don't forget to [emit events when a file changes](https://github.com/robin-drexler/chrome-extension-auto-reload-watcher)

## Why...

...reloading the entire tab instead of just using the extensions management api too reload/re-enable extensions?
Currently disabling and enabling extensions again causes any open inspection window (console log etc.) to close, which I found to be too annoying.


## Development

To hack this code, make sure you have [NodeJS](http://nodejs.org) installed, then navigate to the root of this project in your command line interface and run the following to install all dependencies:
```
npm install
```

Generate a `build/` folder which can be loaded into Chrome as an unpacked extension:
```
npm run build
```

Automatically rebuild modified files into `build/` when they're saved:
```
npm run watch
```

Generate `dist/chrome-extension.zip`, which can be uploaded to the Chrom web store:
```
npm run dist
```

## Contributors

This extension was originally developed by [robin-drexler](https://github.com/robin-drexler/chrome-extension-auto-reload).

Updates by [JeromeDane](https://github.com/JeromeDane/chrome-extension-auto-reload) to fix broken reload method using [arikw's method](https://github.com/arikw/chrome-extensions-reloader/blob/master/background.js#L1). Added gulp build process and removed [socket.io-client](https://www.npmjs.com/package/socket.io-client) code from repo so it could be loaded as a dependency instead.

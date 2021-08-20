# Bleno (Node.js Bluetooth LE) for MacOS

The mac bindings in the [`bleno`](https://github.com/sandeepmistry/bleno) repository use a XPC connection and an undocumented protocol to communicate directly with the bluetooth daemon.
This is error prone, as the protocol needs to be reverse engineered by sniffing the communication between a regular program which uses the official CoreBluetooth API and the
bluetooth daemon. Since the protocol is not public Apple can change it at anytime (For now every new OSX release changed the protocol)._

This package provides the same functionality as the regular bleno mac bindings using the official [CoreBluetooth API](https://developer.apple.com/documentation/corebluetooth).

This project uses `@abandonware/bleno` fork of `bleno`. It uses `xpc-connect`, instead of the
abandoned `xpc-connection` npm package.

## System Requirements

* Node.js v6.14.2 or later.
* macOS 10.7 or later

## Prerequisites

### macOS

* install [pyenv](https://github.com/pyenv/pyenv)
* install [nvm](https://nvm.sh)
* install [Xcode](https://itunes.apple.com/ca/app/xcode/id497799835?mt=12)

## Usage

Simply require `bleno-mac` instead of `bleno`:

```javascript
const bleno = require('bleno-mac');
```

On non-Mac platforms this will use the regular [bleno](https://github.com/noble/bleno/blob/master/README.md) implementation and on MacOS it will use the native binding using the official CoreBluetooth API.

## Note

Be careful to not write to the `Client Characteristic Configuration` descriptor directly to enable notification.
Use `subscribe` instead to enable and listen to notifications.

## Implementation Status

Everything should work that also works with the regular bleno mac bindings.

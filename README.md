## LNRPC [![Build Status](https://travis-ci.org/Matt-Jensen/lnrpc.svg?branch=master)](https://travis-ci.org/Matt-Jensen/lnrpc)

Synced to [LND master branch](https://github.com/lightningnetwork/lnd/blob/master/version.go)

### Features
- 🛠Auto-generates [lnd/lnrpc](https://github.com/lightningnetwork/lnd/tree/master/lnrpc) client
- ✨Wraps requests in promises
- 🤝Easily setup SSL and Macaroons
- 📚Instantiates all gRPC services

### Installation

```sh
yarn add lnrpc

# Or
npm i lnrpc -S
```

For best results, be sure to [install lnd](https://github.com/lightningnetwork/lnd/blob/master/docs/INSTALL.md) before using this project and ensure you have an lnd instance running with `--no-macaroons`, unless you provide macaroon authentication to your lnrpc instance.

### Usage

Connecting to an lnd instance at `localhost:10001`.

```javascript
const createLnrpc = require('lnrpc');

(async function() {
  const lnrpc = await createLnrpc();

  // All requests are promisified
  const balance = await lnrpc.walletBalance({});

  // ...and you're off!
  console.log(balance);
})();
```

### Options

```javascript
const createLnrpc = require('lnrpc');

(async function() {
  const lnrcpCustom = await createLnrpc({
    /*
     By default lnrpc connects to `localhost:10001`,
     however we can point to any host.
     */
    server: '173.239.209.2:3001',

    /*
     By default  lnrpc looks for your tls certificate at:
     `~/.lnd/tls.cert`, unless it detects you're using macOS and
     defaults to `~/Library/Application\ Support/Lnd/tls.cert`
     however you can configure your own SSL certificate path like:
     */
    tls: './path/to/tls.cert',

    /*
     You can also provide a TLS certificate directly as a string
     (Just make sure you don't commit this to git).
     Overwrites: `tls`
     */
    cert: process.env.MY_SSL_CERT,

    /*
     Optional path to configure macaroon authentication
     from LND generated macaroon file.
     */
    macaroonPath: './path/to/data/admin.macaroon',

    /*
     Optional way to configure macaroon authentication by
     passing a hex encoded string of your macaroon file
     */
    macaroon: process.env.MY_MACAROON_HEX,
  });
})();
```

### API Reference

[All lnrpc methods documentation can be found here](http://api.lightning.community).

### Contributors

To develop on the project please run:

```sh
git clone git@github.com:Matt-Jensen/lnrpc.git && cd $_
yarn
npm run start
```

### License

This project is licensed under the MIT License.

# @carnesen/bitcoin-rpc-href [![npm version](https://badge.fury.io/js/%40carnesen%2Fbitcoin-rpc-href.svg)](https://badge.fury.io/js/%40carnesen%2Fbitcoin-rpc-href) [![Build Status](https://travis-ci.com/carnesen/bitcoin-rpc-href.svg?branch=master)](https://travis-ci.com/carnesen/bitcoin-rpc-href)

A Node.js client for bitcoin's remote procedure call (RPC) interface. This package includes runtime JavaScript files suitable for Node.js >=8 as well as the corresponding TypeScript type declarations.

## Usage

```ts
const { readRpcHref } = require('@carnesen/bitcoin-rpc-href');
const { URL } = require('url');

const href = readRpcHref();
// http://__cookie__:aaabbb@127.0.0.1:18443/

const url = new URL(href);
// URL {
//   href: 'http://__cookie__:aaabbb@127.0.0.1:18443/',
//   origin: 'http://127.0.0.1:18443',
//   protocol: 'http:',
//   username: '__cookie__',
//   password: 'aaabbb',
//   host: '127.0.0.1:18443',
//   hostname: '127.0.0.1',
//   port: '18443',
//   pathname: '/',
//   search: '',
//   searchParams: URLSearchParams {},
//   hash: '' }
```
## API

### `readRpcHref(configFilePath?): href`
Reads bitcoin configuration files to determine an "href" connection string for the RPC interface. The logic in this function is meant to reproduce as closely as possible that of the `bitcoin-cli` client that ships with the bitcoin server software. Among other things, if the configuration does not contain an `rpcpassword`, that means that "cookie-based" authentication is enabled. In that case `readRpcHref` reads the username and password from the `rpccookiefile` file written to `datadir` on startup.

#### `configFilePath`
Optional `string`. String path of a bitcoin configuration file. Default value is the platform-dependent location where bitcoin looks for its config file e.g. `~/.bitcoin/bitcoin.conf` on Linux.

#### `href`
A string of the form `http://<username>:<password>@<hostname>:<port>/` as defined by the [WHATWG URL](https://nodejs.org/api/url.html#url_the_whatwg_url_api) standard. The href can be passed to `createBitcoinRpc` to create an RPC client. 

## Related
- [@carnesen/bitcoin-rpc](https://github.com/carnesen/bitcoin-rpc): A Node.js client for bitcoin's remote procedure call (RPC) interface
- [@carnesen/bitcoin-config](https://github.com/carnesen/bitcoin-config): A Node.js library for bitcoin server software configuration
- [@carnesen/bitcoin-service](https://github.com/carnesen/bitcoin-service): A Node.js library for managing the bitcoin service `bitcoind`
- [@carnesen/bitcoin-software](https://github.com/carnesen/bitcoin-software): A Node.js library for installing bitcoin server software

## License

MIT © [Chris Arnesen](https://www.carnesen.com)

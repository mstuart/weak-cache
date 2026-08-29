<div align="center">
  <img src="docs/assets/logo.svg" alt="weakref-store — A WeakRef-based cache that automatically evicts entries when values are garbage collected" width="720">
</div>

<p align="center"><strong>A WeakRef-based cache that automatically evicts entries when values are garbage collected</strong></p>

<p align="center">
  <a href="https://github.com/mstuart/weakref-store/actions/workflows/main.yml"><img src="https://github.com/mstuart/weakref-store/actions/workflows/main.yml/badge.svg" alt="CI"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="https://www.npmjs.com/package/weakref-store"><img src="https://img.shields.io/npm/v/weakref-store?label=npm" alt="npm"></a>
  <a href="https://deepwiki.com/mstuart/weakref-store"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
  <a href="https://socket.dev/npm/package/weakref-store"><img src="https://socket.dev/api/badge/npm/package/weakref-store" alt="Socket"></a>
  <img src="https://img.shields.io/badge/node-%E2%89%A522-339933.svg" alt="Node 22+">
</p>

---
## Install

```sh
npm install weakref-store
```

## Usage

```js
import WeakCache from 'weakref-store';

const cache = new WeakCache({
	onEvict(key) {
		console.log(`${key} was garbage collected`);
	},
});

let value = {data: 'hello'};
cache.set('key', value);

console.log(cache.get('key'));
//=> {data: 'hello'}

console.log(cache.has('key'));
//=> true
```

## API

### new WeakCache(options?)

#### options

Type: `object`

##### onEvict

Type: `(key) => void`

Callback invoked with the key when an entry is evicted by garbage collection.

### .get(key)

Returns the value for the key, or `undefined` if the key does not exist or its value has been garbage collected.

### .set(key, value)

Set a key-value pair. The value must be an object (required for `WeakRef`). Throws `TypeError` for primitives.

### .has(key)

Returns `true` if the key exists and the value is still alive.

### .delete(key)

Removes an entry. Returns `true` if the entry existed.

### .size

The approximate number of entries. May include entries whose values have been collected but not yet finalized.

## Related

- [WeakRef](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakRef) - MDN WeakRef documentation
- [FinalizationRegistry](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/FinalizationRegistry) - MDN FinalizationRegistry documentation

## License

MIT

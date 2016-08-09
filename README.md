## What should you use for offline storage of your Progressive Web App?

Suggestion:

* URL addressable resources: Use the (Service Worker) Cache API
* All other data: IndexedDB (using a Promise wrapper library)

| Type        | Sync | Async               | Web Workers | Window | Service Workers | Gotchas                                                                                                           | Libraries                                                                                                                                                                    |
|-------------|------|---------------------|-------------|--------|-----------------|-------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| IndexedDB   |      | ✔  (event based)    | ✔           | ✔      | ✔               | Mandatory complexity  (schema versioning, transactions)                                                           | [localForage][], [dexie](http://dexie.org/), [idb](https://github.com/jakearchibald/indexeddb-promised), [PouchDB][], [Lovefield][], [ydn-db][] |
| Cache API   |      |  ✔  (promise based) | ✔           | ✔      | ✔               |                                                                                                                   | [sw-toolbox](https://github.com/GoogleChrome/sw-toolbox)                                          
| Cookies     | ✔    |                     |             |        |                 | Size-limited, only strings. [Async API proposed](https://github.com/bsittler/async-cookies-api)                                                       | [js-cookie](https://github.com/js-cookie/js-cookie), [Cookies.js](https://github.com/ScottHamper/Cookies)                                                                    |
| DOM Storage | ✔    |                     |             |        |                 | Size-limited, only strings.                                                        |                                                                                                                                                                              |
| WebSQL      |      | ✔  (callback based) |             |        |                 | Rejected by Edge, Firefox.  Likely to unship in Chrome. Not available in a Web/Service Worker.                    |                                                                                                                                                                              |
| AppCache    |      |                     |             |        |                 | Chrome: Deprecating HTTP support,  Firefox: Intent to Deprecate                                                     |                                                                                                                                                                              |                                                                           |
| FileSystem  | ✔    | ✔  (callback based) | ✔           | ✔      |                 | Sandboxed - not native file access. No interest from other vendors outside Chrome |                                                                                                                                                                              |
| File API    |      |                     |             |        |                 | Directory Upload - MSFT and Moz (?)  shipping webkit-prefixed API                                                 |                                                                                                                                                                              |

[localForage]: https://mozilla.github.io/localForage/
[PouchDB]: https://pouchdb.com/
[Lovefield]: https://github.com/google/lovefield
[ydn-db]: https://github.com/yathit/ydn-db

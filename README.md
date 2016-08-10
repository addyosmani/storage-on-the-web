## What should you use for offline storage of your Progressive Web App?

Suggestion:

* URL addressable resources: Use the (Service Worker) Cache API
* All other data: IndexedDB (using a Promise wrapper library)

| Type        | Sync | Async               | Web Workers | Window | Service Workers | Gotchas                                                                                                           | Libraries                                                                                                                                                                    |
|-------------|------|---------------------|-------------|--------|-----------------|-------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [IndexedDB][]   |      | ✔  (event based)    | ✔           | ✔      | ✔               | Mandatory complexity  (schema versioning, transactions). [Observers proposed](https://github.com/WICG/indexed-db-observers)                                                           | [localForage][] or [idb](https://github.com/jakearchibald/indexeddb-promised) (simple key-value data, promises), [Dexie](http://dexie.org/) (complex queries, secondary indices), [PouchDB][] (sync), [Lovefield][] (relational), [ydn-db][] (dexie-like, works with WebSQL) |
| [Cache API][]   |      |  ✔  (promise based) | ✔           | ✔      | ✔               |                                                                                                                   | [sw-toolbox](https://github.com/GoogleChrome/sw-toolbox)                                          
| Cookies     | ✔    |                     |             |        |                 | Size-limited, only strings. [Async API proposed](https://github.com/bsittler/async-cookies-api)                                                       | [js-cookie](https://github.com/js-cookie/js-cookie), [Cookies.js](https://github.com/ScottHamper/Cookies)                                                                    |
| DOM Storage | ✔    |                     |             |        |                 | Size-limited, only strings.                                                        |                                                                                                                                                                              |
| File API    |      |                     |             |        |                 | Directory Upload - MSFT and Moz (?)  shipping webkit-prefixed API                                                 |   [FileAPI library][]. For file-saving see [FileSaver.js][] and the [writable-files][] proposals                                                                                                                                                                           | 
| WebSQL      |      | ✔  (callback based) |             |        |                 | Rejected by Edge, Firefox.  Likely to unship in Chrome. Not available in a Web/Service Worker.                    |                                                                                                                                                                              |
| [AppCache][]    |      |                     |             |        |                 | Chrome: [Deprecating HTTP support](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/UKF8cK0EwMI/discussion),  Firefox: [Intent to Deprecate](https://www.fxsitecompat.com/en-CA/docs/2016/application-cache-support-will-be-removed/)                                                     |                                                                                                                                                                              |                                                                           |
| [FileSystem][]  | ✔    | ✔  (callback based) | ✔           | ✔      |                 | Sandboxed - not native file access. No interest from other vendors outside Chrome |                                                                                                                                                                              |

[IndexedDB]: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
[Cache API]: https://developer.mozilla.org/en-US/docs/Web/API/Cache
[FileSystem]: https://developer.mozilla.org/en-US/docs/Web/API/FileSystem
[AppCache]: https://developer.mozilla.org/en-US/docs/Web/HTML/Using_the_application_cache
[localForage]: https://mozilla.github.io/localForage/
[PouchDB]: https://pouchdb.com/
[Lovefield]: https://github.com/google/lovefield
[ydn-db]: https://github.com/yathit/ydn-db
[FileAPI library]: https://github.com/mailru/FileAPI
[FileSaver.js]: https://github.com/eligrey/FileSaver.js
[writable-files]: https://github.com/WICG/writable-files

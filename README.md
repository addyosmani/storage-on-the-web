## What should you use for offline storage of your Progressive Web App?

Recommentations:

* **URL addressable resources: Use the (Service Worker) Cache API**
* **All other data: IndexedDB (using a Promise wrapper library)**

| Type        | Sync | Async               | Web Workers | Window | Service Workers | Gotchas                                                                                                           | Libraries                                                                                                                                                                    |
|-------------|------|---------------------|-------------|--------|-----------------|-------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [IndexedDB][]   |      | ✔  (event based)    | ✔           | ✔      | ✔               | Mandatory complexity  (schema versioning, transactions). [Observers proposed][]                                                           | [localForage][] (promises, legacy browser support), [idb-keyval][] (<500K, promises, if only need key-value), [idb][] (promises, also does iteration, indexing), [Dexie][] (complex queries, secondary indices), [PouchDB][] (sync), [Lovefield][] (relational), [ydn-db][] (dexie-like, works with WebSQL) |
| [Cache API][]   |      |  ✔  (promise based) | ✔           | ✔      | ✔               |                                                                                                                   | [sw-toolbox][]                                          
| Cookies     | ✔    |                     |             |        |                 | Size-limited, only strings. [Async Cookies API proposed][]                                                       | [js-cookie][], [Cookies.js][]                                                                    |
| [Web Storage][] | ✔    |                     |             |        |                 | Size-limited, only strings.                                                        | [store.js][], [lawnchair][]                                                                                                                                                                            |
| [File API][]   |✔ (callback based)      |✔                   |✔             |✔        |                 | Superseded by the [File and Directory Entries API][]                                                 |   [FileAPI library][]. For file-saving see [FileSaver.js][] and the [writable-files][] proposals                                                                                                                                                                           | 
| [WebSQL][]      |      | ✔  (callback based) |             |        |                 | Rejected by Edge, Firefox.  Likely to unship in Chrome. Not available in a Web/Service Worker.                    |                                                                                                                                                                              |
| [AppCache][]    |✔      |                     |             |        |                 | [Chrome: Deprecating HTTP support][],  [Firefox: Intent to Deprecate][]                                                     |                                                                                                                                                                              |                                                                           |
| [FileSystem][]  | ✔    | ✔  (callback based) | ✔           | ✔      |                 | Sandboxed - not native file access. No interest from other vendors outside Chrome |                                                                                                                                                                              |

## Current and future work

* [Durable Storage][]: protect storage from the user agent’s clearing policies 
* [Indexed Database API 2.0][]: advanced key-value data management
* [Quota Management API][]: check how much quota an app/origin is using
* [Directory downloads][]: allow sites to download directories without .zip files
* [File and Directory Entries API][]: support for file and directory upload by drag-and-drop

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
[File API]: https://developer.mozilla.org/en-US/docs/Web/API/File
[Web Storage]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API
[WebSQL]: https://www.w3.org/TR/webdatabase/
[store.js]: https://github.com/marcuswestin/store.js
[lawnchair]: https://github.com/brianleroux/lawnchair
[File and Directory Entries API]: https://wicg.github.io/entries-api/
[idb-keyval]: https://www.npmjs.com/package/idb-keyval
[Observers proposed]: https://github.com/WICG/indexed-db-observers
[idb]: https://www.npmjs.com/package/idb
[Chrome: Deprecating HTTP support]: https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/UKF8cK0EwMI/discussion
[Firefox: Intent to Deprecate]: https://www.fxsitecompat.com/en-CA/docs/2016/application-cache-support-will-be-removed/
[Cookies.js]: https://github.com/ScottHamper/Cookies
[js-cookie]: https://github.com/js-cookie/js-cookie
[Async Cookies API proposed]: https://github.com/bsittler/async-cookies-api
[sw-toolbox]: https://github.com/GoogleChrome/sw-toolbox
[Dexie]: http://dexie.org/
[Durable Storage]: https://storage.spec.whatwg.org/
[Directory downloads]: https://github.com/drufball/directory-download
[Quota Management API]: https://www.w3.org/TR/quota-api/
[Indexed Database API 2.0]: https://w3c.github.io/IndexedDB/

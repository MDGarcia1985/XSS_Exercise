{
  "log": {
    "version": "1.2",
    "creator": {
      "name": "WebInspector",
      "version": "537.36"
    },
    "pages": [
      {
        "startedDateTime": "2026-10-19T17:34:28.534Z",
        "id": "page_1",
        "title": "https://xss-game.appspot.com/level4",
        "pageTimings": {
          "onContentLoad": 304.2520000017248,
          "onLoad": 601.0470000328496
        }
      },
      {
        "startedDateTime": "2026-10-19T18:01:06.875Z",
        "id": "page_2",
        "title": "https://xss-game.appspot.com/level5",
        "pageTimings": {
          "onContentLoad": 281.0719999833964,
          "onLoad": 555.3000000072643
        }
      },
      {
        "startedDateTime": "2026-10-19T18:07:49.794Z",
        "id": "page_4",
        "title": "https://xss-game.appspot.com/level5",
        "pageTimings": {
          "onContentLoad": 161.10000002663583,
          "onLoad": 402.98399998573586
        }
      }
    ],
    "entries": [
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "toggleCode",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 78,
                "columnNumber": 4
              },
              {
                "functionName": "onclick",
                "scriptId": "112",
                "url": "https://xss-game.appspot.com/level3",
                "lineNumber": 59,
                "columnNumber": 68
              }
            ]
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level3/code/1",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level3/code/1"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level3"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 14:36:27 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "828f7b4f0e2e25d78045e56ddb8c6784"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 101,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.251.211.20",
        "startedDateTime": "2026-10-19T14:36:27.390Z",
        "time": 72.07699998980388,
        "timings": {
          "blocked": 2.5479999770484865,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.22799999999999998,
          "wait": 68.62000000776723,
          "receive": 0.6810000049881637,
          "_blocked_queueing": 1.9309999770484865,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "13117"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "onclick",
                "scriptId": "145",
                "url": "https://xss-game.appspot.com/level3/source",
                "lineNumber": 21,
                "columnNumber": 43
              }
            ]
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level3/file/level.py",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level3/file/level.py"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level3/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 14:39:10 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "f5895ed3995db76b28cca98f0ac726d4"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 99,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.251.211.20",
        "startedDateTime": "2026-10-19T14:39:09.949Z",
        "time": 61.44899997161701,
        "timings": {
          "blocked": 2.403999988038093,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.23299999999999998,
          "wait": 58.09999997537211,
          "receive": 0.7120000082068145,
          "_blocked_queueing": 1.8559999880380929,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "13117"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "onclick",
                "scriptId": "146",
                "url": "https://xss-game.appspot.com/level3/source",
                "lineNumber": 20,
                "columnNumber": 45
              }
            ]
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level3/file/index.html",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level3/file/index.html"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level3/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 14:40:04 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "d0fe25055698566a56aaa2050d256f38"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 98,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.251.211.20",
        "startedDateTime": "2026-10-19T14:40:04.690Z",
        "time": 147.97200000612065,
        "timings": {
          "blocked": 33.68400002748519,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.25400000000000134,
          "wait": 113.1980000157617,
          "receive": 0.8359999628737569,
          "_blocked_queueing": 2.037000027485192,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "13117"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "levelSolved",
                "scriptId": "11",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 22,
                "columnNumber": 7
              },
              {
                "functionName": "",
                "scriptId": "874",
                "url": "",
                "lineNumber": 0,
                "columnNumber": 0
              }
            ]
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/level3/record",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/level3/record"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level3"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-length",
              "value": "0"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 17:20:41 GMT"
            },
            {
              "name": "expires",
              "value": "Mon, 19 Oct 2026 17:20:41 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "238dd385240dad81744756c0556391c1"
            }
          ],
          "cookies": [],
          "content": {
            "size": 0,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 265,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.250.177.244",
        "startedDateTime": "2026-10-19T17:20:41.535Z",
        "time": 444.5430000096075,
        "timings": {
          "blocked": 3.324000000089407,
          "dns": 24.402,
          "ssl": 215.217,
          "connect": 260.715,
          "send": 0.36099999999999,
          "wait": 155.02099999860303,
          "receive": 0.7200000109151006,
          "_blocked_queueing": 2.171000000089407,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "73781"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "952",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "952",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "",
                "scriptId": "953",
                "url": "https://xss-game.appspot.com/level4/source",
                "lineNumber": 93,
                "columnNumber": 6
              }
            ],
            "parent": {
              "description": "setTimeout",
              "callFrames": [
                {
                  "functionName": "",
                  "scriptId": "953",
                  "url": "https://xss-game.appspot.com/level4/source",
                  "lineNumber": 92,
                  "columnNumber": 4
                }
              ]
            }
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level4/file/index.html",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level4/file/index.html"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level4/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 17:34:29 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "584ebb3a634a0156255eac98c0ee2508"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 102,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.251.214.212",
        "startedDateTime": "2026-10-19T17:34:29.612Z",
        "time": 73.34299996728078,
        "timings": {
          "blocked": 3.158999962568283,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.23099999999999998,
          "wait": 69.26500000463054,
          "receive": 0.6880000000819564,
          "_blocked_queueing": 2.532999962568283,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "78088",
        "pageref": "page_1"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "952",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "952",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "",
                "scriptId": "953",
                "url": "https://xss-game.appspot.com/level4/source",
                "lineNumber": 97,
                "columnNumber": 6
              }
            ],
            "parent": {
              "description": "setTimeout",
              "callFrames": [
                {
                  "functionName": "",
                  "scriptId": "953",
                  "url": "https://xss-game.appspot.com/level4/source",
                  "lineNumber": 96,
                  "columnNumber": 4
                }
              ]
            }
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level4/file/index.html",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level4/file/index.html"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level4/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 17:34:30 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "ea2f97150bde90c5255eac98c0ee2b53"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 98,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.251.214.212",
        "startedDateTime": "2026-10-19T17:34:30.123Z",
        "time": 69.70699998782948,
        "timings": {
          "blocked": 2.4999999805800615,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.21899999999999997,
          "wait": 66.35199999566748,
          "receive": 0.6360000115819275,
          "_blocked_queueing": 1.7479999805800617,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "78088",
        "pageref": "page_1"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "levelSolved",
                "scriptId": "910",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 22,
                "columnNumber": 7
              },
              {
                "functionName": "",
                "scriptId": "1068",
                "url": "",
                "lineNumber": 0,
                "columnNumber": 0
              }
            ]
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/level4/record",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/level4/record"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level4"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-length",
              "value": "0"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 17:36:41 GMT"
            },
            {
              "name": "expires",
              "value": "Mon, 19 Oct 2026 17:36:41 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "520cbb1ce1baf9db778e4a591265e366"
            }
          ],
          "cookies": [],
          "content": {
            "size": 0,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 166,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.251.214.212",
        "startedDateTime": "2026-10-19T17:36:41.265Z",
        "time": 61.68100005015731,
        "timings": {
          "blocked": 2.7540000126101076,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.254,
          "wait": 57.9530000266321,
          "receive": 0.7200000109151006,
          "_blocked_queueing": 2.1650000126101077,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "78088",
        "pageref": "page_1"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "1132",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "1132",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "",
                "scriptId": "1133",
                "url": "https://xss-game.appspot.com/level5/source",
                "lineNumber": 102,
                "columnNumber": 6
              }
            ],
            "parent": {
              "description": "setTimeout",
              "callFrames": [
                {
                  "functionName": "",
                  "scriptId": "1133",
                  "url": "https://xss-game.appspot.com/level5/source",
                  "lineNumber": 101,
                  "columnNumber": 4
                }
              ]
            }
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level5/file/level.py",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level5/file/level.py"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level5/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 18:01:07 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "23875c44746307d483a62607863f64be"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 103,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.250.189.148",
        "startedDateTime": "2026-10-19T18:01:07.908Z",
        "time": 69.99799999175593,
        "timings": {
          "blocked": 2.263999993767589,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.18600000000000005,
          "wait": 66.83300002514571,
          "receive": 0.7149999728426337,
          "_blocked_queueing": 1.6579999937675893,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "86607",
        "pageref": "page_2"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "1132",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "1132",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "",
                "scriptId": "1133",
                "url": "https://xss-game.appspot.com/level5/source",
                "lineNumber": 106,
                "columnNumber": 6
              }
            ],
            "parent": {
              "description": "setTimeout",
              "callFrames": [
                {
                  "functionName": "",
                  "scriptId": "1133",
                  "url": "https://xss-game.appspot.com/level5/source",
                  "lineNumber": 105,
                  "columnNumber": 4
                }
              ]
            }
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level5/file/level.py",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level5/file/level.py"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level5/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 18:01:08 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "10f33a35193eeb7f83a62607863f6790"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 99,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.250.189.148",
        "startedDateTime": "2026-10-19T18:01:08.406Z",
        "time": 66.75100000575185,
        "timings": {
          "blocked": 2.7530000113919377,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.238,
          "wait": 63.01799999054894,
          "receive": 0.742000003810972,
          "_blocked_queueing": 1.8820000113919377,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "86607",
        "pageref": "page_2"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "1218",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "1218",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "",
                "scriptId": "1219",
                "url": "https://xss-game.appspot.com/level5/source",
                "lineNumber": 102,
                "columnNumber": 6
              }
            ],
            "parent": {
              "description": "setTimeout",
              "callFrames": [
                {
                  "functionName": "",
                  "scriptId": "1219",
                  "url": "https://xss-game.appspot.com/level5/source",
                  "lineNumber": 101,
                  "columnNumber": 4
                }
              ]
            }
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level5/file/level.py",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level5/file/level.py"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level5/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 18:07:50 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "d039f3703f8889aae444a10b249d5abe"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 217,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.250.177.84",
        "startedDateTime": "2026-10-19T18:07:50.664Z",
        "time": 228.53300002344326,
        "timings": {
          "blocked": 2.5150000294856727,
          "dns": 38.836000000000006,
          "ssl": 49.818999999999996,
          "connect": 112.356,
          "send": 0.37000000000000455,
          "wait": 73.7829999916777,
          "receive": 0.6730000022798777,
          "_blocked_queueing": 1.7850000294856727,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "88905",
        "pageref": "page_4"
      },
      {
        "_initiator": {
          "type": "script",
          "stack": {
            "callFrames": [
              {
                "functionName": "logXHR",
                "scriptId": "1218",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 91,
                "columnNumber": 7
              },
              {
                "functionName": "selectFile",
                "scriptId": "1218",
                "url": "https://xss-game.appspot.com/static/game.js",
                "lineNumber": 143,
                "columnNumber": 2
              },
              {
                "functionName": "",
                "scriptId": "1219",
                "url": "https://xss-game.appspot.com/level5/source",
                "lineNumber": 106,
                "columnNumber": 6
              }
            ],
            "parent": {
              "description": "setTimeout",
              "callFrames": [
                {
                  "functionName": "",
                  "scriptId": "1219",
                  "url": "https://xss-game.appspot.com/level5/source",
                  "lineNumber": 105,
                  "columnNumber": 4
                }
              ]
            }
          }
        },
        "_priority": "High",
        "_resourceType": "xhr",
        "cache": {},
        "connection": "443",
        "request": {
          "method": "GET",
          "url": "https://xss-game.appspot.com/feedback/level5/file/level.py",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": ":authority",
              "value": "xss-game.appspot.com"
            },
            {
              "name": ":method",
              "value": "GET"
            },
            {
              "name": ":path",
              "value": "/feedback/level5/file/level.py"
            },
            {
              "name": ":scheme",
              "value": "https"
            },
            {
              "name": "accept",
              "value": "*/*"
            },
            {
              "name": "accept-encoding",
              "value": "gzip, deflate, br, zstd"
            },
            {
              "name": "accept-language",
              "value": "en-US,en;q=0.9"
            },
            {
              "name": "dnt",
              "value": "1"
            },
            {
              "name": "priority",
              "value": "u=1, i"
            },
            {
              "name": "referer",
              "value": "https://xss-game.appspot.com/level5/source"
            },
            {
              "name": "sec-ch-ua",
              "value": "\"Brave\";v=\"155\", \"Chromium\";v=\"155\", \"Not(A:Brand\";v=\"24\""
            },
            {
              "name": "sec-ch-ua-mobile",
              "value": "?0"
            },
            {
              "name": "sec-ch-ua-platform",
              "value": "\"Windows\""
            },
            {
              "name": "sec-fetch-dest",
              "value": "empty"
            },
            {
              "name": "sec-fetch-mode",
              "value": "cors"
            },
            {
              "name": "sec-fetch-site",
              "value": "same-origin"
            },
            {
              "name": "user-agent",
              "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/155.0.0.0 Safari/537.36"
            }
          ],
          "queryString": [],
          "cookies": [],
          "headersSize": -1,
          "bodySize": 0
        },
        "response": {
          "status": 200,
          "statusText": "",
          "httpVersion": "http/2.0",
          "headers": [
            {
              "name": "alt-svc",
              "value": "h3=\":443\"; ma=2592000,h3-29=\":443\"; ma=2592000"
            },
            {
              "name": "cache-control",
              "value": "no-cache"
            },
            {
              "name": "content-encoding",
              "value": "gzip"
            },
            {
              "name": "content-length",
              "value": "22"
            },
            {
              "name": "content-type",
              "value": "text/html; charset=utf-8"
            },
            {
              "name": "date",
              "value": "Mon, 19 Oct 2026 18:07:51 GMT"
            },
            {
              "name": "server",
              "value": "Google Frontend"
            },
            {
              "name": "vary",
              "value": "Accept-Encoding"
            },
            {
              "name": "x-cloud-trace-context",
              "value": "d5cf921bc2f7f0f9e444a10b249d5927"
            }
          ],
          "cookies": [],
          "content": {
            "size": 2,
            "mimeType": "text/html"
          },
          "redirectURL": "",
          "headersSize": -1,
          "bodySize": -1,
          "_transferSize": 99,
          "_error": null,
          "_fetchedViaServiceWorker": false
        },
        "serverIPAddress": "142.250.177.84",
        "startedDateTime": "2026-10-19T18:07:51.161Z",
        "time": 81.16399997379631,
        "timings": {
          "blocked": 2.4009999810904263,
          "dns": -1,
          "ssl": -1,
          "connect": -1,
          "send": 0.19899999999999995,
          "wait": 75.87199998358638,
          "receive": 2.6920000091195107,
          "_blocked_queueing": 1.7709999810904264,
          "_workerStart": -1,
          "_workerReady": -1,
          "_workerFetchStart": -1,
          "_workerRespondWithSettled": -1
        },
        "_connectionId": "88905",
        "pageref": "page_4"
      }
    ]
  }
}
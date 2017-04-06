# api documentation for  [express-error-handler (v1.1.0)](https://github.com/dilvie/express-error-handler#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-express-error-handler.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-express-error-handler) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-express-error-handler.svg)](https://travis-ci.org/npmdoc/node-npmdoc-express-error-handler)
#### A graceful error handler for Express applications.

[![NPM](https://nodei.co/npm/express-error-handler.png?downloads=true)](https://www.npmjs.com/package/express-error-handler)

[![apidoc](https://npmdoc.github.io/node-npmdoc-express-error-handler/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-express-error-handler_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-express-error-handler/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-express-error-handler/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-express-error-handler/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Eric Elliott"
    },
    "bugs": {
        "url": "https://github.com/dilvie/express-error-handler/issues"
    },
    "dependencies": {
        "mout": "0.12.0"
    },
    "description": "A graceful error handler for Express applications.",
    "devDependencies": {
        "bunyan-request-logger": "1.0.2",
        "connect-cache-control": "1.0.0",
        "express": "^4.9.8",
        "grunt": "~0.4.1",
        "grunt-contrib-jshint": "1.0.0",
        "restify": "4.0.4",
        "supertest": "1.2.0",
        "tape": "4.5.1",
        "through": "~2.3.4",
        "updtr": "0.1.7",
        "watch": "0.17.1"
    },
    "directories": {},
    "dist": {
        "shasum": "ff2edb1fedcfcab1e601c60aab3554982f1f6497",
        "tarball": "https://registry.npmjs.org/express-error-handler/-/express-error-handler-1.1.0.tgz"
    },
    "gitHead": "610999b2263fcffefe4cb4daa1099fcbf670ca02",
    "homepage": "https://github.com/dilvie/express-error-handler#readme",
    "keywords": [
        "error",
        "errors",
        "handling",
        "handler",
        "express",
        "connect"
    ],
    "license": "MIT",
    "main": "error-handler.js",
    "maintainers": [
        {
            "name": "ericelliott",
            "email": "eric@ericleads.com"
        }
    ],
    "name": "express-error-handler",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/dilvie/express-error-handler.git"
    },
    "scripts": {
        "latest": "updtr",
        "lint": "grunt hint",
        "pretest": "npm run -s lint",
        "start-example": "node examples/app.js | bunyan",
        "test": "node ./test/runtests.js",
        "watch": "watch 'clear && npm run -s test' ."
    },
    "version": "1.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module express-error-handler](#apidoc.module.express-error-handler)
1.  [function <span class="apidocSignatureSpan">express-error-handler.</span>clientError ()](#apidoc.element.express-error-handler.clientError)
1.  [function <span class="apidocSignatureSpan">express-error-handler.</span>httpError (status, message)](#apidoc.element.express-error-handler.httpError)
1.  [function <span class="apidocSignatureSpan">express-error-handler.</span>isClientError (status)](#apidoc.element.express-error-handler.isClientError)



# <a name="apidoc.module.express-error-handler"></a>[module express-error-handler](#apidoc.module.express-error-handler)

#### <a name="apidoc.element.express-error-handler.clientError"></a>[function <span class="apidocSignatureSpan">express-error-handler.</span>clientError ()](#apidoc.element.express-error-handler.clientError)
- description and source-code
```javascript
clientError = function () {
  var args = [].slice.call(arguments);

  console.log('WARNING: .clientError() is ' +
    'deprecated. Use isClientError() instead.');

  return this.isClientError.apply(this, args);
}
```
- example usage
```shell
...
  }
};

createHandler.isClientError = isClientError;
createHandler.clientError = function () {
  var args = [].slice.call(arguments);

  console.log('WARNING: .clientError() is ' +
    'deprecated. Use isClientError() instead.');

  return this.isClientError.apply(this, args);
};

// HTTP error generating route.
createHandler.httpError = httpError;
...
```

#### <a name="apidoc.element.express-error-handler.httpError"></a>[function <span class="apidocSignatureSpan">express-error-handler.</span>httpError (status, message)](#apidoc.element.express-error-handler.httpError)
- description and source-code
```javascript
function httpError(status, message) {
  var err = new Error();
  err.status = status;
  err.message = message ||
    statusCodes[status] ||
    'Internal server error';

  return function httpErr(req, res, next) {
    next(err);
  };
}
```
- example usage
```shell
...
        // do some custom thing here...
      }
    }
  });

// After all your routes...
// Pass a 404 into next(err)
app.use( errorHandler.httpError(404) );

// Handle all unhandled errors:
app.use( handler );
'''

Or for a static page:
...
```

#### <a name="apidoc.element.express-error-handler.isClientError"></a>[function <span class="apidocSignatureSpan">express-error-handler.</span>isClientError (status)](#apidoc.element.express-error-handler.isClientError)
- description and source-code
```javascript
function isClientError(status) {
  return (status >= 400 && status <= 499);
}
```
- example usage
```shell
...
var errorHandler = require('express-error-handler'),
handler = errorHandler({
  serializer: function(err) {
    var body = {
      status: err.status,
      message: err.message
    };
    if (createHandler.isClientError(err.status)) {
      ['code', 'name', 'type', 'details'].forEach(function(prop) {
        if (err[prop]) body[prop] = err[prop];
      });
    }
    return body;
  }
});
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

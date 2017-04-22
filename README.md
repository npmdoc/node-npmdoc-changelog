# npmdoc-changelog

#### api documentation for  [changelog (v1.0.7)](http://github.com/dylang/changelog)  [![npm package](https://img.shields.io/npm/v/npmdoc-changelog.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-changelog) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-changelog.svg)](https://travis-ci.org/npmdoc/node-npmdoc-changelog)

#### Command line tool (and Node module) that generates a changelog in color output, markdown, or json for modules in npmjs.org's registry as well as any public github.com repo.

[![NPM](https://nodei.co/npm/changelog.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/changelog)

- [https://npmdoc.github.io/node-npmdoc-changelog/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-changelog/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-changelog/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-changelog/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-changelog/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-changelog/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Dylan Greene"
    },
    "bin": {
        "changelog": "./bin/changelog.js"
    },
    "bugs": {
        "url": "http://github.com/dylang/changelog/issues"
    },
    "dependencies": {
        "chalk": "^0.5.1",
        "cli": "^0.6.4",
        "has-color": "^0.1.1",
        "lodash": "^2.4.1",
        "moment": "^2.5.0",
        "q": "^1.0.1",
        "request": "^2.34.0",
        "semver": "^4.0.3",
        "wordwrap": "^0.0.2"
    },
    "description": "Command line tool (and Node module) that generates a changelog in color output, markdown, or json for modules in npmjs.org's registry as well as any public github.com repo.",
    "devDependencies": {
        "chai": "^1.9.1",
        "grunt": "^0.4.1",
        "grunt-contrib-jshint": "^0.10.0",
        "grunt-contrib-watch": "^0.6.1",
        "grunt-mocha-test": "^0.12.1",
        "grunt-notify": "^0.3.1",
        "grunt-readme": "^0.4.5",
        "grunt-templates-dylang": "^1.0.0",
        "load-grunt-tasks": "^0.6.0",
        "mocha": "^1.18.2",
        "proxyquire": "^1.0.1",
        "time-grunt": "^1.0.0"
    },
    "directories": {
        "lib": "./lib",
        "bin": "./bin"
    },
    "dist": {
        "shasum": "e95de6dc14082948bd49618304e9c9e854e821e5",
        "tarball": "https://registry.npmjs.org/changelog/-/changelog-1.0.7.tgz"
    },
    "engines": {
        "node": ">= 0.10.0"
    },
    "gitHead": "66b3f4b9fc99c1a812e1009ed1e1e1e14c153342",
    "homepage": "http://github.com/dylang/changelog",
    "keywords": [
        "changelog",
        "change log",
        "commit messages",
        "commits",
        "changes",
        "history",
        "what's new",
        "change set"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "http://github.com/dylang/changelog/raw/master/LICENSE"
        }
    ],
    "main": "lib/changelog",
    "maintainers": [
        {
            "name": "dylang"
        }
    ],
    "name": "changelog",
    "optionalDependencies": {},
    "preferGlobal": true,
    "repository": {
        "type": "git",
        "url": "git+https://github.com/dylang/changelog.git"
    },
    "scripts": {
        "test": "grunt test"
    },
    "version": "1.0.7"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

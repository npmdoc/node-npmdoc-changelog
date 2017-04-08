# api documentation for  [changelog (v1.0.7)](http://github.com/dylang/changelog)  [![npm package](https://img.shields.io/npm/v/npmdoc-changelog.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-changelog) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-changelog.svg)](https://travis-ci.org/npmdoc/node-npmdoc-changelog)
#### Command line tool (and Node module) that generates a changelog in color output, markdown, or json for modules in npmjs.org's registry as well as any public github.com repo.

[![NPM](https://nodei.co/npm/changelog.png?downloads=true)](https://www.npmjs.com/package/changelog)

[![apidoc](https://npmdoc.github.io/node-npmdoc-changelog/build/screenCapture.buildNpmdoc.browser.%252Fhome%252Ftravis%252Fbuild%252Fnpmdoc%252Fnode-npmdoc-changelog%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-changelog/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-changelog/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-changelog/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Dylan Greene",
        "email": "dylang@gmail.com"
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
            "name": "dylang",
            "email": "dylang@gmail.com"
        }
    ],
    "name": "changelog",
    "optionalDependencies": {},
    "preferGlobal": true,
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module changelog](#apidoc.module.changelog)
1.  [function <span class="apidocSignatureSpan">changelog.</span>generate (project, versionRequested)](#apidoc.element.changelog.generate)
1.  [function <span class="apidocSignatureSpan">changelog.</span>markdown (data)](#apidoc.element.changelog.markdown)
1.  [function <span class="apidocSignatureSpan">changelog.</span>terminal (data)](#apidoc.element.changelog.terminal)



# <a name="apidoc.module.changelog"></a>[module changelog](#apidoc.module.changelog)

#### <a name="apidoc.element.changelog.generate"></a>[function <span class="apidocSignatureSpan">changelog.</span>generate (project, versionRequested)](#apidoc.element.changelog.generate)
- description and source-code
```javascript
function generate(project, versionRequested) {

if (!project) {
    return new Error('Need help? --help or more help at https://github.com/dylang/changelog');
}

if (project.match(/github.com/)) {
    var repo = project.match(/github\.com\/([^\/]*\/[^\/]*)/);
    if (repo && repo[1]) {
        repo = repo[1].replace(/\.git$/, '');
        log.debug('using github repo ' + repo);
        return github.changelog(repo, versionRequested);
    }

    return new Error('Bad repo url: ' + project);
}

if (project.split('/').length === 2) {
    log.debug('using github repo ' + project);
    return github.changelog(project, versionRequested);
}

log.debug('using npm module ' + project);
return npm.packageHistory(project)
    .then(github.commitMessages)
    .then(function(data) {
        return processNpmAndGithubData(data, versionRequested);
    });
}
```
- example usage
```shell
...



### Changelog API

Changelog can be easily integrated into other tools.

#### 'changelog.generate(name, versions)

* 'name' string, _required_ NPM module name from registry.
* 'versions' integer or semver, _optional_ Number of versions, or the semver version to show.


''''js
var changelog = require('changelog');
...
```

#### <a name="apidoc.element.changelog.markdown"></a>[function <span class="apidocSignatureSpan">changelog.</span>markdown (data)](#apidoc.element.changelog.markdown)
- description and source-code
```javascript
function markdown(data) {
    var output = [];

    data.versions.map(function(version, i){
        if (version.changes) {
            var date = version.date;
            var versionString = (version.version ? version.version + ' / ' : '') +
                    moment(date).format("YYYY-MM-DD");

            // add a blank line between sections
            if (i > 0) {
                output.push('');
            }

            output.push(versionString);
            output.push(new Array(versionString.length + 1).join('='));
            output.push('');

            var uniqueChanges = {};
            version.changes.forEach(function(change){
                if (!uniqueChanges[change.message]) {
                    var message = change.message;
                    if (data.project && data.project.github) {
                        message = message.replace(/#([0-9]+)/g, '[#$1](https://github.com/' + data.project.github + '/issues/$1' + ')');
                    }
                    output.push(bullet(message, '*', true));
                }
                uniqueChanges[change.message] = true;
            });
        }
    });

    return output.join('\n');
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.changelog.terminal"></a>[function <span class="apidocSignatureSpan">changelog.</span>terminal (data)](#apidoc.element.changelog.terminal)
- description and source-code
```javascript
function terminal(data) {

    var output = [];

    data.versions.map(function(version, i){


        var date = version.date;
        var versionString = (version.version ? version.version + ' / ' : '') +
                moment(date).format("YYYY-MM-DD");

        // add a blank line between sections
        if (i > 0) {
            output.push('');
        }

        output.push(chalk.yellow(versionString));


        if (!version.changes) {
            return output.push(bullet('Changelog not found.'));
        }


        var uniqueChanges = {};
        version.changes.forEach(function(change){
            if (!uniqueChanges[change.message]) {
                var message = change.message
                    .replace(/([^']*)'([^']*)'([^']*)/g, '$1' + chalk.green('$2') + '$3')
                    .replace(/#([0-9]+)/g, chalk.blue.underline('https://github.com/' + data.project.github + '/issues/$1'))
                    .replace(/^(\[[^\]]*\])/, chalk.cyan('$1'));
                output.push(bullet(message));
            }
            uniqueChanges[change.message] = true;
        });
    });

    return output.join('\n');
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

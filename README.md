# api documentation for  shelljs-nodecli (v0.1.1)  [![npm package](https://img.shields.io/npm/v/npmdoc-shelljs-nodecli.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-shelljs-nodecli) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-shelljs-nodecli.svg)](https://travis-ci.org/npmdoc/node-npmdoc-shelljs-nodecli)
#### ShellJS Node CLI Extension

[![NPM](https://nodei.co/npm/shelljs-nodecli.png?downloads=true)](https://www.npmjs.com/package/shelljs-nodecli)

[![apidoc](https://npmdoc.github.io/node-npmdoc-shelljs-nodecli/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-shelljs-nodecli_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-shelljs-nodecli/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-shelljs-nodecli/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-shelljs-nodecli/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Nicholas C. Zakas"
    },
    "dependencies": {
        "shelljs": "~0.2"
    },
    "description": "ShellJS Node CLI Extension",
    "devDependencies": {
        "chai": "~1.9.0",
        "eslint": "~0.4",
        "istanbul": "~0.1.45",
        "mocha": "~1.13.0",
        "rewire": "~2.0.0",
        "sinon": "~1.9.0"
    },
    "directories": {},
    "dist": {
        "shasum": "f1beb5563754c475d06f7d0833e0f6075e462d3b",
        "tarball": "https://registry.npmjs.org/shelljs-nodecli/-/shelljs-nodecli-0.1.1.tgz"
    },
    "license": "MIT",
    "main": "./lib/shelljs-nodecli.js",
    "maintainers": [
        {
            "name": "nzakas",
            "email": "nicholas@nczconsulting.com"
        }
    ],
    "name": "shelljs-nodecli",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "scripts": {
        "lint": "node Makefile.js lint",
        "major": "node Makefile.js major",
        "minor": "node Makefile.js minor",
        "patch": "node Makefile.js patch",
        "test": "node Makefile.js"
    },
    "version": "0.1.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module shelljs-nodecli](#apidoc.module.shelljs-nodecli)
1.  [function <span class="apidocSignatureSpan">shelljs-nodecli.</span>exec (name)](#apidoc.element.shelljs-nodecli.exec)
1.  [function <span class="apidocSignatureSpan">shelljs-nodecli.</span>getPath (name, root)](#apidoc.element.shelljs-nodecli.getPath)



# <a name="apidoc.module.shelljs-nodecli"></a>[module shelljs-nodecli](#apidoc.module.shelljs-nodecli)

#### <a name="apidoc.element.shelljs-nodecli.exec"></a>[function <span class="apidocSignatureSpan">shelljs-nodecli.</span>exec (name)](#apidoc.element.shelljs-nodecli.exec)
- description and source-code
```javascript
exec = function (name) {
    var cliPath = this.getPath(name),
        cmd = [cliPath],
        args = [],
        i = 1,
        len = arguments.length;

    if (cliPath) {
        while (i < len && (typeof arguments[i] === "string")) {
            cmd.push(arguments[i]);
            i++;
        }

        args.push(cmd.join(" "));

        while (i < len) {
            args.push(arguments[i]);
            i++;
        }

        return exec.apply(null, args);
    } else {
        throw new Error("Couldn't find " + name + ".");
    }

}
```
- example usage
```shell
...
## The Solution

Since Node binaries are specified in their 'package.json' files, it's actually pretty easy to look up the location of the runtime
 file and get the path. That's where the ShellJS Node CLI extension comes in:

'''js
var nodeCLI = require("shelljs-nodecli");

nodeCLI.exec("eslint", "myfile.js");
'''

The nodeCLI utility has its own 'exec()' that is specifically for use when executing Node CLIs. It searches through the working
directory's 'node_modules' directory to find a locally installed utility. If it's not found there, then it searches globally. If
 it's still not found, then an error is thrown.

You can pass in as many string arguments as you'd like, and they will automatically be concatenated together with a space in between
, such as:

'''js
...
```

#### <a name="apidoc.element.shelljs-nodecli.getPath"></a>[function <span class="apidocSignatureSpan">shelljs-nodecli.</span>getPath (name, root)](#apidoc.element.shelljs-nodecli.getPath)
- description and source-code
```javascript
getPath = function (name, root) {

    var pkg = getPackage(name, root || "");

    if (pkg) {
        if (pkg.bin && pkg.bin[name]) {
            return "node " + path.join(root || "", "node_modules", name, pkg.bin[name]).replace(/\\/g, "/");
        }
    } else if (which(name)) {
        return name;
    }

    return "";
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

# Creating Node Package

NPM documentation: [Packages and modules](https://docs.npmjs.com/packages-and-modules/)

## [Creating a package.json file](https://docs.npmjs.com/creating-a-package-json-file)

### [Setting config options for the init command](https://docs.npmjs.com/creating-a-package-json-file#setting-config-options-for-the-init-command)

```bash
npm set init.author.email "example-user@example.com"
npm set init.author.name "example_user"
npm set init.license "MIT"
```

### [Creating a default package.json file](https://docs.npmjs.com/creating-a-package-json-file#creating-a-default-packagejson-file)

```bash
npm init --yes      

Wrote to /path/to/package/package.json:
{
  "name": "your-module-name",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "author <author@mail.com>",
  "license": "MIT"
}
```

Add `publishConfig`:

```json
"publishConfig": { "registry": "https://npm.pkg.github.com/<username>" }
```

### Fields

A `package.json` file must contain **"name"** and **"version"** fields.

- **name**: must be lowercase and one word, and may contain hyphens and underscores.
- **version**: must be in the form x.x.x and follow the [semantic versioning guidelines](https://docs.npmjs.com/about-semantic-versioning).
- author: `Your Name <email@example.com> (http://example.com)`. email and website are both optional.

---

## [Creating Node.js modules](https://docs.npmjs.com/creating-node-js-modules)

### [index.js](https://docs.npmjs.com/creating-node-js-modules#create-the-file-that-will-be-loaded-when-your-module-is-required-by-another-application)

```js
exports.printMsg = function() {
  console.log('Hello World')
}
```

### [Test your module](https://docs.npmjs.com/creating-node-js-modules#test-your-module)

### Login

Generate new token: [Personal access tokens](https://github.com/settings/tokens). Add the `repo` and `read:packages` scopes.

Add `GITHUB_TOKEN`:

```bash
vi ~/.npmrc

//npm.pkg.github.com/:_authToken=TOKEN
```

Login:

```bash
npm login --registry=https://npm.pkg.github.com/

Username: <your-npm-username>
Password: <TOKEN>
Email: (this IS public) <your-public-email>

Logged in as <your-npm-username> on https://registry.npmjs.org/.
```

#### Publish

- For private packages and unscoped packages: `npm publish`
- For scoped public packages: `npm publish --access public`

#### Demo

1. Create a new test directory outside of your project directory:

```bash
mkdir test-directory
cd /path/to/test-directory
```

2. Install your module:

```bash
npm install <your-module-name>
```

3. Create a `test.js`:

```js
const demo = require('creating-node-package')

demo.printMsg()
```

4. Run:

```bash
node test.js

Hello World
```

---

## In GitHub

Go to `https://github.com/<username>/<repository>/packages`.

Step 1: Use `publishConfig` option in your package.json
`"publishConfig": { "registry": "https://npm.pkg.github.com/<username>" }`

Step 2: Authenticate

`$ npm login --registry=https://npm.pkg.github.com/`

Step 3: Publish

`$ npm publish`
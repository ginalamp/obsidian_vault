# Errors or Mac Issues
#mac #javascript 


# Install Lodash
Solve issues

Issue 1: `npm ERR! Darwin 21.4.0 when installing lodash`
* Solution: update & upgrade brew
	* [gyp ERR! configure error #3220](https://github.com/lovell/sharp/issues/3220)

Issue 2: `npm error /usr/local/lib/node_modules/npm/lib/cli.js:2module.exports = async process => {^^^^^^^SyntaxError: Unexpected identifier`
* Solution: install nvm and then install node with nvm
	* [getting unexpected token in mac terminal after installing node](https://stackoverflow.com/questions/71032330/getting-unexpected-token-in-mac-terminal-after-installing-node)
		* [Node Version Manager](https://github.com/nvm-sh/nvm)
```shell
# update & upgrade brew
brew update && brew upgrade

# install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# install node with nvm
nvm install node

# install lodash
npm i -g npm
npm i lodash
```

# Run node after npm package init

Solution: add `"type": "module",` to top of `package.json` 
* [SyntaxError: Cannot use import statement outside a module](https://stackoverflow.com/questions/58384179/syntaxerror-cannot-use-import-statement-outside-a-module)

```json
// Example
{
   "type": "module", // added
   "name": "mosh-js-basics",
   "version": "1.0.0",
   "description": "mosh-js-basics-udemy",
   "main": "basics.js",
   ...
 }
```

# cheatSheet

Dev notes I often need. Visit at [cheatSheet.software](http://cheatsheet.software).

## Node

### Node Version Manager (NVM)

To manage the different versions of Node it makes sense to use the Node version Manager (NVM). 

* [`nvm` usage](https://github.com/creationix/nvm#usage)
* [Checking the installed Node version as Jest test](https://gitlab.com/tillg/scrapeMachine/blob/master/test.js)


### JSHint

In order to code in ES6 and tell this JShint, add a comment at the top of the file: `/* jshint esversion: 6 */` 

### JS, OOP and the sort

* [OOP in JS on Mozilla](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS)
* Very helpful: [The Object Explorer](https://sdras.github.io/object-explorer/) and [the Array Explorer](https://sdras.github.io/array-explorer/)
* About [Getter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get) and [Setter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set) on Mozilla.

### Logging

Some Winston documents:

* [Getting Started Quickly With Node.js Logging, April 2018, Erik Dietrich](https://blog.scalyr.com/2018/04/getting-started-quickly-node-js-logging/)
* [The source of winston documentation: The winston Repo ;)](https://github.com/winstonjs/winston)

In case you want to log JSON files to the console use [prettyjson](http://rafeca.com/prettyjson/).

### Building a CLI

* A good [article](https://scotch.io/tutorials/build-an-interactive-command-line-application-with-nodejs)
* Use [commander.js](https://github.com/tj/commander.js/)


### Promises

* [A Simple Guide to ES6 Promises, Brandon Morelli, May 14 2018](https://codeburst.io/a-simple-guide-to-es6-promises-d71bacd2e13a): A very clear introduction to Promises. I read it many times - and will probably have to read it more often...
* [Returning Promise and/or callback](https://stackoverflow.com/questions/36837963/javascript-return-promise-and-or-call-callback): How to write a function that returns a promise and/or uses Callbacks
* [Node's promisify and callbackify](https://medium.com/trabe/understanding-nodes-promisify-and-callbackify-d2b04efde0e0)
* [Function decorators: Transforming callbacks into promises and back again, Joel Thoms, May 2017](https://hackernoon.com/transforming-callbacks-into-promises-and-back-again-e274c7cf7293): Explains how his own version of `promisify` and `callbackify` works.
* [Dynamic Promise Chains](http://hellote.com/dynamic-promise-chains/)
* [A comprehensive approach to promises](https://codeburst.io/playing-with-javascript-promises-a-comprehensive-approach-25ab752c78c3): Very good explanation about `.then` chaining
* [ES6 Promises: Patterns and Anti-Patterns](https://medium.com/datafire-io/es6-promises-patterns-and-anti-patterns-bbb21a5d0918): Very good and helpful reading!

### Files, writing / reading

* [How to write file if parent folder doesn't exist?](https://stackoverflow.com/questions/16316330/how-to-write-file-if-parent-folder-doesnt-exist) A thing I often needed...

### Saving keys & passwords

How and where do you save passwords or keys that your codes need to run? Especially if your code lives publicly in Github?

Answer: Put your keys in an extra file that is not tracked in git (i.e. that is listed in your `.gitignore` file):

`keys.js`:
```javascript
// add this file to .gitignore

module.exports = {
        google: {
            clientID: 'enter your client id here',
            clientSecret: 'enter your client secret here'
        }
};
```

And then use it in your code. An example:

`passport-setup.js`:
```javascript
const passport = require('passport');
const GoogleStrategy = require('passport-google-oauth20').Strategy;
const keys = require('./keys');

passport.use(
    new GoogleStrategy({
        // options for google strategy
        clientID: keys.google.clientID,
        clientSecret: keys.google.clientSecret
    }, () => {
        // passport callback function
    })
);
```
Taken from [this video](https://www.youtube.com/watch?v=7udDtgLs0ss&list=PL4cUxeGkcC9jdm7QX143aMLAqyM-jTZ2x&index=7) (or see in [this repo](https://github.com/iamshaunjp/oauth-playlist/tree/lesson-7/config)).

### App formats: CLI and API based

To make a CLI based app use [`commander.js`](https://github.com/tj/commander.js/): 
```javascript
const program = require('commander');
// Require logic.js file and extract controller functions using JS destructuring assignment
const { addContact, getContact } = require('./logic');

program
  .version('0.0.1')
  .description('Contact management system');

program
  .command('addContact <firstame> <lastname> <phone> <email>')
  .alias('a')
  .description('Add a contact')
  .action((firstname, lastname, phone, email) => {
    addContact({firstname, lastname, phone, email});
  });

program
  .command('getContact <name>')
  .alias('r')
  .description('Get contact')
  .action(name => getContact(name));

program.parse(process.argv);
```

See for a more complete guide [here](https://scotch-io.cdn.ampproject.org/v/s/scotch.io/amp/tutorials/build-an-interactive-command-line-application-with-nodejs?amp_js_v=0.1&usqp=mq331AQGCAEoATgB#origin=https%3A%2F%2Fwww.google.com.vn&prerenderSize=1&visibilityState=prerender&paddingTop=54&p2r=0&horizontalScrolling=0&csi=1&aoh=15312707752711&viewerUrl=https%3A%2F%2Fwww.google.com.vn%2Famp%2Fs%2Fscotch.io%2Famp%2Ftutorials%2Fbuild-an-interactive-command-line-application-with-nodejs)

### `.gitignore`

A sample `.gitignore` file is [here](dot.gitignore).

## Bash

* Find a file somewhere on the disk: `sudo find / -name "*part-of-the-filename*.js"`
* Find the process id that is listening on a port: `lsof -i:3000`. Very often you want to kill this process: `kill <process id here>`
* Repeat last command with sudo: `sudo !!`
* Background tasks: `<whatever command> &`
* Execute a `.profile` so that the new settings become valid in the current shell: `source ~/.profile`

## Recent thoughts, reading, things to try

* [Build A Live Paint Application With React](https://codeburst.io/build-a-live-paint-application-with-react-ed534b403706): A thing I always wanted: Collaborative working on a board. May be this could be a starting point, and later we add a React-Native App on a large Android-powered touch screen...

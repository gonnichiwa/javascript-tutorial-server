# Tutorial server

Hi everyone!

This is a standalone server for the javascript tutorial https://javascript.info.

You can use it to run the tutorial locally and translate it into your language.

# Installation

(If you have an old copy of the English tutorial, please rename `1-js/05-data-types/09-destructuring-assignment/1-destructuring-assignment` to `1-js/05-data-types/09-destructuring-assignment/1-destruct-user`).


1. Install [Git](https://git-scm.com/downloads) and [Node.JS](https://nodejs.org).

    These are required to update and run the project.
    For Windows just download and install, otherwise use standard OS install tools (packages or whatever convenient).
    
    Please use Node.JS 10. 
    
    If you're using Node.JS 8, then the default NPM package manager is buggy, please update it with `npm up -g` command before you proceed.
    
    (Maybe later, optional) If you're going to change images, please install [GraphicsMagick](http://www.graphicsmagick.org/).

2. Install global Node modules:

    ```
    npm install -g bunyan gulp
    ```

3. Create the root folder.

    Create a folder `/js` for the project. You can use any other directory as well, just adjust the paths below.

4. Clone the tutorial server into it:

    ```
    cd /js
    git clone https://github.com/iliakan/javascript-tutorial-server
    git clone https://github.com/iliakan/jsengine javascript-tutorial-server/modules/jsengine
    ```

    Please note, there are two clone commands. That's not a typo: `modules/jsengine` is cloned from another repository.

5. Clone the tutorial text into it.

    The text repository has `"-language"` postfix at the end, e.g for the French version `fr`, for Russian – `ru` etc.
    
    E.g. for the Russian version:
    ```
    cd /js
    git clone https://github.com/iliakan/javascript-tutorial-ru
    ```

6. Run the site

    Run the site with the same language. Above we cloned `ru` tutorial, so:

    ```
    cd /js/javascript-tutorial-server
    ./edit ru
    ```

    This will import the tutorial from `/js/javascript-tutorial-ru` and start the server.

    Wait a bit while it reads the tutorial from disk and builds static assets.

    Then access the site at `http://127.0.0.1:3000`.

7. Edit the tutorial

    As you edit text files in the tutorial text repository (cloned at step 5), 
    the webpage gets reloaded automatically. 
 
    
# Change server language

The server uses English by default for navigation and other non-tutorial messages.

You can set another language it with the second argument of `edit`.

E.g. import `ru` tutorial and use `ru` locale for the server

```
cd /js/javascript-tutorial-server
./edit ru ru
```

Please note, the server must support that language. That is: server code must have corresponding locale files for that language, otherwise it exists with an error. As of now, `ru` and `en` are fully supported.
    
# Dev mode

If you'd like to edit the server code, *not* the tutorial text (assuming you're familiar with Node.js), then there are two steps.

First, run the command that imports (and caches) the tutorial:

```
// NODE_LANG sets server language
// TUTORIAL_ROOT is the full path to tutorial repo, by default is /js/javascript-tutorial-$NODE_LANG

cd /js/javascript-tutorial-server
NODE_LANG=en TUTORIAL_ROOT=/js/javascript-tutorial-ru npm run gulp jsengine:koa:tutorial:import
``` 
        
And then `./dev <server language>` runs the server:

```
cd /js/javascript-tutorial-server
./dev en
```

Running `./dev` uses the tutorial imported and cached by the previous command. 

It does not watch tutorial text, but it reloads the server after code changes.
 
Again, that's for developing the server code itself, not writing the tutorial.
    
# TroubleShooting

If something doesn't work – [file an issue](https://github.com/iliakan/javascript-tutorial-server/issues/new).

Please mention OS and Node.js version.

Also please pull the very latest git code and install latest Node.js modules before publishing an issue.

--  
Yours,  
Ilya Kantor 
iliakan@javascript.info


# Massachusetts State Retirement Board Retirement Calculator Prototype

Application can be found hosted here: http://gov-retirement-calculator.herokuapp.com/

## Overview

This repo contains team 302's retirement calculator rework. 

The app is structured as a SPA (single-page app) served with Express.js on a Node.js server. The logic and presentation are implemented using Angular.js. Some familiarity with the MEAN stack is recommended for development, although nothing needs to be modified to copy the project as-is.


This document outlines the necessary steps and precautions necessary for:  
* A developer who wishes to extend this application
* Operations to succcessfully host this application

## Development

### Setting up for local development  

This app does not rely on any external dependencies for local development. It is enough to run:


```
# within the project directory
$ npm install
$ node server.js
```
Then navigate to http://localhost:3000


### I want to modify *something*

### Changing the design of the webpage

The CSS and styling is implemented using the Massachusetts new Mayflower design library as a requirement. It is worth noting that the reference to the library is not secure, and HTTPS cannot be used (the style will not render otherwise).

There are also changes to the DOMAIN the library does, and to prevent such qualities or JQuery additional functions are created to set controller variables to reflect the correct values.

See ``public/views/calculator.view.client.html``

This file is almost entirely HTML/CSS, refer to the express documentation to see how it is combined with the index.html a layer up. One thing to watch out for is places where the values are bound to the Angular model

### Inserting an analytics framework or modifying the **header** 


See ``public/index.html``


Angular can sometimes obscure aspects of user interaction to analytics software, and this app was not designed with that in mind. Refer to your analytics' documentation.


### Modifying the calculator logic

See ``public/services/calculator.client.services.js:calculateData()``

### Implementing an external service to pull information

An open method and service is left for external calls to an API or database if needed or for future extensibility.

See ``public/services/calculator.client.services.js:retrieveInfo()``

### Tests

The test framework is implemented in Karma and Jasmine - with configurations for headless nodes in integration with testing through a Jenkins node with modified settings to alleviate potential compatibility issues.
Test coverage is also implemented with karma to show what is covered and what is not.

Testing can be initiated on the command line via the following commands:
``` 
npm test
karma start
```

For more, see ``karma.conf.js``


## Deployment

### Deploy from server

Follow the local deploy guidelines. In addition, a reverse proxy (such as nginx or apache) must be placed to properly listen on port 80 to redirect to the app, which listens on 3000. An [example of this configuration can be found on this StackOverflow post](https://stackoverflow.com/questions/5009324/node-js-nginx-what-now).

### Deploy to Heroku

This app is set up to be deployed to a heroku instance

```
$ npm install heroku-cli 
$ heroku login 				#This is will prompt for your heroku credentials
$ heroku git:clone -a <REPO>
$ git push heroku master    #To push it to Heroku's git repository
```

### Possible Hangups

* HTTPS / CORS policies

If CSS is not loading when the website is loaded over https, this is because the CSS is being pulled from the [Mayflower mass.gov style guide](mayflower.digital.mass.gov) over http. Many browser prevent this due to security reasons.

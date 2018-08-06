## Process managers

------
- [ ] **Use PM2**
------

Node processes are meant to fail-fast. Any unexpected errors would leave the server application in an unpredictable state and so it is better to exit the process and restart the server. However, the logic to restart the server needs to live somewhere outside of your node application. This is where process managers come in.

A Process Manager is responsible for maintaining multiple instances of the node processes for a single application. It is possible to roll your own, but as with most things it is best to use a mature framework if it exists because we need it to be reliable and proven.

#### PM2
[PM2](http://pm2.keymetrics.io/) is a process manager with many advanced features: monitoring, graceful shutdown, log file management, exception management, etc. It is available as an npm package.

#### nodemon
[nodemon](http://nodemon.io/) is mostly used for *local development*. It features file watching and can be configured with a config file. It can also run as a daemon.

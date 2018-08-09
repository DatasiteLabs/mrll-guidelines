# Node guidelines
Merrill Corporation: 2018 v1

## Purpose of this guide
* **Getting started with a new node project**: Infrastructure guides
* **Reference**: A knowledge base of conventions and best practices that should be used across all node projects

## Checklist
[Use this checklist](checklist.md) for your project to ensure that it aligns with the rest of the organization.

## Getting started

* [Node version](getting-started/node-version.md)
  * [ ] Use v10
* [Javascript features support](getting-started/javascript-features-support.md)
  * [ ] Use typescript
  * [ ] Remember to import the typings for third-party dependencies and to save them in devDependencies
  * [ ] Use the same `tslint.json` and `tsconfig.json` whenever possible
* [Frameworks](getting-started/frameworks.md)
  * [ ] Use express
* [Setting up Logging](getting-started/setting-up-logging.md)
  * [ ] Use Winston for logging
  * [ ] Use Splunk for log analysis


## Build

### Summary
* [ ] Use webpack to build
* [ ] Run the server with javascript (not typescript)
* [ ] Stay within confines of pipeline unless absolutely necessary

## Development

* [Project structure](development/project-structure.md)
  * [ ] Ensure that all filenames are *lower-case*
  * [ ] Ensure that the root index file contains the minimum amount of initialization code and nothing else
  * [ ] Ensure that you break the application up by *resources*
  * [ ] Ensure that you are using the recommended libraries for each use case
* [Testing](development/testing.md)
  * [ ] Use Jest
* [Non-blocking code](development/non-blocking-code.md)
  * [ ] Ensure that code does not block
  * [ ] Ensure that all I/O is asynchronous except in limited cases
  * [ ] Use promises for all asynchronous code - convert callbacks to promises if needed
* [Error handling](development/error-handling.md)
  * [ ] Ensure that exceptions are caught and minimize UncaughtExceptions
  * [ ] Ensure that promises have an error handler at the root of the promise chain
  * [ ] Use custom Errors to help with managing Errors
* [Callback hell](development/callback-hell.md)
  * [ ] embrace the functional nature of javascript: write small and single-purpose functions
  * [ ] consider using named functions instead of lambdas
  * [ ] favour promises over callbacks
  * [ ] if you use async/await, ensure that errors are handled
* [logging](development/using-logging.md)
  * [ ] use Winston for logging
  * [ ] initialize winston

### Authentication

#### Summary
- [ ] use Passport for authentication

## Configuration and set up

- [ ] Use PM2 as a process manager
- [ ] Use nginx as a reverse proxy
- [ ] Store all configuration in environment variables

* [Process management](configuration-setup/process-management.md)
* [Environment configuration](configuration-setup/environment-configuration.md)

### nginx
[Nginx](https://www.nginx.com/) should be used as a load balancer and for SSL termination before handing off to PM2.

## Checklist
Use this checklist to help you when developing an application

### Application setup
- [ ] **Using node v10**
- [ ] **Using typescript**
- [ ] **tsconfig and tslint are set up in standard way**
- [ ] **Using express**

### Build
- [ ] **Using pipeline provided**

### Development
- [ ] **lower-case filenames**
- [ ] **root index file only performs initialization**
- [ ] **libs are used to encapsulate domains**
- [ ] **promises are always returned from functions (rather than executing in the background)**
- [ ] **promises are always handled at the top level (in the controllers)**
- [ ] **global error handler exists**
- [ ] **uncaught exceptions are handled and process exits**
- [ ] **use of jest (older projects may use mocha)**
- [ ] **winston is set up**
- [ ] **winston is initialized at start up**
- [ ] **environment variables are captured at application startup**
- [ ] **application terminates if all the required environment variables are not present**
- [ ] **there is no blocking code except in very limited and deliberate cases**

### Running
- [ ] **PM2 is set up**

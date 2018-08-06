## Environment configuration

------
- [ ] **Use cfenv to retrieve the environment configuration in the application**
- [ ] **Make the application terminate if all the expected keys are not found**
------

Cloud Foundry has a particular way of injecting environment variables:

* [Cloud Foundry docs](https://docs.cloudfoundry.org/buildpacks/node/node-service-bindings.html)
* [cfenv](https://github.com/cloudfoundry-community/node-cfenv): Package to help with parsing the environment variables into an object that can be used immediately

> Rather than rolling our own, it is recommended to use this method of reading environment variables.

> Ensure that there is an initialization step when the app starts to read in the environment variables into the config service. Do not start the app unless all the expected variables are present.

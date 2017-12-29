# @barchart/log4js
## A fork of [log4js-node](https://github.com/log4js-node/log4js-node)

### Fork Obsolescence

The maintainer of log4js-node has indicated an intent to address the underlying issue in version 3.0 (link [here](https://github.com/log4js-node/log4js-node/issues/528#issuecomment-341386306)).
 
 
### Fork Rationale

This library was forked and modified to resolve incompatibility with between [webpack](https://webpack.js.org/) and dynamic module loading. In order to accomplish this, two changes were made:


#### Change 1: Use Template String for Dynamic Module Load

Specifically, the [configuration script](https://github.com/log4js-node/log4js-node/blob/master/lib/configuration.js#L52) uses the following syntax: 


    return require(modulePath);


This prevents webpack from building a dependency tree. Consequently, the code was modified use a template string:


    return require(`${modulePath}`);


This causes webpack to assume that all files within the context should be included. 


#### Change 2: Remove unnecessary appenders

Since the previous change will cause all script files to be included in the bundle, some appenders (with external dependencies) were removed. These include:

* lib/appenders/gelf.js
* lib/appenders/hipchat.js
* lib/appenders/logFaces-HTTP.js
* lib/appenders/logFaces-UDP.js
* lib/appenders/loggly.js
* lib/appenders/logstashUDP.js
* lib/appenders/mailgun.js
* lib/appenders/multiprocess.js
* lib/appenders/recording.js
* lib/appenders/redis.js
* lib/appenders/slack.js
* lib/appenders/smtp.js


# netsuite-js 
[![CircleCI](https://circleci.com/gh/Navomi-Jaden/netsuite-js/tree/master.svg?style=svg)](https://circleci.com/gh/Navomi-Jaden/netsuite-js/tree/master)
[![Known Vulnerabilities](https://snyk.io/test/github/navomi-jaden/netsuite-js/badge.svg)](https://snyk.io/test/github/navomi-jaden/netsuite-js)

A Node wrapper for the NetSuite SOAP API.


## Install

```bash
$ git clone git@github.com/Jaden-Giordano/netsuite-js.git
```


## Usage

```javascript
var NetSuite = require('netsuite-js');
var credentials =  {
  "email": "test@test.com",
  "password": "password",
  "account": 123456,
  "role": 3
};
var config = new NetSuite.Configuration(credentials);
var service = new NetSuite.Service(config);
service
  .init()
  .then(function(/*client*/) {
    console.log('WSDL processed. Service description:');
    console.log(service.config.client.describe());

    var recordRef = new NetSuite.Records.RecordRef();
    recordRef.internalId = 5084;
    recordRef.type = 'employee';

    console.log('Getting Employee record');
    return service.get(recordRef);
  })
  .then(function(result, raw, soapHeader) {
    if (result.readResponse.status.$attributes.isSuccess !== 'true') {
      console.error('Error');
      console.error(result.readResponse.status.statusDetail);
    }
    console.log(result);
    console.log('Last Request:');
    console.log(service.config.client.lastRequest);
  })
  .catch(function(err) {
    console.error(err);
  });
```

## Running the examples

* Copy `example/credentials.json.sample` to `example/credentials.json`
* Fill in with your NetSuite credentials
* Run `node example/simple.js` or other examples

## API
You can find autogenerated docs at: http://crosslead.github.io/netsuite-js/docs/lib/index.js.html

The autogenerated docs are created via the `gulp docs` task and pushed to the `gh-pages` branch.

_(More examples of end-to-end usage scenarios coming soon)_

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [gulp](http://gulpjs.com/).

This is a project based on Cucumber.js found at [https://www.npmjs.com/package/cucumber](https://www.npmjs.com/package/cucumber) and is only meant to be used alongside the project found there.

The purpose of this package is to save a JSON file of the cucumber report under the name output.json inside the Jenkins workspace to be used in generating cucumber reports.

I simply exchanged the process.stdout.write( data ) with a require('fs').writeFileSync('output.json', data, {encoding: 'utf-8'} ) when the JENKINS_HOME environment variable is present, all other functionality of cucumber is left alone and is taken from version 0.4.9.
This should cause all the reports inside of Jenkins to be printed to output.json and all local implementation to be left alone.

I also added a callback.skip()
Before there was only callback.pending() and callback.fail() but since our tests are relying on outside services I want the tests to skip and not fail if the services are not running or timing out ( you might argue that any external calls should be mocked but there are reasons against that in our case ). Use callback.skip() however you want, or choose not to! That's just why I included it in this latest version.

USAGE:

``` shell
$ npm install cucumber-for-jenkins
```

only use this inside of Jenkins, use cucumber-js for all local development, and only use the json format, as other formats will just be written to a file and not do you much good.

to run this in shell on Jenkins use the command

``` shell
node node_modules/.bin/cucumber-js -f json
```

skipping a step in cucumber

```javascript
    callback.skip();
```

All functionality is kept from cucumber-js so all the tags and scenario outlines and whatever other cool functionality you enjoy in version 0.4.9 is maintaned.
Once the feature test has completed, then check into your Jenkins workspace folder and you will find output.json in the root level.

Enjoy!

## Contact

* [chemdrew.com](http://chemdrew.com)

iPeer v4 Server
========================

**Master branch**

[![Build Status](https://travis-ci.org/cisdev2/ipeer4-server.svg?branch=master)](https://travis-ci.org/cisdev2/ipeer4-server)

**Dev branch**

[![Build Status](https://travis-ci.org/cisdev2/ipeer4-server.svg?branch=dev)](https://travis-ci.org/cisdev2/ipeer4-server)

**Code Analytics**

[![Code Climate](https://codeclimate.com/github/cisdev2/ipeer4-server/badges/gpa.svg)](https://codeclimate.com/github/cisdev2/ipeer4-server)
[![Test Coverage](https://codeclimate.com/github/cisdev2/ipeer4-server/badges/coverage.svg)](https://codeclimate.com/github/cisdev2/ipeer4-server)

Documentation
------------------------

See the [/doc](/doc) directory for more documentation and development notes.

Basics
------------------------
You will need composer: https://getcomposer.org/

Before developing or running, execute this command from the root of this repo to install the dependencies:

    composer install

To run the server:

    php app/console server:run

Once running, check out the auto-generated api documentation at: [http://localhost:8000/api/doc/](http://localhost:8000/api/doc/). Change the port as needed.

For tinkering, you can use the sandbox at `/api/doc`, a command line HTTP client, or a browser extension ([Postman - REST Client](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en) is quite nice).

Database
------------------------

When running for the first time, setup the database parameters in `app/config/parameters.yml`. Also run the following the create the database and tables for you:

    php app/console doctrine:database:create
    php app/console doctrine:schema:update --force

The tests make use of some "fixture" sample data. To load this into the regular database, run:

    php app/console doctrine:fixtures:load

To reset the database, run:

    php app/console doctrine:database:drop --force
    php app/console doctrine:database:create
    php app/console doctrine:schema:update --force

To reset the database and load the fixtures, use the `reset` shell script:
    ./app/reset

Tests
------------------------

Tests are automatically run at Travis CI: [https://travis-ci.org/cisdev2/ipeer4-server](https://travis-ci.org/cisdev2/ipeer4-server)

However, Travis can take a while to run, so we recommend testing manually and just testing the code/module/class your currently working on.

Tests can be run with `phpunit`. They run on a different database, so they don't affect the main one. Change `src` to a more specific path/file if you want to run a specific test. The `-c app` just loads the test config file from the `app` folder:

    phpunit -c app src

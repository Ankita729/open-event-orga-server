#  Open Event Orga Server

The Open Event Orga Server enables organizers to manage events from concerts to conferences and meetups. It offers features for events with several tracks and venues. Event managers can create invitation forms for speakers and build schedules in a drag and drop interface. The event information is stored in a database. The system provides API endpoints to fetch the data, and to modify and update it. Organizers can import and export event data in a standard compressed file format that includes the event data in JSON and binary media files like images and audio.

[![Build Status](https://travis-ci.org/fossasia/open-event-orga-server.svg?branch=master)](https://travis-ci.org/fossasia/open-event-orga-server)
[![Dependency Status](https://gemnasium.com/badges/github.com/fossasia/open-event-orga-server.svg)](https://gemnasium.com/github.com/fossasia/open-event-orga-server)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/1ac554483fac462797ffa5a8b9adf2fa)](https://www.codacy.com/app/fossasia/open-event-orga-server?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=fossasia/open-event-orga-server&amp;utm_campaign=Badge_Grade)
[![Issue Count](https://codeclimate.com/github/fossasia/open-event-orga-server/badges/issue_count.svg)](https://codeclimate.com/github/fossasia/open-event-orga-server)
[![Test Coverage](https://codeclimate.com/github/fossasia/open-event-orga-server/badges/coverage.svg)](https://codeclimate.com/github/fossasia/open-event-orga-server/coverage)
[![Coverage Status](https://coveralls.io/repos/github/fossasia/open-event-orga-server/badge.svg?branch=master)](https://coveralls.io/github/fossasia/open-event-orga-server?branch=master)
[![codecov](https://codecov.io/gh/fossasia/open-event-orga-server/branch/master/graph/badge.svg)](https://codecov.io/gh/fossasia/open-event-orga-server)
[![Gitter](https://badges.gitter.im/fossasia/open-event-orga-server.svg)](https://gitter.im/fossasia/open-event-orga-server?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

## Communication

Please join our mailing list to discuss questions regarding the project: https://groups.google.com/forum/#!forum/open-event

Our chat channel is on gitter here: https://gitter.im/fossasia/open-event-orga-server

## Demo version

A demo version is automatically deployed from our repositories:
* [Go to demo version deployed from master branch](http://open-event.herokuapp.com/)
* [Go to demo version deployed from development branch](http://open-event-dev.herokuapp.com/)

## Installation

### How do I install the Open Event System on a Server

Please check out [the documentation here](/docs/INSTALLATION.md).

### How do I run Open Event Server locally

A step-by-step guide on how to run Orga Server on a system locally can be found in [Installations document](/docs/INSTALLATION_LOCAL.md)

### How do I install Open-Event Server with Vagrant

For installation steps on how to deploy Open-Event Server using vagrant please refer to [Vagrant installation](docs/INSTALLATION_VAGRANT.md)

### How do I install Open Event Orga Server on Google Cloud

To install the system on Google Cloud please refer to the [Google Cloud installation readme](/docs/INSTALLATION_GOOGLE.md).

### How do I install the Open Event Orga Server on AWS

To install the system on AWS please refer to the [AWS installation readme](/docs/INSTALLATION_AWS.md).

### How do I install Open Event Orga Server on Digital Ocean

To install the system on Digital Ocean please refer to the [Digital Ocean installation readme](/docs/INSTALLATION_DIGITALOCEAN.md).

### How do I install Open Event Server with Docker

To install Open-Event Server with Docker please refer to [Docker installation](/docs/INSTALLATION_DOCKER.md)

### How do I deploy Open-Event Server to Heroku

For steps regarding how to deploy your version of the Open Event Server to Heroku, please refer [Heroku deployment](docs/INSTALLATION_HEROKU.md) or use the one button deployment.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Redis

Orga Server requires Redis to run Celery which runs the background tasks in the application.

To setup Redis in your system, use the `run_redis.sh` script. It will download and build redis in the project's folder.
Also if Redis has been already downloaded, it won't download it again.

```sh
bash run_redis.sh
```

To start the redis server, run the following command while at project's root directory.

```sh
redis-3.2.1/src/redis-server
```

You can use ampersand (&) at the end of the above command if you want to start redis server as daemon (i.e. in background).

```sh
redis-3.2.1/src/redis-server &
```

If you want to use a different Redis server than the above, then you can provide the server url in `REDIS_URL` environment variable.
The default value for `REDIS_URL` is `redis://localhost:6379/0` which is the same as that of local Redis server.


## Technology Stack

Please get familiar with the components of the project in order to be able to contribute.

### Components

* Database - [Postgres](https://www.postgresql.org)
* Webserver - [Nginx](https://www.nginx.com)
* App server - [uwsgi](https://github.com/unbit/uwsgi)
* Web framework - [flask](http://flask.pocoo.org) (particularly [flask-admin](https://github.com/flask-admin))

### Services and Dependencies

#### Authentication OAuth

OAuth is used to get information from Facebook and Google accounts, that enables users to sign in with their respective credentials:
 1. Google https://accounts.google.com/o/oauth2/auth
 2. Facebook https://graph.facebook.com/oauth

#### Twitter

The server integrates twitter on event pages. To obtain the required keys visit: https://dev.twitter.com/overview/documentation

#### Instagram

It is possible to extend the functionality and offer images from Instagram in the event service. To obtain required keys visit: https://www.instagram.com/developer/authentication/

#### Google Maps

We are using on Google maps to get information about location (info about country, city, latitude and longitude) https://maps.googleapis.com/maps/api/ We use it to get current location and display closes events.

#### Local Storage and Amazon S3

We are storing audio, avatars and logos either on local storage or Amazon S3. Read more about the set up of [Amazon S3 here](/docs/AMAZON_S3.md)

#### Sendgrid
To send emails we are using sendgrid
https://api.sendgrid.com/api/mail.send.json

#### Heroku Logs

We use heroku releases to see which version is deployed https://api.heroku.com/apps/open-event/releases
and we also use Github to get info about commit (for example: commit message, author name) at https://api.github.com/repos/fossasia/open-event-orga-server/commits

#### Payment Gateways

For ticket sales the service integrates payment gateways:
 1. Stripe
 2. Paypal

## API Access and Import/Export

Every installation of the project includes the API docs with Swagger, e.g. here on the test install http://open-event-dev.herokuapp.com/api/v2/ .

A hosted version of the API docs is available in the gh-pages branch of the repository at https://fossasia.github.io/open-event-orga-server/api/v2/

The data of events is provided over API endpoints as described [here](/docs/API.md)

It is also possible to export or import data matching the API structure as a compressed file with JSON and binary media files. Read more about this [here](/docs/IMPORT_EXPORT.md).

## Roles

The system has two kind of role type. 1. System roles are related to the Open Event organization and operator of the application. 2. Event Roles are related to the users of the system with their different permissions. Read more [here](/docs/ROLES.md).

## Configuration

### How to configure Bower

We use [Bower](http://bower.io) to manage front-end dependencies. `cd` to the directory where `bower.json` is stored and run:
* First we have to install npm and nodejs. Run the following:
```sudo apt-get install npm```

* Then run the following command to get Bower:
```sudo npm install -g bower```

* Finally run the following command to install the dependencies from bower.json:
```
bower install
```

Note: If you are working from within a proxied network of an organization/institute, Bower might not be able to install the libraries. For that, we need to configure .bowerrc to work via proxy.
* Open .bowerrc in any text editor like vim. Run:
```vim .bowerrc```
* The contents of .bowerrc will be something like this:
```
{
	"directory": "app/static/admin/lib"
}
```
* Modify the file to add "proxy" and "https-proxy" properties like this:
```
{
	"directory": "app/static/admin/lib",
	"proxy": "http://172.31.1.23:8080",
	"https-proxy": "http://172.31.1.23:8080"
}
```
* Save and exit. Now we can run ```bower install``` to install our libraries.


## Development

### Development Mode

To enable development mode (development Flask config), set `APP_CONFIG` environment variable to "config.DevelopmentConfig".

```
export APP_CONFIG=config.DevelopmentConfig
```

### Model updates

When writing changes to models. Use migrations.

 ```
 # To generate a migration after doing a model update
 python manage.py db migrate

 # To sync Database
 python manage.py db upgrade

 # To rollback
 python manage.py db downgrade

 ```

When checking in code for models, please update migrations as well.


## Testing

First install the repo and set up the server according to the steps listed. Make sure you have installed are the dependencies required for testing by running

```
pip install -r requirements/tests.txt
```

### Running unit tests

* Next go to the project directory and run the following command:
```
python -m unittest discover tests/unittests/
```
* It will run each test one by one.

* You can also use the following command to run tests using nosetests :
```
nosetests tests/unittests/
```

### Running robot framework tests
* Make sure you have FireFox installed
* Start your local flask server instance.
* Go to the project directory and Run the tests by using the following command.

```
robot -v SERVER:{server_name} -v SUPERUSER_USERNAME:{super_user_email_here} -v SUPERUSER_PASSWORD:{super_user_password} tests/robot
```

Change all the parameters inside `{}` as per your local server. The final command would look like:
```
robot -v SERVER:localhost:5000 -v SUPERUSER_USERNAME:test@opev.net -v SUPERUSER_PASSWORD:test_password tests/robot
```
* Once the tests are completed, a report and a log would be generated at `report.html` and `log.html` repectively in your root directory.

## Logging

Certain information is being logged and stored in the database for future reference, resolving conflicts in case of hacks and for maintaining an overview of the system. Read more about [loggin here](/docs/LOGS.md).

## Contributions, Bug Reports, Feature Requests

This is an Open Source project and we would be happy to see contributors who report bugs and file feature requests submitting pull requests as well. Please report issues here https://github.com/fossasia/open-event-orga-server/issues


## Branch Policy

We have the following branches
 * **development**
	 All development goes on in this branch. If you're making a contribution,
	 you are supposed to make a pull request to _development_.
	 PRs to master must pass a build check and a unit-test check on Travis
 * **master**
   This contains shipped code. After significant features/bugfixes are accumulated on development, we make a version update, and make a release.


## License

This project is currently licensed under the GNU General Public License v3. A
copy of LICENSE.md should be present along with the source code. To obtain the
software under a different license, please contact FOSSASIA.

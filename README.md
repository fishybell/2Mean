# TooMean
### Too Mean fo Life

An angular2 MEAN stack. Using webpack

## Install
Make sure you are using node ~7 to install.

To install clone the repo and npm install it. 

```bash
$ git clone <repo addr>
$ npm install
```

The first time installed, the package will generate a self signed
cert for TLS. If you want to generate a new one you can use
```bash npm run gen-cert```

## Running
To run use npm start. Wow that too is simple.

```bash
$ npm start
```

This command will run webpack and the server concurrently. Webpack will
watch for changes and compile typescript when a change is detected.

## Configure

### Hostname
If you are developing locally then you should be fine without this step.
Otherwise you must set the `TOOMEAN_APP_HOST` environment variable to the
hostname you use in your browser. Otherwise you will be unable to authenticate
users.

### AWS Access Keys

To use aws-s3 file upload functionality, a valid access key must be installed
on your local system at (by default):

- Mac/Linux: ~/.aws/credentials
- Windows: C:\\Users\\USERNAME\\.aws\\config

This file should contain your AWS Access key ID and secret, like so:

```
[default]
aws_access_key_id = <id>
aws_secret_accessKey = <key>
```

To enable s3 file storage you must edit your config/config.js in the following
ways:

- the `use` field must be set to `s3` for each upload type
- the `bucket` field in the `s3` object must be set
- the `dest` field in the `s3` object must be set

These can be hardcoded (don't do that) or set using environment variables.
Access keys can also be passed in as environment variables.
For more information or to use different configuration refer to 
[Configuring the AWS Command Line Interface] (http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)

### Elasticsearch Logging
To enable elasticsearch logging you must define the following environment
variables:

- `TOOMEAN_ES_HOST`
- `TOOMEAN_ES_PORT`

Optionally you can also enable the following environment variables:

- `TOOMEAN_ES_APIVERSION`
- `TOOMEAN_ES_CONSISTENCY`
- `TOOMEAN_LOG_LEVEL`

# Too Mean


## Add Menu item:
inside of app-client/module-name/config create a file called menu.json 
below is an example menu object for the articles module
```
[{
  "template": "Articles",
  "state": "/articles",
  "position": 2,
  "roles": [],
  "subitems": [
  {
    "template": "New",
    "state": "/articles/new",
    "roles": ["user"]
  },
  {
    "template": "List",
    "state": "/articles",
    "roles": ["user"]
  }]
}]

```
* template is the name of the menu item
* state is the routerLink
* roles is an array of user roles who the menu item will render for
* subitems will appear in a dropdown below the main menu item

## Role Manager
Admin users can configure roles in a tree structure to simplify
granting permissions to certain resources. For example, creating a
role called 'roleA' with parent 'user' would mean that the user role
has access to everything roleA can access as well. 

Users have one main role and an array of subroles depending on their
main role's position in the role tree. 

TODO: continue documentation once endpoints are dynamic and we have a 
UI for managing what roles a user is in.

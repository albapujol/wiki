# Readme

## About
As I wanted a wiki that just uses plain markdown files as backend, that is easy
to use and that is written in python, to enable me to easily hack around,
but found nothing, I just wrote this down. I hope that it might help others ,too.

## Features

* Markdown Syntax Editing
* Tags
* Regex Search
* Random URLs
* Web Editor
* Pages can also be edited manually, possible uses are:
	* use the cli
	* use your favorite editor
	* sync with dropbox
	* and many more
* easily themable
* Default Bootstrap3 theme.
* Integration with MathJax.

## Setup
Just clone this repository, cd into it, run `pip install -r requirements.txt`
and create `content/` in the root directory, and `config/` with a `config.py` in it,
that contains at least the following:

	# encoding: <your encoding (probably utf-8)
	SECRET_KEY='a unique and long key'
	TITLE='Wiki' # Title Optional
	
The `content` and `config` folder can be changed, respectively, by altering the parameters
`app.config['CONTENT_DIR']` and `app.config['CONFIG_DIR']` in the `app.py` file.

## Start
Afterwards just run the app however you want. I personally recommend something
like gunicorn:
	
	gunicorn app:app

You can install `setproctitle` with pip to get meaningful process names.

If you just want to try something out or debug something, you can execute
the app with `python app.py` which will run the development server in debug
mode. Have fun.

### Users
The users are stored in a file called `users.json`. This file must be located in the folder
specified in the configuration `app.config['CONFIG_DIR']`.


Example format (clear text and hashed password):
```json
{
  "admin": {
    "active": true, 
    "authentication_method": "cleartext", 
    "authenticated": false, 
    "password": "admin", 
    "roles": []
  }
   "admin_hashed": {
    "active": true, 
    "authentication_method": "hash", 
    "authenticated": false, 
    "hash": "....", 
    "roles": ['admin']
  }
}
```
Note: the hash can be computed using the `make_salted_hash` function on `app.py`.
Note: in the example, only `admin_hacked` will have edit permissions.

### Cache
A cahcue functionality has been added. The cache refreshes every 3600 seconds or when the page is edited
through the web interface. Still in beta phase.

To enable the cache, add the configuration to the `config.py` file:

    CACHE_TYPE = 'filesystem'
    CACHE_DIR = 'cache'

The redis cache is  implemented but not tested.

## Theming
The templates are based on jinja2. I used
[bootstrap](http://twitter.github.com/bootstrap/) for the design. NOTE: Updated to bootstrap3.
If you want to change the overall design, you should edit `templates/base.html`
and/or `static/bootstrap.css`. If you do not like specific parts of the site,
it should be fairly easy to find the equivalent template and edit it.

## Contributors

Thank you very much to my two top contributers @walkerh and @traeblain. You two have posted so many issues and especially solved them with so many pull requests, that I sometimes lose track of it! :)


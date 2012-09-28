ChatSecure Push Server
======================

An experimental design for a privacy-minded push server.

Installation
------------

You will need to install [CouchDB](http://couchdb.apache.org) using the package manager of your choice:

On Mac OS X, I recommend [Homebrew](http://mxcl.github.com/homebrew/):

    $ brew install -v couchdb

Or on Ubuntu:

    $ apt-get install couchdb

If you don't have Python and pip, get them.

    $ easy_install pip

Setup your virtual environment. You'll probably need to do some more stuff too.

    $ pip install virtualenv virtualenvwrapper
    $ mkvirtualenv cps
    $ workon cps
    
You will need to install the following dependencies: `apns`, `flask`, `couchdbkit`

    (cps)$ pip install apns flask couchdbkit
    
Setup
---------

TODO: Write this section.
    

Definitions
---------

**Device Push Token (DPT):** Unique (possibly changing) device token returned from iOS device. This is used by APNs to send messages to a specific endpoint.





      "account_id": {
          "password": "hashed password",
          "dpt": ["32 bytes of hex in string format", "This is returned from the iOS device"],
          "pat": ["randomly generated push access tokens"]
      }
    }

Server Functions
--------------

* `register(dpt, receipt)`
	* Returns `account_id` and `password`
	* Verifies In-App Purchase receipt with Apple before account creation
* `update_dpt(account_id, password, dpt)`
	* Updates the device push token for a user
* `request_pat(account_id, password)`
	* Returns a new push access token
* `list_pat(account_id, password)`
	* Returns a list of the currently active PATs
* `block_pat(account_id, password, pat)`
	* Removes a PAT from list of active PATs, removing it from the whitelist.
* `knock(account_id, pat, anonymous=false)`
	* Sends push message to active `dpt` associated with `account_id`
	* Only sent if `pat` is in the `account_id`'s whitelist 
	* If `anonymous` is `true`, don't send `pat` in push message.

License
---------

	ChatSecure Push Server
	Copyright (C) 2012 Chris Ballinger
	
	This program is free software: you can redistribute it and/or modify
	it under the terms of the GNU Affero General Public License as
	published by the Free Software Foundation, either version 3 of the
	License, or (at your option) any later version.
	
	This program is distributed in the hope that it will be useful,
	but WITHOUT ANY WARRANTY; without even the implied warranty of
	MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
	GNU Affero General Public License for more details.
	
	You should have received a copy of the GNU Affero General Public License
	along with this program.  If not, see <http://www.gnu.org/licenses/>.
---
layout: page
title: Rails Setup
permalink: /rails-setup/
---

These are the instructions to bring up the Rails environment for the dash-ingest codeline on your local machine.

### Software:

* ruby 2.1.2p95
* Rails 3.2.19

### Directories needed (create from top-level dash-ingest):

* uploads
* test_uploads
* log
* tmp/backup
* tmp/pids
* tmp/cache
* tmp/sockets 

### Modify as needed:

* config/database.yml
* config/datashare.yml
* config/merritt.yml
* deploy.rb (if doing deployment) 

### Run Rake task for populating the institution table, only when deploying the app for the first time on a server:

````
$ RAILS_ENV=env bundle exec rake db:setup
```` 

(replace 'env' with the name of the current environment).


When **running rails server**, you have to specify the local environment like this:  Why?

The local is an environment that Mark created and I think it’s a workaround for user login problems since you can’t easily get a shibboleth login locally because of encryption, certificates and having to run some shib software.  It basically automatically logs you in to the app with a fake user. (It’s the user with NULL email address in the database.)

````
$ RAILS_ENV=local rails server
````

**Capistrano commands**: (from your local if you have ssh on the server)

````
$ Cap development deploy
$ Cap development deploy:restart
````

The test command is:

````
$ RAILS_ENV=test rake test:integration
````

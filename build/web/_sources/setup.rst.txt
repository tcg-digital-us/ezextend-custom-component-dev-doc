
Setup
=====

NVM
---

Set NVM to use the NodeJs version required for this project:

.. parsed-literal::

   nvm use \ |node-version|\ 

Nginx
-----

ezeXtend will require an Nginx reverse proxy so that calls made to local routes will be redirected to their relevant services, whether those services are running on the local dev machine, or on a cloud-hosted VM.

To edit the Nginx configuration you are going to want to add a configuration file named :code:`ezeXtend_proxy`  inside the folder :code:`/etc/nginx/sites-available/`. Within the file, you will need to define an Nginx server and the proxy route locations with minimal configuration, such as below:

.. code:: none

   server {
      location /module_designer/ {
         proxy_pass http://127.0.0.1:3001/;
      }

      location /elastic_api/ {
         proxy_pass http://127.0.0.1:9241/;
      }
   }

The purpose of this configuration is to only register two url routes, :code:`/module_designer/` and :code:`/elastic_api/` that redirect calls for both the ezeXtend react page itself and the Elasticsearch database.

Now you can start Nginx with:

.. code:: bash

   sudo nginx

.. NOTE::

   If Nginx starts successfully, you will see no errors or output, as it begins the server and runs it in the background. Because Nginx starts and runs in the background, before trying to run it, it is helpfull to use :code:`htop` before hand to ensure that it isn't already running. If it us, kill the currently running Nginx with :code:`sudo pkill -9 nginx`.

ezeXtend
--------

Now we must prepare the ezeXtend project to be run. The ezeXtend project is split into two pieces, one inside of the other. The module designer project contains both the frontend for the ezeXtend page (in the :code:`ui` folder) as well as backend code (in :code:`server`) that helps it interface with Kibana/Elasticsearch behind the scenes.

Whenever we are extending the functionality of the front end (creating custom visualisations, etc.) we can run the front end in either a development mode which lacks an amount of full functionality, or a release mode that more closely emulates the full functionality of the page when working in tandem with Kibana/Elasticsearch. To achieve that full release functionality, you must build the :code:`ui` react project inside :code:`module_designer` and use the Nginx reverse proxy to provide Elasticsearch connection functionality. This may sound confusing but we will cover both aspects.

Development Mode
################

To run ezeXtend in development mode, execute:

.. code:: bash 

   cd /EZEXTEND_ROOT/ui
   npm install
   npm start

Assuming all went well, then the react project should start up and be available at :code:`http://localhost:3000`.

Release Mode
############

To run ezeXtend in release mode, execute:

.. code:: bash

   cd /EZEXTEND_ROOT/
   npm install
   cd /EZEXTEND_ROOT/ui
   npm install
   npm run build
   cd ..
   npm start

Again, assuming all went well, then the release version of the React project should be available at :code:`http://<local domain>/module_designer` where the :code:`<local domain>` can either be localhost, or any host that you have listed in your :code:`/etc/hosts` file that redirect to :code:`127.0.0.1`.
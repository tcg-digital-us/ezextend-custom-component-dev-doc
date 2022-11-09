
Install
=======

To work with ezeXtend, first you must install the current ezeXtend codebase in your development workspace. The current way to do this is to get the pre-setup project provided in the subversion repository for Mcube version |mcube-version|. The subversion repository link is: 

.. parsed-literal::
    
   \http://svnmcube.tcgdigital.com/svn/MCube_Implementation/Development_Artefacts/Dev-Area/\ |mcube-version|\ /

Clone the repository to a folder of your choice, such as your user home folder.

.. note::

   Use our Subversion guide (here) if you are unfamiliar with retrieving projects using TCG Digital's Subversion repository.

Once you have cloned the Subversion repository, the codebase for ezeXtend can be found within:

.. parsed-literal:: 

   \ |mcube-version|\ /Code/module_designer/

Going forward, this :code:`module_designer` folder will be referred to as :code:`/EZEXTEND_ROOT`.

NVM
---

Node Version Manager is essential when working within a NodeJS environment as it allows us to download and use specific versions of NodeJS and Node Package Manager (NPM) given that many different projects may require different versions. The installation instructions for NPM can be found on `their website <https://github.com/nvm-sh/nvm#installing-and-updating>`_

After installing, tell NVM to download the specific version we need (If you already have this version installed, you can skip the installation command):

.. parsed-literal::

   nvm install \ |node-version|\ 


Nginx
-----

**Minimum Version: 14+ (v16.13.2 reccomended)**

Nginx is a server software that we will be using as a simple reverse proxy for our development environment. This is required so that we can develop 'as if' we are working with a backend located outside of our development environment or on the cloud, etc. This is important for greater control in port allocation and bypassing any issues that might arise from violating Cross-Origin Resource Sharing (CORS) policy.

You will need to install the latest version of Nginx on your development environment. If you are using our Dockerized development container, then Nginx should alredy be installed.

This guide will only cover configuration for Linux based operating systems, so Windows or Mac users may need to adapt this guide to however Nginx differs on those systems (locations of config files, etc.).

Install Nginx with your package manager, e.g.:

.. code::

   sudo apt-get install nginx

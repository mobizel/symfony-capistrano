Symfony Capistrano
==================

Symfony capistrano allow you to deploy your Symfony application using `Capistrano`_ and `Symfony Flex`_ Composer plugin.

Installation
------------

This repository hosts contributed recipes for Composer packages that are not
part of the "official" `Symfony recipes`_. To enable recipes defined in this
repository for your project, run the following command:

.. code-block:: bash

    composer config extra.symfony.allow-contrib true

Add the package to your composer requirements.

.. code-block:: bash

    composer require mobizel/symfony-capistrano

How to deploy using Capistrano
------------------------------

Note:

This page give some hit about Capistrano. To go further check `the official documentation`_

Capistrano is a common tools to deploy a Symfony app. It allows to deploy your app without any interruption.
Your document root in on a symlink which corresponds to a release directory.
This symlink is updated when your build finished successfully.


**Install Dependencies**

We are going to use `Bundler`_ to install capistrano

.. code-block:: bash

    $ gem install bundler

Run bundler install command to install gem dependancies in the project Gemfile


.. code-block:: bash

    $ bundle install

.. _Bundler: http://bundler.io

**Configure your environments**

By defaults, there are two environments pre-configured:

* staging
* production

These environments are configured in on ``etc/capistrano/deploy/`` directory.
Replace ``XX.XXX.XX.XXX`` with your server ip addresses

**Deploy the staging environment**

.. code-block:: bash

    $ bundle exec "cap staging deploy"

**Deploy the production environment**

.. code-block:: bash

    $ bundle exec "cap production deploy"

**Create your own task**

Capistrano allow you to build your own to exec during your deployment.
This exemple create a task that execute a command on deployment target server.

.. code-block:: ruby

    namespace :namespace do
        desc "task description"
        task :task_name do
          on roles(:all) do |host|
                  execute 'command executed on target server'
          end
        end
    end

**Tasks hooks**

Capistrano provides hooks in order to exec your task before or after a specific task.
For example if you want to run a task to set a proxy on a remote server before any git check :

.. code-block:: ruby

    before 'git:check', 'deploy:add_proxy'

.. _`Capistrano`: http://capistranorb.com
.. _`Symfony Flex`: https://github.com/symfony/flex
.. _`Symfony recipes`: https://github.com/symfony/recipes
.. _`the official documentation`: http://capistranorb.com

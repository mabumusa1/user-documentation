How to install Mautic
#####################

There are several ways to install Mautic, you should select the most appropriate method for your situation and technical knowledge.

- :ref:`Installing from the production package`, either :ref:`using the web-based installer` or :ref:`installing at the command line<Installing with command line>`,
- Installing locally by :ref:`cloning from GitHub<Installing from GitHub>` - for testing and local development,
- :ref:`Installing with Composer`

Installing from the production package
**************************************

The Mautic production package can be installed either by uploading the zipped installation package into the server location or using command line installations. The Mautic production package also requires access to a database server.

The Mautic installation is a three-step process:

1. Integrate the database server with the Mautic server.
   
2. Create an administrator account to access the Mautic server.
   
3. Set up the email server for email marketing automation.

Preparing for installation
==========================

Before installing a package, ensure that:

* Your server environment meets the minimum requirements for the version you are installing. Read more in :xref:`Mautic's Requirements`.
  
* Your server directory is writable by the Mautic web server.
  
* Your database meets the minimum requirements for the supported databases and valid user permissions to access to the database. Read more in :xref:`Mautic's Requirements`.
  
* Your server has enough free disk space to run the installation. Consider the database size as well.
  
* PHP's `max_execution_time` is at least 240 seconds.

Downloading a production package
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To get started :xref:`Download Mautic` to access the zip file of the latest stable release. 

For more information about the available Mautic packages, visit the Mautic Releases :xref:`Mautic Releases` page.

Uploading the production package
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After downloading a desired package, upload the package zip file to your web server, and unzip it in the directory where the Mautic instance will be hosted.

Your web server must have the permissions to access the unzipped files. For more information on file and folder permissions, visit [this page](troubleshooting/file-ownership-and-permissions).

Using the web-based installer
=============================

To access the Mautic server from your browser, enter the URL that corresponds to the Mautic instance (for example, `https://m.example.com`) in your web browser. It is recommended to secure your installation with an SSL certificate (https).

Conducting Environment checks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After loading the package in the server, the Mautic installer checks if it can run successfully in your server environment. 

Installation errors, displayed in red, must be resolved for completing the Mautic package installation successfully. Warnings, displayed in orange, are often recommendations for a better Mautic experience.

.. image:: images/mautic-install-pre-flight-check.png
  :width: 600
  :alt: Screenshot showing Mautic pre-flight checks with warning about installing on a non-SSL connection

If the environment check is successful (green), click **Next Step** to begin the installation process.

Integrating the Database
~~~~~~~~~~~~~~~~~~~~~~~~

Mautic assumes that the database is on the same server as Mautic.  

For setting the database server on the **Mautic Installation-Database Setup** window:

* Select **Database Driver**.
  
* Enter **Database Host**.
  
* Enter **Database Name**.
  
* Enter **Database Username**.
  
* If desired, you can also enter values for **Database Port**, **Database Table Prefix**, **Database Password**, and **Prefix for backup tables**.
  
* By default, **Backup existing tables?** is turned on, but you should turn it off for a new installation.

.. image:: images/mautic-database-configuration.png
  :width: 600
  :alt: Screenshot of database configuration screen

Click **Next Step**.

Creating the administrator user account
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create an Administrator account for your Mautic instance, enter values for the different fields on the **Mautic Installation - Administrative User** window. 

.. image:: images/mautic-create-admin-user.png
  :width: 600
  :alt: Screenshot showing the create user screen

Click **Next Step**.

Configuring Email settings
~~~~~~~~~~~~~~~~~~~~~~~~~~

To configure your Email settings for your Mautic instance, enter details of your email provider on the **Mautic Installation - Email Configuration** window. You can use a tool such as :xref:`Mailhog` to configure a local instance for testing. 

.. image:: images/mautic-email-configuration.png
  :width: 600
  :alt: Screenshot showing the email configuration screen

For configuring your Email sender settings:

* Enter the name and email address of the user whose credentials will be used by default for all outgoing email communications. Verify that the provided email address has been successfully authorized by your email provider.
  
* **Queue** emails and send them through a cron job (to trigger the queue processing) instead of sending them immediately for for larger instances of email handling.
  
* Select **Mailer transport**. If your provider isn't listed, select **Other SMTP Server** and provide the SMTP credentials. API-based sending is significantly faster than SMTP. Depending on the provider you select, additional fields appear to allow you to enter API keys and select regions.
  
* Enter **Server** and **Port** for your email provider.
  
* Select **Encryption** and **Authentication mode** for your email provider.

Click **Next Step** to log into the Mautic server.

Logging into Mautic
~~~~~~~~~~~~~~~~~~~

On the Mautic login window, enter your Mautic administrator credentials to log into your Mautic instance. 

.. image:: images/mautic-login-screen.png
  :width: 600
  :alt: Screenshot of Mautic login screen

Click **login** to continue working on your Mautic instance.

Installing with command line
============================

Mautic can also be installed using the command line. You can either pass the settings parameters in the command, or create a local PHP file with your database settings. You can also define properties in this file using the syntax expected by the command-line options. 

Use the command ``path/to/php bin/console mautic:install --help`` for the list of options and flags available.

.. code-block:: php

     --db_driver=DB_DRIVER                    Database driver. [default: "pdo_mysql"]
      --db_host=DB_HOST                        Database host.
      --db_port=DB_PORT                        Database port.
      --db_name=DB_NAME                        Database name.
      --db_user=DB_USER                        Database user.
      --db_password=DB_PASSWORD                Database password.
      --db_table_prefix=DB_TABLE_PREFIX        Database tables prefix.
      --db_backup_tables=DB_BACKUP_TABLES      Backup database tables if they exist; otherwise drop them. [default: true]
      --db_backup_prefix=DB_BACKUP_PREFIX      Database backup tables prefix. [default: "bak_"]
      --admin_firstname=ADMIN_FIRSTNAME        Admin first name.
      --admin_lastname=ADMIN_LASTNAME          Admin last name.
      --admin_username=ADMIN_USERNAME          Admin username.
      --admin_email=ADMIN_EMAIL                Admin email.
      --admin_password=ADMIN_PASSWORD          Admin user.
      --mailer_from_name[=MAILER_FROM_NAME]    From name for email sent from Mautic.
      --mailer_from_email[=MAILER_FROM_EMAIL]  From email sent from Mautic.
      --mailer_transport[=MAILER_TRANSPORT]    Mail transport.
      --mailer_host=MAILER_HOST                SMTP host.
      --mailer_port=MAILER_PORT                SMTP port.
      --mailer_user=MAILER_USER                SMTP username.
      --mailer_password[=MAILER_PASSWORD]      SMTP password.
      --mailer_encryption[=MAILER_ENCRYPTION]  SMTP encryption (null|tls|ssl).
      --mailer_auth_mode[=MAILER_AUTH_MODE]    SMTP auth mode (null|plain|login|cram-md5).
      --mailer_spool_type=MAILER_SPOOL_TYPE    Spool mode (file|memory).
      --mailer_spool_path=MAILER_SPOOL_PATH    Spool path.

Use the syntax below within a local .php file:

.. code-block:: php

  <?php
  // Example local.php to test install (to adapt of course)
  $parameters = array(
    // Do not set db_driver and mailer_from_name as they are used to assume Mautic is installed
    'db_host' => 'localhost',
    'db_table_prefix' => null,
    'db_port' => 3306,
    'db_name' => 'mautic',
    'db_user' => 'mautic',
    'db_password' => 'mautic',
    'db_backup_tables' => false,
    'db_backup_prefix' => 'bak_',
    'admin_email' => 'admin@example.com',
    'admin_password' => 'mautic',
    'mailer_transport' => null,
    'mailer_host' => null,
    'mailer_port' => null,
    'mailer_user' => null,
    'mailer_password' => null,
    'mailer_api_key' => null,
    'mailer_encryption' => null,
    'mailer_auth_mode' => null,
  );

Installing with a local PHP file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 

Run the following command after replacing the path to PHP bin and mautic instance URL. 

``path/to/php bin/console mautic:install https://m.example.com``

If desired, you can also add parameters in the install command:

.. code-block:: php

  path/to/php bin/console mautic:install https://m.example.com
  --mailer_from_name="Example From Name" --mailer_from_email="mautic@localhost"
  --mailer_transport="smtp" --mailer_host="localhost" --mailer_port="1025"
  --db_driver="pdo_mysql" --db_host="db" --db_port="3306" --db_name="db" --db_user="db" --db_password="db" 
  --db_backup_tables="false" --admin_email="admin@mautic.local" --admin_password="mautic"

As the installation process begins, it flags up warnings and aborts if there are any critical errors.

.. code-block:: shell

  Mautic Install
  ==============

  Parsing options and arguments...
  0 - Checking installation requirements...
  Missing optional settings:
    - [0] The <strong>memory_limit</strong> setting in your PHP configuration is lower than the suggested minimum limit of %min_memory_limit%. Mautic can have performance issues with large datasets without sufficient memory.
  Ready to Install!
  1 - Creating database...
  1.1 - Creating schema...
  1.2 - Loading fixtures...
  2 - Creating admin user...
  3 - Email configuration and final steps...

  ================
  Install complete
  ================

You can now login to your Mautic instance with your Mautic admin credentials.

Installing from GitHub
**********************
TODO

Installing with Composer
************************
Since :xref:`Mautic 4` it's possible to install and manage Mautic using the full power of Composer. Mautic uses the lastest version of :xref:`Composer`.

Mautic is in the process of decoupling plugins and themes from core, however at present while they have been technically mirrored out into separate repositories, the source files remain in the main :xref:`Mautic GitHub repository`.

When you clone from GitHub, running ``composer install`` installs all the dependencies, there are some other handy features which you can take advantage of when installing and managing Mautic.

Using the Recommended Project
=============================

The Mautic :xref:`Recommended Project` is a template which provides a starter kit for managing your Mautic dependencies with Composer.

.. note::
  The instructions below refer to the global composer installation. You might need to replace composer with ``php composer.phar`` or something similar for your setup.

The basic command to use the Recommended Project is:

.. code-block:: shell

  composer create-project mautic/recommended-project:^4 some-dir --no-interaction

With Composer you can be required to download new dependencies to your installation.

.. code-block:: shell

  cd your-directory
  composer require mautic/mautic-saelos-bundle:~2.0

The Composer ``create-project`` command passes ownership of all files to the created project. You should create a new git repository, and commit all files not excluded by the .gitignore file.

What does the Recommended Project template actually do?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When installing the given composer.json the following occurs:

- Install Mautic in the docroot directory.
- Autoloader uses the generated composer autoloader in vendor/autoload.php, instead of the one provided by Mautic in docroot/vendor/autoload.php.
- Plugins - packages of type mautic-plugin - are in docroot/plugins/.
- Themes - packages of type mautic-theme - are in docroot/themes/.
- Creates docroot/media directory.
- Creates environment variables based on your .env file. See .env.example.

Updating Mautic Core
~~~~~~~~~~~~~~~~~~~~

The Recommended Project attempts to keep all of your Mautic core files up-to-date.

The project ``mautic/core-composer-scaffold`` updates your scaffold files whenever there is an update to ``mautic/core-lib``.

If you customize any of the "scaffolding" files - commonly .htaccess - you may need to merge conflicts if new release of Mautic Core result in changes to your modified files.

Follow the steps below to update your core files.

1 Run ``composer update mautic/core-lib --with-dependencies`` to update Mautic core and its dependencies.

2 Run ``git diff`` to determine if any of the scaffolding files have changed. Review the files for any changes and restore any customizations to .htaccess or others.

3 Commit everything all together in a single commit, so the docroot remains in sync with the core when checking out branches or running git bisect.

4 In the event that there are non-trivial conflicts in step 2, you may wish to perform these steps on a branch, and use ``git merge`` to combine the updated core files with your customized files. This facilitates the use of a three-way merge tool such as :xref:`kdiff3`. This setup isn't necessary if your changes are simple; keeping all of your modifications at the beginning or end of the file is a good strategy to keep merges easy.

5 Run the following commands to update your database with any changes from the release:

.. code-block:: shell

  bin/console cache:clear 
  bin/console mautic:update:apply --finish 
  bin/console doctrine:migration:migrate --no-interaction 
  bin/console doctrine:schema:update --no-interaction --force 
  bin/console cache:clear

Composer FAQs
=============

Should you commit downloaded third party plugins?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Composer says that the :xref:`Composer commit dependencies`. They provide arguments against but also workarounds if a project decides to do it anyway.

Should you commit the scaffolding files?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The :xref:`Mautic Composer scaffold` plugin can download the scaffold files - for example index.php, .htaccess - to the docroot/ directory of your project.


If you haven't customized those files you could choose to not commit them in your version control system - for example, git. If that's the case for your project it might be convenient to automatically run the Mautic Scaffold plugin after every install or update of your project.

You can achieve that by registering `@composer mautic:scaffold` as post-install and post-update command in your composer.json:

.. code-block:: json

  "scripts": {
      "post-install-cmd": [
          "@composer mautic:scaffold",
          "..."
      ],
      "post-update-cmd": [
          "@composer mautic:scaffold",
          "..."
      ]
  },

How can you apply patches to downloaded plugins?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you need to apply patches - depending on the plugin, a pull request is often a better solution - you can do so with the composer-patches plugin.

To add a patch to Mautic plugin foobar insert the patches section in the extra section of composer.json:


.. code-block:: json

  "extra": {
      "patches": {
          "mautic/foobar": {
              "Patch description": "URL or local path to patch"
          }
      }
  }

How can you specify a PHP version?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This project supports PHP 7.4 as the minimum version currently (check :xref:`Mautic's Requirements`), however, it's possible that a Composer update may upgrade some package that could then require PHP 7+ or 8+.

To prevent this you can add this code to specify the PHP version you want to use in the config section of composer.json:

.. code-block:: json

  "config": {
      "sort-packages": true,
      "platform": {
          "php": "7.4"
      }
  },

Setting up a local testing environment with DDEV
************************************************

Often there is a need to have a local environment for testing Mautic - for example making a backup, testing new features or bug fixes.

We use DDEV as our tool of choice for this purpose. It is very easy to work with.

To learn how to set up DDEV with Mautic, please check the documentation in the Contributors Handbook at https://contribute.mautic.org/contributing-to-mautic/tester.
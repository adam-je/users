Installation
============

Composer
------

```
composer require cakedc/users:~3.0
```

if you want to use social login features...

```
composer require opauth/opauth:1.0.x-dev
composer require opauth/facebook:1.0.x-dev
composer require opauth/twitter:1.0.x-dev
```

Creating Required Tables
------------------------
If you want to use the Users tables to store your users and social accounts:

```
bin/cake migrations migrate -p Users
```

Note you don't need to use the provided tables, you could customize the table names, fields etc in your
application and then use the plugin configuration to use your own tables instead. Please refer to the [Extending the Plugin](Extending-the-Plugin.md) 
section to check all the customization options

Load the Plugin
-----------

Ensure the Users Plugin is loaded in your config/bootstrap.php file

```
Plugin::load('Users', ['routes' => true, 'bootstrap' => true]);
```

Customization
----------
(please specify direcory name)/config/bootstrap.php
```
Configure::write('Users.config', ['users']);
Plugin::load('Users', ['routes' => true, 'bootstrap' => true]);
```

Then in your config/users.php
```
return [
    'Opauth.Strategy.Facebook.app_id' => 'YOUR APP ID',
    'Opauth.Strategy.Facebook.app_secret' => 'YOUR APP SECRET',
    //etc
];
```

For more details, check the Configuration doc page

Load the UsersAuth Component
---------------------

Load the Component in your (please specify direcory name)/src/Controller/AppController.php, and use the passed Component configuration to customize the Users Plugin:

```
    public function initialize()
    {
        parent::initialize();
        $this->loadComponent('Flash');
        $this->loadComponent('Users.UsersAuth');
    }
```



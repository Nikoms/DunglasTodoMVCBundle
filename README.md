DunglasTodoMVCBundle
====================

This a [Symfony](http://symfony.com) implementation of [TodoMVC](http://todomvc.com/).

> TodoMVC is a project which offers the same Todo application implemented using MV* concepts in most of the popular JavaScript MV\* frameworks of today.

It uses [Backbone.js](http://backbonejs.org/) and [Chaplin.js](http://chaplinjs.org/) client-side and [FOSRestBundle](https://github.com/FriendsOfSymfony/FOSRestBundle) for the REST JSON API server-side.
The client-side code is wrote in [CoffeeScript](http://coffeescript.org/).

Screenshot
----------

![screenshot](https://raw.github.com/addyosmani/todomvc/gh-pages/screenshot.png)

Yes, this is TodoMVC.

Install
-------

First, [install Symfony using Composer](http://symfony.com/doc/current/book/installation.html).
Go yo your application directory and use composer to install the bundle and its dependencies:

    composer require dunglas/todomvc-bundle dev-master

Next, enable these bundles in `AppKernel.php`:

```php
// app/AppKernel.php
public function registerBundles()
{
    return array(
        // ...
        new JMS\SerializerBundle\JMSSerializerBundle($this),
        new FOS\RestBundle\FOSRestBundle(),
        new Dunglas\TodoMVCBundle\DunglasTodoMVCBundle(),
        // ...
    );
}
```

Add these lines at the end of `app/config/config.yml`:

```yaml
fos_rest:
    routing_loader:
        default_format: json
    body_listener:
        decoders:
            json: dunglas.decoder.jsonToForm
```

Add DunglasTodoMVCBundle to Assetic's bundles option in `config.yml`:

```yaml
assetic:
    #...
    bundles:        [ DunglasTodoMVCBundle ]
```

And the routes to `app/config/routing.yml`:

```yaml
dunglas_todomvc:
    resource: "@DunglasTodoMVCBundle/Resources/config/routing.yml"
    prefix:   /
```

Last step, isntall the assets:

    php app/console assets:install web

Open *http://localhost/app_dev.php* in your browser and try this Symfony implementation of TodoMVC.

Compile the client side-code
----------------------------

If you want to rebuild the client-side CoffeScript code go to the `Ressources/` directory and run:

    coffee --bare --output public/js/ coffee/

Add the `--watch` option to recompile at each change.
Of course you need the CoffeeScript compiler.

Credits
-------

This bundle has been created by [Kévin Dunglas](http://dunglas.fr).
The CoffeeScript code is largely inspired of the [Brunch + Chaplin TodoMVC implementation](https://github.com/addyosmani/todomvc/tree/gh-pages/labs/dependency-examples/chaplin-brunch) of [Paul Millr](http://paulmillr.com/).

![TodoMVC](https://raw.github.com/addyosmani/todomvc/gh-pages/media/logo.png)
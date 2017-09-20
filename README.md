Installation
============

Step 1: Download the Bundle
---------------------------

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```console
$ composer require wearejust/image-optim-bundle "~1"
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter](https://getcomposer.org/doc/00-intro.md)
of the Composer documentation.

Step 2: Enable the Bundle
-------------------------

Then, enable the bundle by adding it to the list of registered bundles
in the `app/AppKernel.php` file of your project:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Wearejust\ImageOptimBundle\WearejustImageOptimBundle(),
        );

        // ...
    }

    // ...
}
```

Step 3: Add extra config to your `config.yml` file
-------------------------

It's possible to override the config we provide, you can specify an custom yml file ```(as Resources/config/theme.yml)``` the following way:

```yml
parameters:
  liip_imagine.jpegoptim.binary: '%kernel.root_dir%/../src/Wearejust/ImageOptimBundle/Resources/bin/jpegoptim'
  liip_imagine.optipng.binary: '%kernel.root_dir%/../src/Wearejust/ImageOptimBundle/Resources/bin/optipng-x64'
  liip_imagine.pngquant.binary: '%kernel.root_dir%/../src/Wearejust/ImageOptimBundle/Resources/bin/pngquant-x64'
  post_processes:
      jpegoptim: { strip_all: true, max: 70, progressive: true }
      optipng: { strip_all: true, level: 5 }

```

After adding this you will be able to use the `post_processes` variable in the defined filter presets. An example for this:

```yml
liip_imagine :

    filter_sets :
        cache : ~

        home_hero_image:
            quality: 100
            filters:
                thumbnail:
                    crop: { start: [0, 0], size: [1100, 1100] }
                    position: center
            post_processors: '%post_processes%'
```
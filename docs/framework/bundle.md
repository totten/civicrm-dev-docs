# Bundle Reference

!!! note "Bundles were introduced in CiviCRM 5.31."

A *resource* is an element that you can mix into the page -- such as a static Javascript file or a dynamic snippet of CSS code.  A resource
*bundle* is a collection of logically related resources.  Using a bundle makes it easy to activate, deactivate, or replace resources as a
group.

## Example

Suppose we've got an improved calendar widget named `mycalendar`. The calendar widget requires several resources:

* JS file (to define the rendering logic and interactive behaviors)
* CSS file (to refine the styling and layout)
* Settings data (to designate some date preferences)

Using the [Resources API](resources.md), we could add each indivudally:

```php
Civi::resources()
  ->addScriptFile('civicrm', 'js/mycalendar.js')
  ->addStyleFile('civicrm', 'css/mycalendar.css')
  ->addVars('mycalendar', [
    'fmt' => Civi::settings()->get('myDateFormat'),
    'minYear' => date('Y', strtotime('-10 years')),
    'maxYear' => date('Y', strtotime('+10 years')),
  ]);
```

A calendar widget is interesting because it may be used on many different pages (e.g.  dashboard, activity management, event management),
and we need to load the same list of resources for all of them.  At the same time, some of those resources may be heavy, and it's
inefficient to load those resources if they're not needed.  How do we load them consistently?  We can use a bundle.

Any pageload that needs `mycalendar` should add the bundle:

```php
Civi::resources()->addBundle('mycalendar');
```

## Register a bundle

Separately, the author of `mycalendar` needs to define the bundle. For example:

```php
function mymodule_civicrm_container($container) {
  $container->addResource(new \Symfony\Component\Config\Resource\FileResource(__FILE__));
  $container->setDefinition('bundle.mycalendar', new \Symfony\Component\DependencyInjection\Definition('CRM_Core_Resources_Bundle', ['mycalendar']))
    ->setFactory('CRM_Core_Resources_Common::createBasicBundle')->setPublic(TRUE);
}


Civi::dispatcher()->addListener('hook_civicrm_alterBundle',function($e) {
  switch ($e->bundle->name) {
    case 'mycalendar':
      $e->bundle->addScriptFile(E::LONG_NAME, 'js/mycalendar.js');
      break;
  }
}, 1000);
```


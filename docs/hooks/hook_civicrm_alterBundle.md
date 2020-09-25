# hook_civicrm_alterBundle

## Summary

A bundle is a collection of closely related [resources (JS, CSS, settings, etc)](../framework/resources.md).
Application-pages may load a bundle by calling `addBundle($name)`, e.g.

```php
Civi::resources()->addBundle(`bootstrap3`)
```

Use `hook_civicrm_alterBundle` to add, modify, or replace resources in a bundle.

## Availability

This hook is available in CiviCRM 5.31 and later.

## Definition

```php
function hook_civicrm_alterBundle($bundle)
```

## Parameters

- `$bundle` - `\CRM_Core_Resources_Bundle`

## Example: Provide `bootstrap3`

By default, the `bootstrap3` bundle is empty.  It is the responsibility of a theme/extension to provide concrete files (CSS/JS) with actual styling.

For example, the core-extension `greenwich` defines a theme (look-and-feel). If the user has chosen this look-and-feel, and if the
application-page uses `bootstrap3`, then we should load the CSS/JS provided by `greenwich`:

```php
function greenwich_civicrm_alterBundle(CRM_Core_Resources_Bundle $bundle) {
  $theme = Civi::service('themes')->getActiveThemeKey();
  switch ($theme . ':' . $bundle->name) {
    case 'greenwich:bootstrap3':
      $bundle->clear();
      $bundle->addStyleFile('greenwich', 'dist/bootstrap3.css');
      $bundle->addScriptFile('greenwich', 'extern/bootstrap3/assets/javascripts/bootstrap.min.js', [
        'translate' => FALSE,
      ]);
      break;
  }
}
```

## List of standard bundles

| Name | Version | Functional description | Default content |
| -- | -- | -- | -- |
| `bootstrap3`    | `5.31` | Loaded only on pages that use [Bootstrap v3 CSS classes](https://getbootstrap.com/docs/3.3/) | No content. Displays a warning. |
| `coreResources` | `5.31` | Loaded as a baseline on all Civi-based pages. | jQuery, select2, and a number of Civi utilities. |
| `coreStyles`    | `5.31` | Loaded as a baseline on all Civi-based pages and *some* CMS-based pages. (Ex: Drupal "View User" may embed Civi profiles.) | `civicrm.css` and/or the `customCSSURL`. |


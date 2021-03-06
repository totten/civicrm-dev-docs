Every API call consists of three elements: the *entity*, *action*, and
*parameters*.  For example, consider a few commonly-used entities along
with the supported actions and parameters:


| Entity                   | Description              | Actions |  Parameters       |
|--------------------------|--------------------------|---------|-------------------|
| <code>Contact</code>     | An individual, <br /> organization, or <br />house-hold.         |<code>create</code><br/><code>get</code><br/><code>delete</code><br/>| <code>contact\_type</code><br /> <code>first\_name</code>  <br /><code>last\_name</code> <br /><code>preferred\_language</code>       |
| <code>Activity</code>    | An phone call, meeting,<br /> or email message. that <br /> has occurred (or will <br /> occur) at a specific <br /> date and time|<code>create</code><br/><code>get</code><br/><code>delete</code><br/>| <code>activity\_type\_id</code> <br /> <code>source\_contact\_id</code> <br /> <code>assignee\_contact\_id</code>    |
| <code>Address</code>     | A street-address related <br /> to a contact. |<code>create</code><br/><code>get</code><br/><code>delete</code><br/>| <code>contact\_id</code>,  <br /> <code>street\_address</code> <br /> <code>city</code>  <br /> <code>state\_province\_id</code> <br /> <code>country\_id</code>     |

(*For full, up-to-date details about specific entities and parameters, use the "API Explorer".*)

The API is available in many different environments (such as PHP, REST, and
Javascript), and the notation differs slightly in each environment.
However, if you understand the canonical notation, then other environments
will appear as small adaptations.

Canonically, an API call is processed by the API kernel.  The `$entity`,
`$action`, and `$params` are passed as inputs, and an associative-array is
returned as output.

```php
$result = Civi::service('civi_api_kernel')->run('Contact', 'get', array(
  'version' => 3,
  'first_name' => 'Alice',
  'last_name' => 'Roberts'
));
```

The result of a successful API call typically looks like this:

```php
array(
  'is_error' => 0,
  'version' => 3,
  'count' => /* number of records */,
  'values' => /* array of records */,
)
```

The result of a failed API call typically looks like this:

````
array(
  'is_error' => 1,
  'error_message' => /* a descriptive error message */,
)
````

(**Note**: A few specialized actions like `getsingle` or `getvalue` may
return success in a different format.)


PHP (civicrm_api3)
------------------

This is the most common way to call the API.

```
try {
  $contacts = civicrm_api3('contact', 'get', array(
    'first_name'  =>  'Alice',
    'last_name'   =>  'Roberts',
  ));
}
catch (CiviCRM_API3_Exception $e) {
  $error = $e->getMessage();
}
printf("Found %d item(s)\n", $contacts['count']);
```

This format matches canonical format almost exactly, with a few improvements
for usability:

 * The function `civicrm_api3()` is easier to remember.
 * The `version => 3` parameter is not required.
 * Errors are reported as PHP exceptions. You may catch the exceptions or (by default) allow
   them to bubble up.

*Note*: If you're writing a Drupal module, a Joomla extension, a WordPress
plugin, or a standalone script, then you may need to **bootstrap** CiviCRM
before using the API.  See the examples in [Bootstrap
Reference](/confluence/display/CRMDOC/Bootstrap+Reference). 


PHP (class.api.php)
----------------------------

CiviCRM v3.4 introduced an object-oriented API client, `class.api.php`.
This class be used locally or remotely to invoke APIs, as in:

```php
require_once 'your/civicrm/folder/api/class.api.php';
$api = new civicrm_api3();
$apiParams = array(
   'first_name'   =>  'Alice',
   'last_name'    =>  'Roberts'
);
if ($api->Contact->Get($apiParams)) {
   //each key of the result array is an attribute of the api
    echo "\n contacts found ".$api->count;
   'contact_type'=>'Individual','return'=>'sort_name,current_employer')) {
} else {
    echo $api->errorMsg();
}
```
 

If you call the API in the object oriented fashion, you do not have to
specify 'version' as a parameter

REST
----

````javascript

// For external services
http://www.example.com/sites/all/modules/civicrm/extern/rest.php
  ?api_key=t0ps3cr3t
  &key=an07h3rs3cr3t
  &json=1
  &debug=1
  &version=3
  &entity=Contact
  &action=get
  &first_name=Alice
  &last_name=Roberts

// For sessions already authenticated by the CMS (e.g. AJAX)
http://www.example.com/civicrm/ajax/rest
  ?json=1
  &debug=1
  &version=3
  &entity=Contact
  &action=get
  &first_name=Alice
  &last_name=Roberts

````

Obviously you should substitute your site in! You can explore the syntax
and options available using the [api
explorer](http://sandbox.civicrm.org/civicrm/ajax/doc#explorer) (also on
your site!)

Please note that the REST interface is subject to [API Security](/confluence/display/CRMDOC/API+Security).

For more details, see [REST
interface](http://wiki.civicrm.org/confluence/display/CRMDOC/REST+interface). 

AJAX
----

````
CRM.api3('entity', 'action', [params], [statusMessage]);

````

For more details, see [AJAX
Interface](/confluence/display/CRMDOC/AJAX+Interface).

The AJAX interface is automatically available for web-pages generated through CiviCRM (such as ***standard CiviCRM web-page****s***, CiviCRM ***extensions***, and custom CiviCRM ***templates***).

The AJAX interface could be made available to other parts of the same website (e.g. a drupal module or wordpress widget) by calling CRM\_Core\_Resources::singleton()-\>addCoreResources() from php. Please note that the AJAX interface is subject to [API Security](/confluence/display/CRMDOC/API+Security) and [Same Origin Policy](http://en.wikipedia.org/wiki/Same_origin_policy). To use it from an external site or application, see REST interface documentation.

Smarty
------

````

{crmAPI var="myContactList" entity="Contact" action="get" version="3" first_name="Alice" last_name="Roberts" }
Found {$myContactList.count} item(s).

````


The smarty call is to add extra information, therefore *create* or
*delete* actions don't make sense in this case.

For more details, see [Smarty API
interface](/confluence/display/CRMDOC/Smarty+API+interface).

CLI (drush)
-----

```
## To run on the default Drupal site
drush civicrm-api contact.get first_name=Alice last_name=Roberts

## To run on Drupal multisite, specify the site name
drush -l www.example.com civicrm-api contact.get first_name=Alice last_name=Roberts
```

CLI (wp-cli)
-----

```
wp civicrm-api contact.get first_name=Alice last_name=Roberts
```

CLI (cv)
-----

````
cv api contact.get first_name=Alice last_name=Roberts
````

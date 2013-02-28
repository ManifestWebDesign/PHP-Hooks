PHP-Hooks
=========
Standalone Hook / Event helper library for PHP


Basic usage:
------------
```php
Hook::add('my_hook', function($message){
  echo $message;
});
Hook::call('my_hook', 'Hello world');  // echo 'Hello world'
```

Removing a single callback from a hook:
---------------------------------------
Hook internally creates unique ids for callbacks, so they can be removed
```php
$callback = function($message){
  echo $message;
};
Hook::add('my_hook', $callback);
Hook::call('my_hook', 'Hello world');  // echo 'Hello world'
Hook::remove('my_hook', $callback);
Hook::call('my_hook', 'Hello world'); // does nothing
```

Removing all callbacks for a hook:
----------------------------------
```php
Hook::add('my_hook', function($message){
  echo $message;
});
Hook::remove('my_hook');
Hook::call('my_hook', 'Hello world'); // does nothing
```

Priority and return false
----------------------------------
```php
Hook::add('my_hook', function($message){
  echo $message;
}, 100); // priority of 100
Hook::add('my_hook', function(){
  return false;
}, 99);
Hook::call('my_hook', 'Hello world'); // does nothing, because the callback that returned false was executed first
```

Get all Hooks
----------------------------------
```php
Hook::add('my_hook', function($message){
  echo $message;
}, 100); // priority of 100
Hook::add('my_hook', function(){
  return false;
}, 99);
Hook::get('my_hook'); // returns numeric array with both callbacks, in the order that they would execute
```

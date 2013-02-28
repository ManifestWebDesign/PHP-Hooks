PHP-Hooks
=========
Standalone Hook / Event helper library for PHP


Basic usage:
------------
Hook::add('my_hook', function($message){
  echo $message;
});
Hook::call('my_hook', 'Hello world');  // echo 'Hello world'


Removing a single callback from a hook:
---------------------------------------
$callback = function($message){
  echo $message;
};
Hook::add('my_hook', $callback);
Hook::call('my_hook', 'Hello world');  // echo 'Hello world'
Hook::remove('my_hook', $callback);
Hook::call('my_hook', 'Hello world'); // does nothing


Removing all callbacks for a hook:
----------------------------------
Hook::add('my_hook', function($message){
  echo $message;
});
Hook::remove('my_hook');
Hook::call('my_hook', 'Hello world'); // does nothing


Priority and return false
----------------------------------
Hook::add('my_hook', function($message){
  echo $message;
}, 100); // priority of 100
Hook::add('my_hook', function(){
  return false;
}, 99);
Hook::call('my_hook', 'Hello world'); // does nothing, because the callback that returned false was executed first

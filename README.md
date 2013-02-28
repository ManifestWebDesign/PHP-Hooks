PHP-Hooks
=========
Standalone Hook / Event helper library for PHP


Basic usage:
------------
<pre><code>
Hook::add('my_hook', function($message){
  echo $message;
});
Hook::call('my_hook', 'Hello world');  // echo 'Hello world'
</code></pre>

Removing a single callback from a hook:
---------------------------------------
<pre><code>
$callback = function($message){
  echo $message;
};
Hook::add('my_hook', $callback);
Hook::call('my_hook', 'Hello world');  // echo 'Hello world'
Hook::remove('my_hook', $callback);
Hook::call('my_hook', 'Hello world'); // does nothing
</code></pre>

Removing all callbacks for a hook:
----------------------------------
<pre><code>
Hook::add('my_hook', function($message){
  echo $message;
});
Hook::remove('my_hook');
Hook::call('my_hook', 'Hello world'); // does nothing
</code></pre>

Priority and return false
----------------------------------
<pre><code>
Hook::add('my_hook', function($message){
  echo $message;
}, 100); // priority of 100
Hook::add('my_hook', function(){
  return false;
}, 99);
Hook::call('my_hook', 'Hello world'); // does nothing, because the callback that returned false was executed first
</code></pre>

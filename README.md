# SimpleConfig

SimpleConfig is a basic configuration container, for PHP.

## Installation

To pull down dependencies and check version compatibility you will need to run [composer](http://getcomposer.org) in
the project root.

## Usage

Values and factories can be provided in the constructor:

```php
$container = new \SimpleConfig\Container(
	[
		'field1' => 'value',
		// etc
	],
	[
		'field2' => function() {
			return new Foo();
		}
	]
);
```

Alternatively, `offsetSet` and `factory` can be used to add values and factories respectively.

The `Container` class implements `ArrayAccess`, so values can simply be accessed using array syntax, e.g.

```php
echo $container['field1']; // prints "value"
```

Factories are invoked once on field fetch, with the resulting value being cached for future use. Factories
can retrieve other values from the container by simply utilising `$this`, e.g.

```php
$container->factory('foo', function() {
	$class = $this['foo.class'];
	return new $class();
});
```
---
layout: default
---

# Factories

## $this->factory->post->create();

Create a post for the testing.

### Description

```
int $this->factory->post->create( array $args[, array $generation_definitions] );
```

Create a post for the testing and returns a post ID.

### Parameters
### Return Values
### Errors/Exceptions

### Example

```
<?php

class SampleTest extends WP_UnitTestCase {

	function testSample() {
		$post_id = $this->factory->post->create_and_get(array('post_title' => 'Hello!'));
		//$post = $this->factory->post->get($post_id);
		var_dump($post_id);
		$this->assertTrue($post_id === 3);
	}
}

```


## $this->factory->post->create_and_get();

```
$this->factory->post->create_and_get();
```

## $this->factory->post->create_many();

```
$this->factory->post->create_many();
```

## $this->factory->attachment->create();

```
$this->factory->attachment->create();
```

## $this->factory->attachment->create_and_get();

```
$this->factory->attachment->create_and_get();
```


## $this->factory->attachment->create_many();
## $this->factory->comment->create();
## $this->factory->comment->create_and_get();
## $this->factory->comment->create_many();
## $this->factory->user->create();
## $this->factory->user->create_and_get();
## $this->factory->user->create_many();
## $this->factory->term->create();
## $this->factory->term->create_and_get();
## $this->factory->term->create_many();
## $this->factory->category->create();
## $this->factory->category->create_and_get();
## $this->factory->category->create_many();
## $this->factory->tag->create();
## $this->factory->tag->create_and_get();
## $this->factory->tag->create_many();
## $this->factory->blog->create();
## $this->factory->blog->create_and_get();
## $this->factory->blog->create_many();
## $this->factory->network->create();
## $this->factory->network->create_and_get();
## $this->factory->network->create_many();

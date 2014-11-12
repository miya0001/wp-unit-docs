---
layout: default
---

# Factory

## $this->factory->post->create();

Create a post for the testing.

### Description

```
int $this->factory->post->create( array $post[, array $generation_definitions] );
```

Create a post for the testing and returns a post ID.

### Parameters

#### $post

(array) (required) An array representing the elements that make up a post.

| Key | Description | Example value |
|-----|----|----|
| post_content | The full text of the post. | Hello World! |
| post_name | The name (slug) for your post | hello-world |
| post_title | The title of your post. | Hello World! |
| post_status | The status of the post. | publish |
| post_type | The post type. | post |
| post_author | The user ID number of the author. | 1 |
| post_excerpt | For all your post excerpt needs. | Hello World! |
| post_date | The time post was made. | 2014-11-11 23:45:30 |

There are other parameters, see [codex](http://codex.wordpress.org/Function_Reference/wp_insert_post).

#### $generation_definitions

(array) (optional) The Generation definitions of the post.

```
$this->default_generation_definitions = array(
	'post_status' => 'publish',
	'post_title' => new WP_UnitTest_Generator_Sequence( 'Post title %s' ),
	'post_content' => new WP_UnitTest_Generator_Sequence( 'Post content %s' ),
	'post_excerpt' => new WP_UnitTest_Generator_Sequence( 'Post excerpt %s' ),
	'post_type' => 'post'
);
```

### Return Values

(int) The ID of the post.


### Example

```
<?php

class SampleTest extends WP_UnitTestCase {

	function testSample() {
		$post_id = $this->factory->post->create( array( 'post_title' => 'Hello!' ) );
		$this->assertEquals( 'Hello!', get_the_title( $post_id ) );
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

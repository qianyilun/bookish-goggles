## Introduction
This is a practice project for self-learning from [Udemy](https://www.udemy.com/php-with-laravel-for-beginners-become-a-master-in-laravel).

###Laravel Fundamentals - Routes
* Naming Routes (26)
    * Sometimes, the url might be super long. For a better experience, we can rename it as by using array.
      Please refer it to `routes/web.php` line 22.
    ```php
      // We use an array to wrap everything
      Route::get('admin/posts/example', array('as'=>'admin.home', function() {
      $url = route('admin.renamed'); // <- than we can access it by using the short name
      return "this url is " . $url;
      }));
    ```

###Laravel Fundamentals - Controller
* Create Controller (28)

    ```$ php artisan make:controller --resource PostsController```

    With **resource**, some of functions - `index(), create(), store(), show(), edit(), update() destroy()` will created for you automatically. 

* Routing Controllers (29)

  In `routes/web.php`

  ```php
  Route::get('/post', 'PostsController@index');
  ```

* Passing Data (30)

  In `routes/web.php`. @ will direct the request to which function that will be invoked.

  ```php
  Route::get('/post/{id}', 'PostsController@index');
  ```

  In `App/Http/Controllers/PostsController.php`

  ```php
  public function index($id)
  {
      return "its working the number " . $id;
  }
  ```

* Resource and Controllers (31)

  In `routes/web.php`

  ```php
  Route::resource('posts', 'PostsController');
  ```

  It will automatically generate all routing functions in the backend. 

  If we type `$php artisan route:list `

  ```bash
  |		 | Method	 | URI					  | Name			 | Action
  +--------+-----------+------------------------+------------------+--------+
  |        | GET|HEAD  | posts                  | posts.index      | App\Http\Controllers\PostsController@index                             | web          |
  |        | POST      | posts                  | posts.store      | App\Http\Controllers\PostsController@store                             | web          |
  |        | GET|HEAD  | posts/create           | posts.create     | App\Http\Controllers\PostsController@create                            | web          |
  |        | GET|HEAD  | posts/{post}           | posts.show       | App\Http\Controllers\PostsController@show                              | web          |
  |        | PUT|PATCH | posts/{post}           | posts.update     | App\Http\Controllers\PostsController@update                            | web          |
  |        | DELETE    | posts/{post}           | posts.destroy    | App\Http\Controllers\PostsController@destroy                           | web          |
  |        | GET|HEAD  | posts/{post}/edit      | posts.edit       | App\Http\Controllers\PostsController@edit                              | web          |
  |        | POST      | register               |                  | App\Http\Controllers\Auth\RegisterController@register                  | web,guest    |
  |        | GET|HEAD  | register               | register         | App\Http\Controllers\Auth\RegisterController@showRegistrationForm      | web,guest    
  +--------+-----------+------------------------+------------------+--------------------
  ```

  * What URL to access the method?

    `.../posts/1 ` or `.../posts/create`

###Laravel Fundamentals - Views


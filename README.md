# Laravel Fractal

A Laravel Service Provider for [League/Fractal](http://fractal.thephpleague.com).

## Installation

Add laravel-fractal to your composer.json file:

```
"require": {
    "gathercontent/laravel-fractal": "dev-master"
}
```

Get composer to install the package:

```
$ composer update gathercontent/laravel-fractal
```

### Registering the Package

Register the service provider within the ```providers``` array found in ```app/config/app.php```:

```php
'providers' => array(
    // ...
    'GatherContent\LaravelFractal\LaravelFractalServiceProvider'
)
```

Add an alias within the ```aliases``` array found in ```app/config/app.php```:


```php
'aliases' => array(
    // ...
    'Fractal' => 'GatherContent\LaravelFractal\LaravelFractalFacade',
)
```

### Configuration

To override the default configuration, you can publish the config files to your application.
Artisan can do this automatically for you via the command line:

```
$ php artisan config:publish gathercontent/laravel-fractal
```

## Usage

### Basic Example

Formatting a single item:

```php
// routes.php
Route::get('/me', array('before' => 'auth', function () {
    return Fractal::item(Auth::user(), new UserTransformer);
}));
```

Formatting a collection:

```php
// routes.php
Route::get('/comments', function () {
    return Fractal::collection(Comment::all(), new CommentTransformer);
});
```

Paginating a collection:

```php
// routes.php
Route::get('/comments', function () {
    $paginator = Comment::paginate();
    $comments = $paginator->getCollection();

    return Fractal::collection($comments, new CommentTransformer, $paginator);
});
```

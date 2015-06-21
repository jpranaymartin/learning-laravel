# Laravel
***
## Laravel 5 Fundamentals
Laravel is an MVC PHP framework. It uses Composer as a package and dependency manager. PHP Artisan is the 'make' equivalent.

### Composer

A package manager for php code.  
Add and update dependencies.

- use `require` to add
- use `update -no--dev` in case of warning messages

- [http://getcomposer.org](http://getcomposer.org)
  - #### Download and make global:  
  `$ curl -sS http://getcomposer.org/installer | php`  
  `$ mv composer.phar usr/local/bin/composer`

Create project: `$ composer create-project laravel/laravel AppFolder`  

<div class='well well-sm'>
Note: use `php -S localhost:9000 -t public` to start the server from the project directory.
</div>
### Routes, Controllers, and Views

File | Location
-----|---------
Routes | /app/Http/routes.php
Controllers | /app/Http/Controllers/
Views | /app/resources/views

#### New 'Page' or 'Action' Workflow:

1. Specify URI in Route file  
`Route::get('uri', 'SomeController@method');`  
Example:  
`Route::get('about', 'PagesController@about');`

2. Add method to controller  
```
public function method() {
    // Eloquent actions and variable setup
    return view('folder.view')->with('name', $name);
}
```  
Example:  
Create PagesController: `$ php artisan make:controller PagesController` (optional flag: `--plain` to avoid resourceful routing boilerplate).  
  * Add method:
```
public function about() {
        $name = 'John Smith';
    return view('pages.about')->with('name', $name);
    //
    // or
    //
    return view('pages.about')->with([
        'name'  => 'John',
        'name2' => 'Jane'
    ]);
    //
    // or
    //
        $data = [];
        $data['name']  = 'John';
        $data['name2'] = 'Jane';
    return view('pages.about', $data);
    //
    // or
    //
        $name = 'John';
        $name2 = 'Jane';
    return view('pages.about', compact('name', 'name2'));
}
```

3. Add folder/view.blade.php  
Example:
  * Create /views/pages/about.blade.php
  * Echo `$name` with `{!! $name !!}` or `{{ *some escaped data* - use in case of user-submitted data }}`

### Blade Fundamentals

Blade allows regular HTML tags and structure.  

Special blocks:
* `@yield('sectionName')` will be placed with any section in the extend-*ing* file marked by `@section('sectionName')...@endsection`.
* Other tags:
  * `@extends('parent')`
  * `@if (condition)...@else...@endif`
  * `@unless` (the opposite of `@if`)
  * `@foreach($collection as $item)...@forelse...@endforeach`

***
##### By Joseph Martin.

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects. Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

You may also try the [Laravel Bootcamp](https://bootcamp.laravel.com), where you will be guided through building a modern Laravel application from scratch.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).


# Laravel Bootcamp

## Quick Installation

```bash
composer create-project laravel/laravel chirper
cd chirper
php artisan serve
```

After that change on .env the DB_CONNECTION to sqlite and delete all other DB_* options.

I did the installation using laragon evironment, but you can use docker as well, just follow the bootcamp guide. 😉

## Installing Laravel Breeze

I chose Vue.js for this section and beyond.

```bash
composer require laravel/breeze --dev
php artisan breeze:install vue
```

Be mindful that laravel/breeze manages the front-end, that said recall it everytime you went to modify the fron-end.

Now run npm Vite module to "hot-module replacement", that means your changes in the code goes direct to the page, it gonna reload as you change it.

```bash
npm install
npm run dev
```

Laravel Artisan also takes care of the Database, run:

```bash
php artisan migrate
```

to commit the local configuration of tables to the database. (sqlite in our case)

## Creating Chirps

Chirps are short messages here.

### Models, Migrations and Controllers

This command is used to create a "Model, Migration and Controller".

```bash
artisan make:model
```

Now let's make our Chirp files.

```bash
php artisan make:model -mrc Chirp
```

By looking at the

```bash
php artisan make:model --help
```

We could see that the -mrc option means that artisan will create a migration, a model, and a resource controller named Chirp.

## Routing

We'll be adding two routes in our app, the index route to show Chirp form and the store route to save the Chirp. Now breeze comes in hand with the Auth middleware, we'll be using it too.

to check all routes on right now, run:

```bash
php artisan route:list
```

## Routing: Inertia

Now we'll be using Inertia to render our page using Vue.js.
For better results, I recommend you to stop npm and run 'npm run dev' again.

As yout may or may not have noticed (I personally didn't at first) but our app menu doesn't have a link to our newest Chirp page, we're now going to add it.

## Chirps: Creating a relationship

We added logic to the Chirps::store method.
Do you remember that Laravel take care of the database? We'll see that in action now, on the previous step we added the line:

```php
$request->user()->chirps()
```

It's a database relationship right there. We're going to add it to the User model.

## Mass Assign Protection

It's seems that passing all data to the Model can be dangerous, when sensible data can be acessed like if we've a "is_admin" column, it'd be editable.
To prevent that we're gonna add a layer of protection.

## Migration

We added a relationship between User and Chirps and also the Chirps Model, but our database didn't receive that until now. We're gonna update our Chirps Migration class.
Now that we have our migration file updated. Let's check our class integration with the database using Laravel Tinker library.
Before all run

```bash
composer dumpautoload
```

since we added some classes and files, let's make composer update our autoloader to laraverl. After that we gonna run

```bash
php artisan tinker
```

tinker is a CLI program that we can use to interact with our laravel app via terminal. Now inside the tinker app, let's run the following command to see all Chirps stored so far:

```bash
Chirp::all();
```

## Showing Chirps

Fun fact: I probably mistyped something and ended up working for almost an hour trying to figure it out what caused my pages to return blank if everything was the same, why my Chirp page isn't showing my Chirps if everything is same? Well, I still have no idea 😁 I stashed every change I made, and then started all over again, and boom! Everything is working fine.

Within the Chirps Controller we're now using Eloquents method to retrieve data from the Database. Before we add a hasMany relantionship between User and Chirps, now we just made the opposite by adding a BelongsTo relantionship between the Chirp and the User.

Laravel may take too much time to show changes in the Front-end, it may the cause of my previous trouble, to overcome it I'm running:
```bash
npm run build
npm run dev
```


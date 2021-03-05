# Prerequisites:
The following programs are needed:
- [(XAMPP recommended)](https://www.apachefriends.org/index.html)
- php 8.0+ with xdebug extension
- [composer](https://getcomposer.org/)
- [node.js](https://nodejs.org/en/)
- [yarn](https://yarnpkg.com/getting-started/install)

## Optional
On Windows you can use my Powershell script collection.
> Note: To run ps1 scripts you need to [Allow powershell script execution](https://superuser.com/questions/106360/how-to-enable-execution-of-powershell-scripts)

- PS-Mod : https://github.com/ps-mod/ps-mod
- PS-Mod: Laravel Package: https://github.com/ps-mod/laravel

> It is recommended to log out and log back in after installing PS-Mod packages

## Install XDebug extension:
On Windows, open a new powershell, and execute this code:
```ps
php -i | clip ; Start-Process https://xdebug.org/wizard
```
This command already copied php info to your clipboard. Now paste it in the textbox, click "analyse" and follow the instructions.

On Linux or mac go to https://xdebug.org/ and follow the instructions there.

# Initialize a laravel repository
When you first clone a laravel repository you need to initialize everything
## Powershell method (Windows only):
> Note: You don't need to run your powershell as administrator

Check if your .env.example configured properly.

1. Create your database (database name should be matching the `DATABASE_NAME` defined in the `.env.example` file)
2. Open Powershell in the source folder and run `./laravel.ps1 init`. You don't have to wait its completion before continuing (in a new powershell window for example) 
3. Run `lumen vhosts reg` to register a virtual host in Apache
4. Run `lumen hosts` to open your hosts file in Visual Studio Code
5. Add the line `127.0.0.1 myapp.test` (replace *myapp* with your project name obviously) and save it. You will need admin rights for this.

Done. You can check out your app on `myapp.test` (configured by your `.env`)

## "Classic" method

1. Copy your `.env.example` file and name it to `.env`
2. Configure your `.env` per your environment
3. Create your database (database name should be matching the `DATABASE_NAME` defined in the `.env` file)
4. Open powershell / cmd / bash in the source folder and run `composer install` you don't need to wait for its completion
5. Register your virtual host: On xampp, open your vhosts (Default: `C:\xampp\apache\conf\extra\httpd-vhosts.conf` ) file and paste the following:
```apacheconf
<VirtualHost *:80>
	ServerName local.test
	DocumentRoot C:\xampp\htdocs
	SetEnv APPLICATION_ENV "development"
	<Directory C:\xampp\htdocs>
		DirectoryIndex index.php
		AllowOverride All
		Order allow,deny
		Allow from all
	</Directory>
</VirtualHost>

<VirtualHost *:80>
	ServerName myapp.test
	DocumentRoot C:\xampp\htdocs\myapp\public
	SetEnv APPLICATION_ENV "development"
	<Directory C:\xampp\htdocs\myapp\>
		DirectoryIndex index.php
		AllowOverride All
		Order allow,deny
		Allow from all
	</Directory>
</VirtualHost>
```
Change the paths and the ServerName according to your app. Your `DocumentRoot` should point to the `public` folder
6. Register your DNS to your virtual hosts: On Windows, open your hosts file (`C:\Windows\System32\drivers\etc\hosts`) and paste the following: `127.0.0.1 myapp.test` (replace *myapp* with your project name obviously) and save it. You will need admin rights for this.
7. After your composer installation is done, install the javascript packages with the command: `yarn`
8. Compile your SCSS and js files: `yarn run development`
9. Create your AppKey (this will be used by Laravel for encryption): `php artisan key:generate`
10. Run your migration and seeders: `php artisan migrate:fresh --seed`

Done. You can check out your app on myapp.test (configured by your .env)

# Creating a new Resource
In this example we have a `Product` model
1. Generate your Model with the console command `php make:model Product --all --resource`
2. Fill out your migration in `2021_03_05_110314_create_products_table.php`. The first part is the date and time of the creation
3. Create your route: in `routes/web.php` add `Route::Resource('product', ProductController::class);` don't forget to include your product controller with `use App\Http\Controllers\ProductController;` on the top of your php file
4. Fill out your controller `App\Http\Controllers\ProductController`. You can check out the [example Product controller](https://github.com/dombidav/laravel_tutorial/blob/main/app/Http/Controllers/ProductController.php) in this repository
5. Add fillable properties to Model: In the `App\Models\Product.php`:
```php
protected $fillable = ['name', 'price'];
```
6. Add views: Create a `product` folder in your `resources/views` folder, create and fill out the following files:
    - `index.blade.php`
    - `show.blade.php`
    - `create.blade.php`
    - `edit.blade.php`
> *Note: Separate Edit form is optional*
7. Write our module test in `Tests/Feature` folder
8. Run it with the command `php artisan test` or `lumen test`
9. Check your code coverage (if your test covers every function you created) with the command ` ./vendor/bin/phpunit --coverage-html tests/Coverage` then you can open your report in `tests/coverage/index.html`. Make changes if necessary
   - If you are using PS-Mod you can use the `lumen test coverage` or `lumen test c` instead

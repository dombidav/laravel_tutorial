<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/dombidav/laravel_tutorial">
   <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400">
  </a>

<h3 align="center">Laravel Crash Course</h3>

  <p align="center">
    Repository of my Laravel Crash Course
    <br />
    <a href="https://github.com/dombidav/laravel_tutorial"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/dombidav/laravel_tutorial">View Demo</a>
    ·
    <a href="https://github.com/dombidav/laravel_tutorial/issues">Report Bug</a>
    ·
    <a href="https://github.com/dombidav/laravel_tutorial/issues">Request Feature</a>
  </p>

- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
    - [Optional: PS-Mod (Windows only)](#optional-ps-mod-windows-only)
    - [2. Clone this project](#2-clone-this-project)
    - [3. Create your local environment](#3-create-your-local-environment)
    - [4. Create your database](#4-create-your-database)
    - [5. Create your virtual host:](#5-create-your-virtual-host)
      - [PS-Mod way:](#ps-mod-way)
      - [Without PS-Mod](#without-ps-mod)
    - [6. Add your app to your DNS](#6-add-your-app-to-your-dns)
      - [Windows:](#windows)
      - [Linux:](#linux)
    - [7. Set up your laravel app:](#7-set-up-your-laravel-app)
      - [PS-Mod way:](#ps-mod-way-1)
      - [Without PS-Mod:](#without-ps-mod-1)
    - [Done](#done)
- [License](#license)
- [Creating a new Resource](#creating-a-new-resource)


<!-- GETTING STARTED -->
# Getting Started

To get a local copy up and running follow these simple steps:

## Prerequisites
- [(XAMPP recommended)](https://www.apachefriends.org/index.html)
- php 8.0+ with xdebug extension
- [composer](https://getcomposer.org/)
- [node.js](https://nodejs.org/en/)
- [yarn](https://yarnpkg.com/getting-started/install)
- [Visual Studio Code](https://code.visualstudio.com/)

### Optional: PS-Mod (Windows only)
To further simplify your development, you can use my [PS-Mod](https://github.com/ps-mod/ps-mod) Powershell script collection. The PS-Mod itself DOES support almost all Linux distributions and macOS (with [Powershell7](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.1)), the Laravel package does not (yet). For this reason you can only use it on Windows for now. 

1. Open Powershell and run the following:
    ```powershell
    Set-ExecutionPolicy Bypass -Scope Process -Force ; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072 ;Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/ps-mod/ps-mod/main/install.ps1'))
    ```
   > **Windows:** If you started your powershell as Administrator, this should install `powershellmod` command for all users. If you want to install this for your user only, run powershell normally and you can safely ignore the _"Access Denied"_ errors.
   
    > **Linux or Mac:** <u>**_DO NOT_**</u> start `pwsh` with `sudo`. You can safely ignore the _"Access Denied"_ errors.
2. Start a new powershell (no admin rights needed) and run the following:
    ```powershell
   psmod require Laravel 
   ```
3. Restart your powershell
4. Test it with the command `lumen a` if you get `Could not open input file: artisan` message your _PS-Mod: Laravel_ script collection is installed successfully.

## Installation

### 1. Install XDebug
On windows, open a new powershell, and execute this code:
```powershell
php -i | clip ; Start-Process https://xdebug.org/wizard
```
This command already copied php info to your clipboard. Now paste it in the textbox, click "analyse" and follow the instructions.

On Linux or mac go to https://xdebug.org/ and follow the instructions there.

### 2. Clone this project
* Clone this repository to your server directory (ex: `C:/xampp/htdocs/`).
```sh
git clone https://github.com/dombidav/laravel_tutorial.git
```
* Open a powershell terminal here (On Windows: shift+right click > Open new Powershell terminal here).

### 3. Create your local environment
* In the source folder (ex. `C:/xampp/htdocs/laravel_tutorial/`) copy the `.env.example` file and rename it to `.env`
> Note: On Windows this can be problematic depending on your folder settings. To quickly rename it in Powershell you can use the command:
> ```powershell
> Copy-Item .env.example .env
> ```
* Now configure your `.env` accordingly to your project needs. Do not forget to set your Database name, username and password. 
> Important: the `APP_URL` variable MUST end with `.test`

### 4. Create your database
* Create a database with the name configured in `.env`.
> <small>With xampp: Start XAMPP and on the control panel start both Apache and MySQL</small>

### 5. Create your virtual host:
> If you're not using XAMPP consult the documentation of your server on how to create VHost.

#### PS-Mod way:
* Run the following:
```powershell
lumen vhosts reg
```

> You can check the content of your vhosts file with the command `lumen vhosts`

#### Without PS-Mod

* Open `xampp/apache/conf/extra/httpd-vhosts.conf` file and paste the following to the end of the file:
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
    DocumentRoot C:\xampp\htdocs\afp4\src\public
    SetEnv APPLICATION_ENV "development"
    <Directory C:\xampp\htdocs\afp4\src\>
        DirectoryIndex index.php
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>
</VirtualHost>
```

### 6. Add your app to your DNS
* Open your HOSTS file
#### Windows:
```powershell
lumen hosts

# Without PS-Mod:

code C:/Windows/System32/drivers/etc/hosts
```

#### Linux:
```bash
sudo code '/etc/hosts'
# or
sudo nano '/etc/hosts'
```
* At the end of the file add the following line <small>(Obviously replace 'myapp' with your app name)</small>:
```
127.0.0.1        myapp.test
```
* Save it. You will need Administrator rights to do this.
* Restart your (Apache) server now

### 7. Set up your laravel app:
* In your source folder run the following:
  #### PS-Mod way:
    ```powershell
    lumen compose
    ```
  #### Without PS-Mod:
    ```powershell
    composer install
    php artisan migrate:fresh --seed
    yarn
    yarn run development
    ```
  
### Done
* You can access your app at the url you have set (ex. `myapp.test`)
* You can run tests with `php artisan test` or with PS-Mod: `lumen test`

# License

Distributed under the MIT License. See `LICENSE` for more information.

---
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

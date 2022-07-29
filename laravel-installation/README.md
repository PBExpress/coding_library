# Laravel Installation

#### [Installation Via Composer](https://laravel.com/docs/9.x/installation#installation-via-composer) <a href="#installation-via-composer" id="installation-via-composer"></a>

If your computer already has PHP and Composer installed, you may create a new Laravel project by using Composer directly. After the application has been created, you may start Laravel's local development server using the Artisan CLI's `serve` command:

```
composer create-project laravel/laravel example-app 
cd example-app 
php artisan serve
```

[**The Laravel Installer**](https://laravel.com/docs/9.x/installation#the-laravel-installer)

Or, you may install the Laravel Installer as a global Composer dependency:

```
composer global require laravel/installer laravel new example-app 
cd example-app 
php artisan serve
```

Make sure to place Composer's system-wide vendor bin directory in your `$PATH` so the `laravel` executable can be located by your system. This directory exists in different locations based on your operating system; however, some common locations include:

* macOS: `$HOME/.composer/vendor/bin`
* Windows: `%USERPROFILE%\AppData\Roaming\Composer\vendor\bin`
* GNU / Linux Distributions: `$HOME/.config/composer/vendor/bin` or `$HOME/.composer/vendor/bin`

### [Meet Laravel](https://laravel.com/docs/9.x/installation#meet-laravel) <a href="#meet-laravel" id="meet-laravel"></a>

Laravel is a web application framework with expressive, elegant syntax. A web framework provides a structure and starting point for creating your application, allowing you to focus on creating something amazing while we sweat the details.

Laravel strives to provide an amazing developer experience while providing powerful features such as thorough dependency injection, an expressive database abstraction layer, queues and scheduled jobs, unit and integration testing, and more.

Whether you are new to PHP or web frameworks or have years of experience, Laravel is a framework that can grow with you. We'll help you take your first steps as a web developer or give you a boost as you take your expertise to the next level. We can't wait to see what you build.

#### [Why Laravel?](https://laravel.com/docs/9.x/installation#why-laravel) <a href="#why-laravel" id="why-laravel"></a>

There are a variety of tools and frameworks available to you when building a web application. However, we believe Laravel is the best choice for building modern, full-stack web applications.

**A Progressive Framework**

We like to call Laravel a "progressive" framework. By that, we mean that Laravel grows with you. If you're just taking your first steps into web development, Laravel's vast library of documentation, guides, and [video tutorials](https://laracasts.com/) will help you learn the ropes without becoming overwhelmed.

If you're a senior developer, Laravel gives you robust tools for [dependency injection](https://laravel.com/docs/9.x/container), [unit testing](https://laravel.com/docs/9.x/testing), [queues](https://laravel.com/docs/9.x/queues), [real-time events](https://laravel.com/docs/9.x/broadcasting), and more. Laravel is fine-tuned for building professional web applications and ready to handle enterprise work loads.

**A Scalable Framework**

Laravel is incredibly scalable. Thanks to the scaling-friendly nature of PHP and Laravel's built-in support for fast, distributed cache systems like Redis, horizontal scaling with Laravel is a breeze. In fact, Laravel applications have been easily scaled to handle hundreds of millions of requests per month.

Need extreme scaling? Platforms like [Laravel Vapor](https://vapor.laravel.com/) allow you to run your Laravel application at nearly limitless scale on AWS's latest serverless technology.

**A Community Framework**

Laravel combines the best packages in the PHP ecosystem to offer the most robust and developer friendly framework available. In addition, thousands of talented developers from around the world have [contributed to the framework](https://github.com/laravel/framework). Who knows, maybe you'll even become a Laravel contributor.

### [Your First Laravel Project](https://laravel.com/docs/9.x/installation#your-first-laravel-project) <a href="#your-first-laravel-project" id="your-first-laravel-project"></a>

We want it to be as easy as possible to get started with Laravel. There are a variety of options for developing and running a Laravel project on your own computer. While you may wish to explore these options at a later time, Laravel provides [Sail](https://laravel.com/docs/9.x/sail), a built-in solution for running your Laravel project using [Docker](https://www.docker.com/).

Docker is a tool for running applications and services in small, light-weight "containers" which do not interfere with your local computer's installed software or configuration. This means you don't have to worry about configuring or setting up complicated development tools such as web servers and databases on your personal computer. To get started, you only need to install [Docker Desktop](https://www.docker.com/products/docker-desktop).

Laravel Sail is a light-weight command-line interface for interacting with Laravel's default Docker configuration. Sail provides a great starting point for building a Laravel application using PHP, MySQL, and Redis without requiring prior Docker experience.

> Already a Docker expert? Don't worry! Everything about Sail can be customized using the `docker-compose.yml` file included with Laravel.

#### [Getting Started On macOS](https://laravel.com/docs/9.x/installation#getting-started-on-macos) <a href="#getting-started-on-macos" id="getting-started-on-macos"></a>

If you're developing on a Mac and [Docker Desktop](https://www.docker.com/products/docker-desktop) is already installed, you can use a simple terminal command to create a new Laravel project. For example, to create a new Laravel application in a directory named "example-app", you may run the following command in your terminal:

```
curl -s "https://laravel.build/example-app" | bash
```

Of course, you can change "example-app" in this URL to anything you like - just make sure the application name only contains alpha-numeric characters, dashes, and underscores. The Laravel application's directory will be created within the directory you execute the command from.

After the project has been created, you can navigate to the application directory and start Laravel Sail. Laravel Sail provides a simple command-line interface for interacting with Laravel's default Docker configuration:

```
cd example-app ./vendor/bin/sail up
```

The first time you run the Sail `up` command, Sail's application containers will be built on your machine. This could take several minutes. **Don't worry, subsequent attempts to start Sail will be much faster.**

Once the application's Docker containers have been started, you can access the application in your web browser at: [http://localhost](http://localhost/).

> To continue learning more about Laravel Sail, review its [complete documentation](https://laravel.com/docs/9.x/sail).

#### [Getting Started On Windows](https://laravel.com/docs/9.x/installation#getting-started-on-windows) <a href="#getting-started-on-windows" id="getting-started-on-windows"></a>

Before we create a new Laravel application on your Windows machine, make sure to install [Docker Desktop](https://www.docker.com/products/docker-desktop). Next, you should ensure that Windows Subsystem for Linux 2 (WSL2) is installed and enabled. WSL allows you to run Linux binary executables natively on Windows 10. Information on how to install and enable WSL2 can be found within Microsoft's [developer environment documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

> After installing and enabling WSL2, you should ensure that Docker Desktop is [configured to use the WSL2 backend](https://docs.docker.com/docker-for-windows/wsl/).

Next, you are ready to create your first Laravel project. Launch [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?rtc=1\&activetab=pivot:overviewtab) and begin a new terminal session for your WSL2 Linux operating system. Next, you can use a simple terminal command to create a new Laravel project. For example, to create a new Laravel application in a directory named "example-app", you may run the following command in your terminal:

```
curl -s https://laravel.build/example-app | bash
```

Of course, you can change "example-app" in this URL to anything you like - just make sure the application name only contains alpha-numeric characters, dashes, and underscores. The Laravel application's directory will be created within the directory you execute the command from.

After the project has been created, you can navigate to the application directory and start Laravel Sail. Laravel Sail provides a simple command-line interface for interacting with Laravel's default Docker configuration:

```
cd example-app ./vendor/bin/sail up
```

The first time you run the Sail `up` command, Sail's application containers will be built on your machine. This could take several minutes. **Don't worry, subsequent attempts to start Sail will be much faster.**

Once the application's Docker containers have been started, you can access the application in your web browser at: [http://localhost](http://localhost/).

> To continue learning more about Laravel Sail, review its [complete documentation](https://laravel.com/docs/9.x/sail).

**Developing Within WSL2**

Of course, you will need to be able to modify the Laravel application files that were created within your WSL2 installation. To accomplish this, we recommend using Microsoft's [Visual Studio Code](https://code.visualstudio.com/) editor and their first-party extension for [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack).

Once these tools are installed, you may open any Laravel project by executing the `code .` command from your application's root directory using Windows Terminal.

#### [Getting Started On Linux](https://laravel.com/docs/9.x/installation#getting-started-on-linux) <a href="#getting-started-on-linux" id="getting-started-on-linux"></a>

If you're developing on Linux and [Docker Compose](https://docs.docker.com/compose/install/) is already installed, you can use a simple terminal command to create a new Laravel project. For example, to create a new Laravel application in a directory named "example-app", you may run the following command in your terminal:

```
curl -s https://laravel.build/example-app | bash
```

Of course, you can change "example-app" in this URL to anything you like - just make sure the application name only contains alpha-numeric characters, dashes, and underscores. The Laravel application's directory will be created within the directory you execute the command from.

After the project has been created, you can navigate to the application directory and start Laravel Sail. Laravel Sail provides a simple command-line interface for interacting with Laravel's default Docker configuration:

```
cd example-app ./vendor/bin/sail up
```

The first time you run the Sail `up` command, Sail's application containers will be built on your machine. This could take several minutes. **Don't worry, subsequent attempts to start Sail will be much faster.**

Once the application's Docker containers have been started, you can access the application in your web browser at: [http://localhost](http://localhost/).

> To continue learning more about Laravel Sail, review its [complete documentation](https://laravel.com/docs/9.x/sail).

#### [Choosing Your Sail Services](https://laravel.com/docs/9.x/installation#choosing-your-sail-services) <a href="#choosing-your-sail-services" id="choosing-your-sail-services"></a>

When creating a new Laravel application via Sail, you may use the `with` query string variable to choose which services should be configured in your new application's `docker-compose.yml` file. Available services include `mysql`, `pgsql`, `mariadb`, `redis`, `memcached`, `meilisearch`, `minio`, `selenium`, and `mailhog`:

```
curl -s "https://laravel.build/example-app?with=mysql,redis" | bash
```

If you do not specify which services you would like configured, a default stack of `mysql`, `redis`, `meilisearch`, `mailhog`, and `selenium` will be configured.

You may instruct Sail to install a default [Devcontainer](https://laravel.com/docs/9.x/sail#using-devcontainers) by adding the `devcontainer` parameter to the URL:

```
curl -s "https://laravel.build/example-app?with=mysql,redis&devcontainer" | bash
```

For convenience, the Laravel installer can also create a Git repository for your new project. To indicate that you want a Git repository to be created, pass the `--git` flag when creating a new project:

```
laravel new example-app --git
```

This command will initialize a new Git repository for your project and automatically commit the base Laravel skeleton. The `git` flag assumes you have properly installed and configured Git. You can also use the `--branch` flag to set the initial branch name:

```
laravel new example-app --git --branch="main"
```

Instead of using the `--git` flag, you may also use the `--github` flag to create a Git repository and also create a corresponding private repository on GitHub:

```
laravel new example-app --github
```

The created repository will then be available at `https://github.com/<your-account>/example-app`. The `github` flag assumes you have properly installed the [GitHub CLI](https://cli.github.com/) and are authenticated with GitHub. Additionally, you should have `git` installed and properly configured. If needed, you can pass additional flags that are supported by the GitHub CLI:

```
laravel new example-app --github="--public"
```

You may use the `--organization` flag to create the repository under a specific GitHub organization:

```
laravel new example-app --github="--public" --organization="laravel"
```

### [Initial Configuration](https://laravel.com/docs/9.x/installation#initial-configuration) <a href="#initial-configuration" id="initial-configuration"></a>

All of the configuration files for the Laravel framework are stored in the `config` directory. Each option is documented, so feel free to look through the files and get familiar with the options available to you.

Laravel needs almost no additional configuration out of the box. You are free to get started developing! However, you may wish to review the `config/app.php` file and its documentation. It contains several options such as `timezone` and `locale` that you may wish to change according to your application.

#### [Environment Based Configuration](https://laravel.com/docs/9.x/installation#environment-based-configuration) <a href="#environment-based-configuration" id="environment-based-configuration"></a>

Since many of Laravel's configuration option values may vary depending on whether your application is running on your local computer or on a production web server, many important configuration values are defined using the `.env` file that exists at the root of your application.

Your `.env` file should not be committed to your application's source control, since each developer / server using your application could require a different environment configuration. Furthermore, this would be a security risk in the event an intruder gains access to your source control repository, since any sensitive credentials would get exposed.

> For more information about the `.env` file and environment based configuration, check out the full [configuration documentation](https://laravel.com/docs/9.x/configuration#environment-configuration).

#### [Directory Configuration](https://laravel.com/docs/9.x/installation#directory-configuration) <a href="#directory-configuration" id="directory-configuration"></a>

Laravel should always be served out of the root of the "web directory" configured for your web server. You should not attempt to serve a Laravel application out of a subdirectory of the "web directory". Attempting to do so could expose sensitive files that exist within your application.

### [Next Steps](https://laravel.com/docs/9.x/installation#next-steps) <a href="#next-steps" id="next-steps"></a>

Now that you have created your Laravel project, you may be wondering what to learn next. First, we strongly recommend becoming familiar with how Laravel works by reading the following documentation:

* [Request Lifecycle](https://laravel.com/docs/9.x/lifecycle)
* [Configuration](https://laravel.com/docs/9.x/configuration)
* [Directory Structure](https://laravel.com/docs/9.x/structure)
* [Service Container](https://laravel.com/docs/9.x/container)
* [Facades](https://laravel.com/docs/9.x/facades)

How you want to use Laravel will also dictate the next steps on your journey. There are a variety of ways to use Laravel, and we'll explore two primary use cases for the framework below.

#### [Laravel The Full Stack Framework](https://laravel.com/docs/9.x/installation#laravel-the-fullstack-framework) <a href="#laravel-the-fullstack-framework" id="laravel-the-fullstack-framework"></a>

Laravel may serve as a full stack framework. By "full stack" framework we mean that you are going to use Laravel to route requests to your application and render your frontend via [Blade templates](https://laravel.com/docs/9.x/blade) or using a single-page application hybrid technology like [Inertia.js](https://inertiajs.com/). This is the most common way to use the Laravel framework.

If this is how you plan to use Laravel, you may want to check out our documentation on [routing](https://laravel.com/docs/9.x/routing), [views](https://laravel.com/docs/9.x/views), or the [Eloquent ORM](https://laravel.com/docs/9.x/eloquent). In addition, you might be interested in learning about community packages like [Livewire](https://laravel-livewire.com/) and [Inertia.js](https://inertiajs.com/). These packages allow you to use Laravel as a full-stack framework while enjoying many of the UI benefits provided by single-page JavaScript applications.

If you are using Laravel as a full stack framework, we also strongly encourage you to learn how to compile your application's CSS and JavaScript using [Laravel Mix](https://laravel.com/docs/9.x/mix).

> If you want to get a head start building your application, check out one of our official [application starter kits](https://laravel.com/docs/9.x/starter-kits).

#### [Laravel The API Backend](https://laravel.com/docs/9.x/installation#laravel-the-api-backend) <a href="#laravel-the-api-backend" id="laravel-the-api-backend"></a>

Laravel may also serve as an API backend to a JavaScript single-page application or mobile application. For example, you might use Laravel as an API backend for your [Next.js](https://nextjs.org/) application. In this context, you may use Laravel to provide [authentication](https://laravel.com/docs/9.x/sanctum) and data storage / retrieval for your application, while also taking advantage of Laravel's powerful services such as queues, emails, notifications, and more.

If this is how you plan to use Laravel, you may want to check out our documentation on [routing](https://laravel.com/docs/9.x/routing), [Laravel Sanctum](https://laravel.com/docs/9.x/sanctum), and the [Eloquent ORM](https://laravel.com/docs/9.x/eloquent).

> Need a head start scaffolding your Laravel backend and Next.js frontend? Laravel Breeze offers an [API stack](https://laravel.com/docs/9.x/starter-kits#breeze-and-next) as well as a [Next.js frontend implementation](https://github.com/laravel/breeze-next) so you can get started in minutes.

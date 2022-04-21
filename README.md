# LARAVEL_REQUEST_LIFE_CYCLE!
AUTO LOADER
-------------------

As a first step, the request will be triggered from the user’s browser, then it will reach web server. Web server (Apache or Nginx) will redirect the given request to Laravel public/index.php file which is simply a starting point for loading the rest of the framework. It loads the auto loader files which is generated by composer.

Then it retrieves an instance of the Laravel application from bootstrap/app.php script. Laravel itself creates an instance of the application, is the initial/first step.

KERNEL
----------
Next step will occur on the Kernel part of the application.

The incoming request is sent to either the HTTP kernel or the console kernel, depending on the type of request that is entering the application .These two kernels serve as the central location that all requests flow through.

HTTP kernel, which is placed in app/Http/Kernel.php. It just receive a Request and return a Response. Bootstrappers that are defined by the Kernel class, which configures error handling, configure logging, detect environments and other tasks to be done before the request handled.

HTTP Kernel will define the list of middleware that are passed through before handled by application.

SERVICE PROVIDERS
------------------------

Next step of the kernel is to load service providers as part of the bootstrapping action. Providers that are needed for the application are placed in config/app.php configuration file.

While the register method calls, all the providers will be registered. Once all providers are registered, then boot method will be called.

DISPATCH REQUEST
-------------------------

Once the application have been bootstrapped and all service providers are registered and booted, the request will be handed over to the router for dispatching. The router will dispatch the request to a route or controller, as well as run any route specific middleware.

ROUTER
--------------

Now request will be dispatched by the Router and it will end up with the views as shown below:

Router will direct the HTTP Request to a Controller or return a view or responses directly by omitting the controller. These routes will be placed in app/routes.php.

Controller app/controllers/ performs specific actions and sends data to a View.

View app/views/ formats the data appropriately, providing the HTTP Response.


[Laravel request life cycle image ](https://user-images.githubusercontent.com/78947251/164401853-7f767019-82ee-4189-a1c6-2633cb758476.png)
Let’s see an example for a request

STEP 1

The user input http:// xyz.com in the browser and hits ‘enter’.

STEP 2

Once the user hit this URL, the browser will send the page request over the Internet to the web server.

STEP 3

Web server will receive the request and analyze the request information. In web server’s configuration file, site’s root path is specified. Based on that, web server will look for index.php file in that root directory, since URL doesn’t contain any sub directory or any other routes.

STEP 4

Web server will direct the request to public/index.php file of laravel application.

STEP 5

In this step, PHP Interpreter is executing the code contained in the index.php file from the request. During this step, auto loader files which are generated by composer will be loaded.

STEP 6

Then it will create the laravel instance and bootstrapping the components of laravel.

STEP 7

The kernel will receive the request, load the service providers and will be redirected to router.

STEP 8

Router will render the view file content and return back to web server.

STEP 9

Web server receives the output from PHP and sends it back over the Internet to a user’s web browser.

STEP 10

The user’s web browser receives the response from the server, and renders the web page on user’s computer.



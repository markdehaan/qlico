# Debugging with Xdebug

## What is Xdebug?

Xdebug is an extension for PHP, and provides a range of features to improve the PHP development experience.

### Step Debugging

A way to step through your code in your IDE or editor while the script is executing.


### Improvements to PHP's error reporting

An improved [var_dump()](https://xdebug.org/docs/develop#display){:target="_blank"} function, stack traces for Notices, Warnings, Errors and Exceptions to highlight the code path to the error.


## Configure Qlico in your project to use Xdebug

Qlico in "dev" stage (default) supports debugging using [Xdebug](https://xdebug.org/){:target="_blank"}.
You can check if it's enabled with `phpinfo();`
![phpinfo](/assets/img/xdebug/phpinfo.png "phpinfo")

Make sure that in your `qlico/.env` file the following values are filled:

`PROJECT_NAME=unique-project-name` this should be an unique project name, if you
have multiple projects with the same name (for example `api` and `frontend`)
name your projects: `project-api` and `project-frontend`. If these names are not
unique, you will not be able to debug multiple projects at the same time.

`XDEBUG_MODE=develop,debug` this setting controls which Xdebug features are
enabled.
[More information about the different modes](https://xdebug.org/docs/all_settings#mode){:target="_blank"}

`XDEBUG_CLIENT_HOST` for macOS users this should be: `host.docker.internal`

If you're running Linux, you can run and copy the output:

```shell
ip addr show docker0 | grep "inet\b" | awk '{print $2}' | cut -d/ -f1
```

For example:
`XDEBUG_CLIENT_HOST=172.17.0.1`

### Full working example of `.env` file

```env title=".env"
PROJECT_NAME=xdebug-example
XDEBUG_MODE=develop,debug
XDEBUG_CLIENT_HOST=host.docker.internal
```

## Configure your IDE

* [PhpStorm](#phpstorm)
* [Visual Studio Code](#visual-studio-code)


### PhpStorm

These instructions also work for IntelliJ IDEA.

#### Open the Project settings and go to: `PHP` -> `Debug`, make sure that the Debug port is: `9003,9000`

![phpstorm-php-debug](/assets/img/xdebug/phpstorm-php-debug.png "phpstorm-php-debug")

#### Next to go: PHP -> Servers<br>

**Name:** `xdebug-example` _Important:_ This name MUST match the `PROJECT_NAME`
in your `.env` file.<br>
**Host:** `localhost`<br>
**Check:** "Use path mappings (select if the server is remote or symlinks are
used)", since we're using a "remote" Docker container.<br>
**Absolute path on the server:** `/var/www/html`<br>

![phpstorm-servers-localhost](/assets/img/xdebug/phpstorm-servers-localhost.png "phpstorm-servers-localhost")

#### Click: "Start listening for PHP Debug Connections" (in the Main toolbar)
![phpstorm-start-listening](/assets/img/xdebug/phpstorm-start-listening.png "phpstorm-start-listening")

After you've clicked the button, the "red" light should be "green"<br>
![phpstorm-is-listening](/assets/img/xdebug/phpstorm-is-listening.png "phpstorm-is-listening")

#### Set a breakpoint somewhere in your code
![phpstorm-add-breakpoint](/assets/img/xdebug/phpstorm-add-breakpoint.png "phpstorm-add-breakpoint")

[For more information about breakpoints in PhpStorm, click here.](https://www.jetbrains.com/help/phpstorm/using-breakpoints.html){:target="_blank"}

#### Open your project in a browser
In my example: Visiting `http://xdebug-example.qlico`

#### Profit
PhpStorm will automatically open up, with Debug information
![phpstorm-debug-screen](/assets/img/xdebug/phpstorm-debug-screen.png "phpstorm-debug-screen")

As you can see at the bottom of the screen: There is a debugger attached.

#### More information about using Debugging in PhpStorm

- [Debug tool window](https://www.jetbrains.com/help/phpstorm/debug-tool-window.html){:target="_blank"}
- [Step through the program](https://www.jetbrains.com/help/phpstorm/stepping-through-the-program.html){:target="_blank"}


### Visual Studio Code

To enable debugging in Visual Studio Code, please install
the [PHP Debug plugin by Xdebug](https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug){:target="_blank"}
first.

A small note on the plugin: This plugin does not support multiple debugging
sessions at the same time.
See this GitHub issue for more information:
[Multiple debugging sessions](https://github.com/xdebug/vscode-php-debug/issues/522){:target="_blank"}

After installation, in your project open: `.vscode/launch.json`

And add the following snippet:

```json title=".vscode/launch.json"
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "hostname": "0.0.0.0",
            "port": 9003,
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}"
            }
        }
    ]
}
```

#### How to start a debug session

#### Go to Run: "Start debugging"

#### Add a breakpoint in VSCode
![vscode-add-breakpoint](/assets/img/xdebug/vscode-add-breakpoint.png "vscode-add-breakpoint")

#### Open your project in a browser
In my example: Visiting `http://xdebug-example.qlico`

#### Profit
In Visual Studio Code
![vscode-debug-screen](/assets/img/xdebug/vscode-debug-screen.png "vscode-debug-screen")

As you can see at the left of the screen: There is a debugger attached.

## Debugging CLI scripts

If you want to debug a CLI PHP Script, please use the alias: `xphp` inside the running PHP Container

For example:

```shell
docker compose exec php ash
```

```shell
xphp index.php
```
This is also possible with Symfony and Laravel commands.
```shell
# Symfony
xphp bin/console app:command

# Laravel
xphp artisan app:command
```

It's the same process for [PhpStorm](#phpstorm)
and [Visual Studio Code](#visual-studio-code), make sure to set it up first.
Now PhpStorm or Visual Studio Code will open. By default, the `php` alias inside
Qlico do not have Xdebug enabled, because this can give side effects, for
example when running `composer install`.

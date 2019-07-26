# Requisites

- [NodeJS](https://nodejs.org/)
- [composer](https://getcomposer.org/)
- [wordup-cli](https://github.com/wordup-dev/wordup-cli)

# Optional

There is no need to use the awps-cli. But you can!

1. If you have awps in your system PATH, just run `npm run new:awps`
2. Then change your .env or wp-config.php files on the root of the project.
**NOTE:** Order is important!!! awps-cli replaces the original .env file of this repo so make sure to change it after you run awps-cli
3. Finnaly make sure to run `npm run update:wp` after.

# Usage

1. Clone this repository

```bash
git clone https://github.com/gpedro34/wordup-awps.git YOUR-PROJECT-NAME-HERE
```

2. Go into YOUR-PROJECT-NAME-HERE/.wordup/ and change your configurations. [Refer to Wordup documentation](https://docs.wordup.dev/config)
3. Next you need to change your .env file inside YOUR-PROJECT-NAME-HERE folder and verify wp-options.php
4. Then open package.json in the YOUR-PROJECT-NAME-HERE folder and edit all instances of "YOUR-PROJECT-NAME-HERE" and "your-project-name-here" by the name of your project (use dashes) and "YOUR_THEME_NAME_HERE" by your theme name (do not use dashes)
5. Once everything is configured properly, run `npm run new:git` and grab a coffee while the engines fire!  
**NOTE:** You may be prompt for sudo password at the end in order to access the docker volume and inject .env and wp-config.php into the running docker environment

The above command should have:

- Setup the docker containers (WP, wp-cli, mysql)
- Setup a new theme called YOUR_THEME_NAME_HERE inside YOUR-PROJECT-NAME-HERE/src/themes/
- Remove the .env.sample, wp-options-sample.php and reinitialized git for the new theme
- Installed composer modules
- Installed npm modules
- Copy wp-config.php and .env to the root of your wordpress installation (sudo command)

# Considerations

## docker-compose

A docker-compose.yml at the root of your project extends the base wordup stack which already consists in:

- Wordpress container
- MySQL DB container
- wp-cli container

The base docker-compose file in this project is extending that stack with the PHPMyAdmin container although it's named d-c.yml so it doesn't get triggered automatically, so make sure to modify it's name to docker-compose.yml if you intend to run PHPMyAdmin automatically at wordup startup.

## PHPMyAdmin

If you need PHPMyAdmin at any point in time just run:

```bash
npm run d-c:up
```

Once you don't need it anymore you can save resources by running:

```bash
npm run d-c:down
```

## Webpack

AWPS uses [Laravel Mix](https://laravel.com/docs/5.6/mix) for assets management. Check the official documentation for advanced options

- Edit the `webpack.mix.js` in the root directory of your theme to set your localhost URL and customize your assets
- `npm run watch` to start browserSync with LiveReload and proxy to your custom URL
- `npm run dev` to quickly compile and bundle all the assets without watching
- `npm run prod` to compile the assets for production

## Copying files to outside of wp-content

### Linux

As the wordpress container wordup launches already a volume called "your-project-name-here_wp_data" that we can inject the files to:

```bash
sudo cp .env /var/lib/docker/volumes/your-project-name-here_wp_data/_data/.env
sudo cp wp-config.php /var/lib/docker/volumes/your-project-name-here_wp_data/_data/wp-config.php
```

For convenience there is a npm script to handle this.

```bash
npm run up-config
```

[See answer 2 and 3](https://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container)

### Windows and Mac

May have to fallback to something in the lines of the [4th or 5th answers](https://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container)
Or maybe use a bind mount to the running wordpress container and then execute a copy command to /var/www/html/.

## Features

### [AWPS theme](https://github.com/Alecaddd/awps)

- Bult-in `webpack.mix.js` for fast development and compiling.
- `OOP` PHP, and `namespaces` with `PSR4` autoload.
- `Customizer` ready with boilerplate and example classes.
- `Gutenberg` ready with boilerplate and example blocks.
- `ES6 Javascript` syntax ready.
- Compatible with `JetPack`, `WooCommerce`, `ACF PRO`, and all the most famous plugins.
- Built-in `FlexBox` Responsive Grid.
- Modular, Components based file structure.
- [Video series explanation of the workflows and structure (a bit outdated) as well as examples](https://www.youtube.com/watch?v=IIJyvjYzpXA&list=PLriKzYyLb28kvx7IVw2sAXtZ2yN4A1otJ&index=2)

### [Wordup](https://github.com/wordup-dev/wordup-cli)

- 💡**Rapidly test new ideas** - And develop your new WordPress theme/plugin projects in wordup.
- ⏱**Speed up your development** - Install a new project with a blank WordPress installation in a matter of minutes
- 🛠️**Boilerplate** - Scaffold your theme/plugin with the official source code from WordPress (e.g. [underscore](https://github.com/automattic/_s)). You can also add code snippets like _Gutenberg_ blocks to your source code.
- ⚙️**Automatic installation of dependencies** - Automatically download and activate public WordPress Plugins/Themes or even Github hosted projects (like e.g. [wp-graphql](https://github.com/wp-graphql/wp-graphql))
- 📚**Fixtures** - Add posts, pages, media files and many more automatically to your WordPress installation and develop immediately with your own page structure
- 🚀**Easy portability** - Export your theme/project or your whole WordPress installation. So that you can install it on a remote server.
- 📦**Backup your installation** - And (re)install a project from an exported wordup project.
- 🤩**Hassle-free remote WordPress connection** - Install your project, based on an existing WordPress hosted website (with the [wordup-connect](https://github.com/wordup-dev/wordup-connect) plugin). Use this feature for example to test major WordPress updates with ease locally.
- 👾**Share your stack** - wordup is the easiest way to share your WordPress project with the world or just your team members. Just type: `git clone`, and then `wordup install`
- ✉️**Catch emails** - Catch all emails from WordPress and view the outgoing emails in a web UI
- [VSCode Extension](https://github.com/wordup-dev/wordup-code)

### This repository

- Combines all of the above in a simple npm package in order to automate the creation of wordpress theme boilerplates using the wordup development environment built on top of Docker and VSCode.

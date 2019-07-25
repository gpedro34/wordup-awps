# docker-compose

The docker-compose.yml at the root extends the base wordup stack which already consists in:

- Wordpress container
- MySQL DB container
- wp-cli container

The base docker compose in this project is extending that stack with the PHPMyAdmin container

# Copying files to outside of wp-content

## Linux

As the wordpress container wordup launches already a volume called YOUR_PROJECT_NAME-wp_data we can use:

```bash
sudo cp ./wp-config/.env /var/lib/docker/volumes/test-installation_wp_data/_data/.env
sudo cp ./wp-config/wp-config.php /var/lib/docker/volumes/test-installation_wp_data/_data/wp-config.php
```

to access replace the files.

For convenience there is a npm script to handle this but ATM does not use environment variables so you will have to replace your project name manually inside the package.json file.

```bash
npm run up-config
```

[See answer 2 and 3](https://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container)

Windows and Mac users may have to fallback to something in the lines of the [4th or 5th answers](https://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container)

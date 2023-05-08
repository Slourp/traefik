
# GitLab Deployment 🚀

This is a GitLab deployment using Docker and Traefik as a reverse proxy. 🐳 ⚙️

## Prerequisites 📋

Before running this deployment, you need to have the following:

- Docker and Docker Compose installed on your machine. 💻
- A domain name with a valid SSL certificate. 🔒
- A registration token for GitLab Runner. 🏃‍♂️

## Configuration 🔧

To configure this deployment, you need to do the following:

1. Clone this repository to your local machine. 🐙

2. Create a file called `.env` in the root directory of the repository and set the following environment variables: 📄

```
PROJECT_NAME=<your project name>
DOMAIN=<your domain name>
NETWORK_NAME=<your network name>
REGISTRATION_TOKEN=<your GitLab Runner registration token>
```

3. Modify the `docker-compose.yml` file to suit your needs. You can change the GitLab version, port mappings, environment variables, and other settings.

4. Run the following command to start the GitLab deployment: 🚀

```
docker-compose up -d
```

## Registering the GitLab Runner 🏃‍♂️

In order to use the GitLab Runner with our GitLab instance, we need to register it. To register the Runner, follow these steps:

1. Make sure that the GitLab Runner service is running by running the following command:

   ```
   docker-compose up -d runner
   ```

2. Once the Runner service is up and running, you can obtain the registration token from the GitLab web interface under `Settings > CI/CD > Runners`.

3. Run the following command to register the Runner:

   ```
   docker-compose run --rm runner gitlab-runner register \
     --non-interactive \
     --url http://gitlab:8929/ \
     --registration-token ${REGISTRATION_TOKEN} \
     --executor docker \
     --docker-image docker:stable \
     --description "Docker Runner" \
     --tag-list "docker,linux,xenial"
   ```

4. Once the Runner is registered, you can start using it to run your CI/CD jobs.

   Note that the Runner is automatically registered with the GitLab server when the `docker-compose up` command is run, but you may need to manually register it if you have made changes to the `docker-compose.yml` file or if the Runner is not registered for some other reason.

## Usage 📝

Once the GitLab deployment is up and running, you can access the GitLab web interface at `https://<your domain name>/`. You can log in with the default administrator account:

- Username: `root`
- Password: `5iveL!fe`

You can also create new user accounts and projects from the web interface. GitLab Runner is automatically registered with the GitLab server and can be used to run CI/CD jobs.

## Maintenance 🛠️

To stop and remove the GitLab deployment, run the following command:

```
docker-compose down
```

To backup and restore the GitLab data, you can use the `gitlab-backup` and `gitlab-restore` commands.

```
docker-compose exec gitlab gitlab-backup create
```

This will create a backup of the GitLab data in the `./volumes/gitlab-data/backups` directory.

To restore the GitLab data from a backup, run the following command:

```
docker-compose exec gitlab gitlab-backup restore BACKUP=YYYY-MM-DD
```

Replace `YYYY-MM-DD` with the date of the backup that you want to restore.

## Need Help? Contact the Developer! 🤝

If you have any questions, issues, or feature requests, feel free to contact the developer of this project.

- Name: David .V
- Email: davidvanmak+github@gmail.com
- GitHub: https://github.com/Slourp/

I'm always happy to help! 😊
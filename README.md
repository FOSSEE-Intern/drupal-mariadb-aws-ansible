# Setup:

## EC2 instance for jenkins:
- Install `jenkins` and it's dependencies.
- Create new `freestyle project`, add your `git repo`.
- Add a build step, Execute shell:
    -   ```shell
        source path/to/your/env
        ansible-playbook path/to/your/playbook
        ```
- Make sure to add `AWS_ACCESSKEY_ID` and `AWS_SECRET_ACCESS_KEY` as environment variables for the ansible inventory to work.

## In your github repo:
- Repository settings > Webhooks > Add webhook
- Payload URL: `http://<jenkins_urls>/github-webhook`

## Ansible playbooks:
- There are three playbooks here:
    - ec2.create.yml
    - rds.create.yml
    - deploy.yml
- ec2.create.yml: creates an EC2 instance for the website to be deployed.
- rds.create.yml: creates a RDS instance for the EC2 instance.
- deploy.yml:
    - This ensures the dependencies like php, php-fpm, php-gd, php-mysqlnd, nginx and git are installed on the system.
    - Installs composer on the system.
    - Ensures the drupal directory is present and creates a durpal project
    - Installs drupal modules required for the website.
    - Initializes the drupal website using drush.
    - Creates `nginx.conf` from the template.
    - Starts or restarts nginx and php-fpm in the end.

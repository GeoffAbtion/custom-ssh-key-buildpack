# Heroku Buildpack: Custom SSH key

Use *Custom SSH key buildpack* if you need to, for example, download a dependency stored in a private repository.

Based on [http://stackoverflow.com/a/29677091/3303182](http://stackoverflow.com/a/29677091/3303182).

## Usage

- Add the buildpack to your app:
  `Heroku buildpacks:add --index 1 https://github.com/abtion/custom-ssh-key-buildpack --app fguplaner-backend-ci`

- Generate a new SSH key (https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

  For this example I will suppose that you named the key `deploy_key`.

- Add the ssh key as a deploy key to the private repository

  * Github: https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys

- Encode the private key as a base64 string and add it as the `IPUNG_SSH_KEY` environment variable of the Heroku app.
- Encode the private key as a base64 string and add it as the `COSA_SSH_KEY` environment variable of the Heroku app.

## Add the deploy key to Heroku configuration
  ```
  # OSX
  $ Heroku config:set IPUNG_SSH_KEY=$(base64 --input nordplaner_ipung_deploy_key.rsa) --app fguplaner-backend-ci
  $ Heroku config:set COSA_SSH_KEY=$(base64 --input nordplaner_cosa_deploy_key.rsa) --app fguplaner-backend-ci

  ```

- Deploy your app and enjoy :)

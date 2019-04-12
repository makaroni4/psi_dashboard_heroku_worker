# PSI Dashboard Heroku Scheduler

This is a Ruby worker that fetches PageSpeed Insights data daily (via Heroku Scheduler) and pushes results to your Github repo with PSI Dashboard.

# Installation

1. Add `PSI_URLS` ENV variable to Heroku app with a comma separated list of URLS: `https://www.foo.bar,https://www.bar.foo`

2. Since Heroku worker will push to our Github repo with dashboard we'd need to generate SSH key pair and add private key to Heroku and add a public key to a Github repo as a deploy key with read & write access.

3. Let's create a heroku app by running `heroku create`

4. Let's add a Heroku buildback which allows us to add the private SSH key: `heroku buildpacks:set --index 1 https://github.com/debitoor/ssh-private-key-buildpack.git`

5. Go to app settings on Heroku and add private SSH key as `SSH_KEY` Environment Variable

6. Coffee break. We're almost there! :coffee:


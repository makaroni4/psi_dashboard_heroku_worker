# PSI Dashboard Heroku Scheduler

This is a Ruby worker that fetches PageSpeed Insights data daily (via Heroku Scheduler) and pushes results to your Github repo with PSI Dashboard.

# Installation

1. Since Heroku worker will push to our Github repo with dashboard we'd need to generate SSH key pair and add private key to Heroku and add a public key to a Github repo as a deploy key with read & write access.

2. Create a Heroku app:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/makaroni4/psi_dashboard_heroku_worker&env[GITHUB_USER_NAME]&env[GITHUB_USER_EMAIL]&env[PSI_DASHBOARD_GITHUB_REPO]&env[PSI_DASHBOARD_FOLDER]&env[PSI_URLS]&env[SSH_KEY])

Make sure to add all Environment variables:

* **GITHUB_USER_NAME** is your Github username
* **GITHUB_USER_EMAIL** is your Github email

* **PSI_DASHBOARD_GITHUB_REPO** is a git URL of your PSI dashboard repo, like `git@github.com:USERNAME/page-speed-insight-dashboard.git`
* **PSI_DASHBOARD_FOLDER** is a project folder, `page-speed-insight-dashboard`

* **PSI_URLS** is a comma separated list of URLS: `https://www.foo.bar,https://www.bar.foo`

* **SSH_KEY** is a private SSH key you've generated in step 1.

3. Coffee break. We're almost there! :coffee:

4. Let's add a Heroku buildback which allows us to add the private SSH key: `heroku buildpacks:set --index 1 https://github.com/debitoor/ssh-private-key-buildpack.git`

5. Go to `Overview` -> `Configure Add-ons` and add `Heroku Scheduler`. You need to set up a job `bin/fetch_data` to run every day.

6. You're all set up! To make sure everything works correctly open `More` menu, select `Run Console` and run `bin/fetch_data` command. You should see the output that the data for all URLs was fetched and successfully uplodaded to a Github repo.

:beers:

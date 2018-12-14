The `/alertcsst` command hook
=========================

A simple webhook to relay an `/alertcsst` command to a private slack room for the Code4Lib Community Safety and Support Team. This is a slightly modified version of lgbtq.technology's [`admin-command`](https://github.com/lgbtq-technology/admin-command).

Installation
------------

0. clone this repository.
1. Install node 4.x or greater
2. Run `npm install`
3. Set up an incoming webhook in slack that sends to your admin channel. Take note of its url.
4. Set up a slack slash command to send to http://yourserver:portnumber/
5. Start the app with `PORT=8080 INTEGRATION_TOKEN=slackintegrationtoken WEBHOOK_URL=yourhookurl PHONE_NUMBER=mobilephone CONDUCT_LINK=https://xxx npm start` and check for errors.
6. Add it to your system startup scripts, or a cron @reboot rule: `@reboot cd /path/to/repo; PORT=8080 INTEGRATION_TOKEN=slackintegrationtoken WEBHOOK_URL=yourhookurl PHONE_NUMBER=mobilephone CONDUCT_LINK=https://xxx npm start`

How to run with docker
------------

0. Install docker if your machine does not have it already (https://docs.docker.com/engine/installation/)
1. Build the docker image with `docker build -t admin-command .`
2. Start the container with `docker run --name slack-admin-command -e PORT=8080 -e INTEGRATION_TOKEN=slackintegrationtoken -e WEBHOOK_URL=yourhookurl PHONE_NUMBER=8005551212 CONDUCT_LINK=https://example.com/ admin-command`
3. Check for logs/ errors with `docker logs slack-admin-command`.
4. Use [docker restart policies](https://docs.docker.com/engine/reference/run/#restart-policies-restart) to keep it running.

How to run with Heroku
------------

0. clone this repository
1. Create a heroku app:  `heroku create appname`
2. Set your config variables: `heroku config:set PORT=8080 INTEGRATION_TOKEN=slackintegrationtoken WEBHOOK_URL=yourhookurl PHONE_NUMBER=8675309 CONDUCT_LINK=https://yyy`
3. deploy to heroku: `git push heroku master`

Note that incoming requests using `/alertcsst` are also logged in the Heroku logs.

Configuration variable reference
------------

* `PORT`: the port on which to allow incoming connections for the webhook server
* `INTEGRATION_TOKEN`: a Slack integration token
* `WEBHOOK_URL`: A Slack incoming webhook URL which is used to create the notification
* `PHONE_NUMBER`: a phone number for the "burner phone" carried by the Community Safety and Support Team
* `CONDUCT_LINK`: Link to the Code of Conduct page for the current conference

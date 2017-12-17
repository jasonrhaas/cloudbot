# slackcloud

**slackcloud** generates word clouds using Slack chat history.

This application runs on a server that is reachable by Slack.  It is triggered by a Slack "Slash Command".  After receiving the POST from Slack it then grabs the history from the Slack channel it was called from.  From that history (100 words), it generates a word cloud and uploads it to the same channel.

## Requirements

- Slack
- Ubuntu or Mac OSX
- Python 2.7

## Quickstart


- On your webserver, `git clone git@github.com:jasonrhaas/slackcloud`.
- Create a custom slash command under the Slack "Custom Integrations" tab.    This is the command you will use to kick off a word cloud.  Configure the command to point towards the webserver that you will be hosting **slackcloud** on.
- Create a custom Bot under the Slack "Custom Integrations" tab.  This bot is the user that will upload the word cloud picture.
- In your environment, add the following environment variables.  For Mac OSX, use **~/.bash_profile**.  For Ubuntu, use **~/.bash_aliases**.

```
# Slack bot token
export SLACK_AUTH='xxxx'
# Slack Team ID
export SLACK_TEAMID='xxxx'
# Slack command name
export SLACK_CMD1_NAME='xxxx'
# Slack command token
export SLACK_CMD1_TOKEN='xxxx'
```

- Inside a virtualenv, run `pip install -r requirements.txt`.
- See specific Mac OSX or Linux sections below for special Pillow and Matplotlib instructions.
- Inside the virtualenv, run `python slackcloud.py`.  The Flask application runs on **localhost:8081**.  That port needs to be forwarded out to port 80 or 443 using Apache or Nginx on your webserver (the same one you set up to use for the Slash command).
- In a slack channel, type `/command` and you should be greeted by a bot responding with a word cloud!

### Mac OSX

- Inside the virtualenv, `pip install Pillow`
- If you try running the application in this state you will get an error message from Matplotlib complaining about running inside a virtualenv.  See [Virtualenv FAQ](http://matplotlib.org/faq/virtualenv_faq.html) for how to workaround this.

### Linux

Installing **Pillow** on Linux can be a little bit tricky and depends on the distribution and OS packages.  See [Pillow install instructions](http://pillow.readthedocs.org/en/3.0.x/installation.html#linux-installation).


### Deploy to Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

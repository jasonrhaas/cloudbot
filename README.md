# slackcloud

**slackcloud** generates word clouds using Slack chat history.

This application runs on a server that is reachable by Slack.  It is triggered by a Slack "Slash Command".  After receiving the POST from Slack it then grabs the history from the Slack channel it was called from.  From that history (100 words), it generates a word cloud and uploads it to the same channel.

## Requirements

- Slack
- Ubuntu or Mac OSX
- Python 2.7

## Quickstart (With Heroku)

1. [Create a new Slack Application](https://api.slack.com/apps?new_app=1)

2. [Create a custom slack bot](https://my.slack.com/services/new/bot)

3. In your environment, add the following environment variables. For Mac OSX, use **~/.bash_profile**.  For Ubuntu, use **~/.bash_aliases**.
    - SLACK_AUTH
       - Bot User OAuth Access Token. It will begin `with xoxb-`
       - `export SLACK_AUTH='xoxb-xxxxxxx'`
    - SLACK_TEAMID
       - [How to find your Slack TeamId](https://stackoverflow.com/a/45339988)
       - `export SLACK_TEAMID='xxxx'`
    - SLACK_CMD1_NAME
       - You can name this whatever you want. By default, it is called `wordcloud`
       - `export SLACK_CMD1_NAME='wordcloud'`
    - SLACK_CMD1_TOKEN
       - Your slack app verification token.
       - `export SLACK_CMD1_NAME='xxxx'`

    ![](https://content.screencast.com/users/fdel15/folders/Jing/media/8702d5a7-5aba-48e1-bbde-1b9f2ca20a57/00000033.png)

4. Click the button below to deploy to Heroku. (Deploying can take a couple of minutes)

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

5. In your Slack App, create a new `Slash Command`
    - The `Command` field must be the same value as `SLACK_CMD1_NAME`
    - The `Request Url` should be your new Heroku app that you created in the previous step.

6. Inside a virtualenv, run `pip install -r requirements.txt`.

7. See specific Mac OSX or Linux sections below for special Pillow and Matplotlib instructions.

8. Inside the virtualenv, run `python slackcloud.py`.

9. In a slack channel, type `/command` and you should be greeted by a bot responding with a word cloud!

### Mac OSX

- Inside the virtualenv, `pip install Pillow`
- If you try running the application in this state you will get an error message from Matplotlib complaining about running inside a virtualenv.  See [Virtualenv FAQ](http://matplotlib.org/faq/virtualenv_faq.html) for how to workaround this.

### Linux

Installing **Pillow** on Linux can be a little bit tricky and depends on the distribution and OS packages.  See [Pillow install instructions](http://pillow.readthedocs.org/en/3.0.x/installation.html#linux-installation).

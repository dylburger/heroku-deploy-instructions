### Requirements

You must have the following software installed:

* [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
* `git`

### Instructions

Log into heroku.com, create a new test app. This can be named whatever you want, as long as an app with that name doesn't exist already on Heroku.

Once created, follow the initial instructions in the section titled "Deploy using Heroku Git", e.g. ensure you run

    heroku login

to log into the Heroku CLI. Then, within your project directory, run

    git init
    heroku git:remote -a your-project

**making sure to replace `your-project` with the name of your project, as noted in the instructions on the page**.

All development of your app should happen within a Python virtual environment. As long as you have all of your Python dependencies (e.g. `flask`) installed within this virtual environment, you should be create a list of these requirements in a `requirements.txt` file using this command:

    pip freeze --local > requirements.txt

This `requirements.txt` file will be used by Heroku when it deploys your app on its servers. In order to run your app, it needs to know what third party software to install!
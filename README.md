### Why?

Heroku provides a platform to facilitate the deployment of web applications. You don't have to learn how to spin up your own Linux server and manage all the bits and pieces of your own web server. You trust Heroku to provide that infrastructure, which lets you focus on the application code.

You can also deploy up to 5 simple apps for free (some services are paid, even for these 5 apps). This makes Heroku an ideal place to deploy Python apps for your portfolio. If your app doesn't have any "backend" (e.g. Python, SQL) components, and uses just HTML / CSS / JS, consider [Github Pages](https://pages.github.com/).

### Requirements

You must have the following software installed:

* [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
* `git`

### Instructions

Log into heroku.com and visit your [list of apps](https://dashboard.heroku.com/apps), clicking on the **New** button in the top-right of the screen and selecting the option **Create new app**. This can be named whatever you want, as long as an app with that name doesn't exist already on Heroku.

Once created, follow the initial instructions in the section titled "Deploy using Heroku Git", e.g. ensure you run

    heroku login

to log into the Heroku CLI. Then, within your project directory, run

    git init
    heroku git:remote -a your-project

**making sure to replace `your-project` with the name of your project, as noted in the instructions on the page**.

All development of your app should happen within a Python virtual environment. As long as you have all of your Python dependencies (e.g. `flask`) installed within this virtual environment, you should be create a list of these requirements in a `requirements.txt` file using this command:

    pip freeze --local > requirements.txt

This `requirements.txt` file will be used by Heroku when it deploys your app on its servers. In order to run your app, it needs to know what third party software your app requires!

The `app.py` file contains the sample Flask app we're going to deploy to Heroku. This contains the simplest amount of code necessary to run a Flask app with a single route.

Finally, we'd like to make sure our app can scale to handle multiple requests at a time. Heroku allows us to define a [`Procfile`](https://devcenter.heroku.com/articles/python-gunicorn), which tells Heroku which commands to run when deployed to Heroku's servers. Our `Procfile` contains the following code:

    web: gunicorn app:app

This command is tied to Heroku's web servers tied to your application, and utilizes [`gunicorn`](https://devcenter.heroku.com/articles/python-gunicorn), which enables us to process multiple HTTP requests at a time (by default, Flask will only process one). This `Procfile` tells `gunicorn` to run the `app` object within the `app.py` file.

Once you've configured everything, just run 

    git add --all
    git commit -m 'Committing Heroku app to git'
    git push heroku master

`git push` will push your code to Heroku, and you should see a log of the activity as Heroku processes your app.

If everything works as planned, you should see the following output at the end of your deploy logs:

    remote: -----> Launching...
    remote:        Released v3
    remote:        https://dylan-test-flask-app.herokuapp.com/ deployed to Heroku
    remote:
    remote: Verifying deploy... done.
    To https://git.heroku.com/dylan-test-flask-app.git
     * [new branch]      master -> master

If so, run

    heroku open

which will launch a web browser pointing to the URL of your app.

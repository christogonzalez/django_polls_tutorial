# Chris's Django Polls App

I created the boilerplate for this project using: https://docs.djangoproject.com/en/5.2/intro/tutorial01/

The views/html files are different than the expected output since I made my own personalized edits! For this project I used two tools for development:

- Conda for my environment manager
- Poetry as my package manager 

** What is Django? **

It's a full-stack tool that helps you create a skeleton design of an app to easily allow you to scale-up into fully functioning system. This is done by doing most of the heavy-lifting in the backend by allowing you to write your ideas in python, something more familar to people, that is then transcribed into your preferred relational database language. It also simplifies testing and routing by allowing you to control these features through python scripts.

** To start the project, run these two commands! **

``` Bash
django-admin startproject mysite djangotutorial
python manage.py startapp polls
```

You can infer that a project can contain multiple apps, where the initial one is mysite and then we add polls to the project in the second command. This shows how Django allows you to scale up a simple project into much more complex systems by allowing you to add stand-alone apps that are the routed together through the python scripts generated in the repo! You can learn more about this in the link above.

## Endpoints

These are all the endpoints that I used throughout my project! All of these where configured in the various `url.py` files found in this repo. Some of the endpoints are standard Django, especially on the admin side since that is an app that is pre-built. But that python file is where you create the format for each endpoint!

For context, http://127.0.0.1:8000 is the local port I used but that can change per user. Focus on the end-bit of each url.

- http://127.0.0.1:8000/polls/
- http://127.0.0.1:8000/polls/{question_id}
- http://127.0.0.1:8000/admin
- http://127.0.0.1:8000/admin/polls/questions
- http://127.0.0.1:8000/admin/polls/questions/{question_id}/change

## Models

Within the Django repo, you are given `models.py` that allows you to create Python objects that you want created into sql tables. This is done through the following two commands:

``` Bash
python manage.py makemigrations polls
python manage.py migrate
```

Which will look through the changes made to the repo's model, convert that new Python code into sql injections, and then uses those to update your database! The first command commits your changes to the models and then the second one actually pushes them to the databases you are connected to.

### Questions

The first model created for this project. It holds all info related to question:

- the question being asked (stored as a String)
- the published date (stored as DateTime)

Lastly, a method named `was_published_recently` is created to compare the published date. Returning a boolean on if the question was created more than a day ago.

### Choices

Questions need to have answers, and that's where this model ties in. The different answer and their votes are stored within this object in the following format:

- the question this choice is answering (stored as mode.Question type)
- the text representing the choice (stored as a string)
- the amount of votes recieved for this choice (stored as an int)

### Model-View-Controller

After doing some research, I have found that Django follows a different architecture (Model-Template-View) to structure their projects. But I will relate what I have learned back to system that I am much more familar with!

- Model -> `models.py` since it direclty outlines how your data is organized and then relates that back to the databases using `manage.py`
- Controller -> 'views.py' because it recieves requests from the user, contains logic on what to do next, and usually returns a response
- View -> templates/polls/ since it contains all the `.html` files that direclty edit what the user is viewing

There are more parts that contribute into the cycle of user interactions to the databases and then back to the user as a view. One being `urls.py` handling the routing of different endpoints. Additionally, `manage.py` is used as an administration tool to call the Django API that allows you to create more questions within this project.

## Secret-key

This is stored in `mysite/settings.py`! Commiting this to repo isn't something to worry about now but you can rotate it, followed by setting a GitHub varaible or creating a `.env` file

## API Testing

Django comes with its own shell, which you can call by typing the following command, `python manage.py shell`. Here is an example of some python code you could write that will affect your database!

``` python
from django.utils import timezone
q = Question(question_text="Does pineapple belong on pizza?", pub_date=timezone.now())
q.save()

q.choice_set.create(choice_text="Of course!", votes=0)
q.choice_set.create(choice_text="That's evil, no!", votes=0)
```
# Chris's Django Polls App

I created the boilerplate for this project using: https://docs.djangoproject.com/en/5.2/intro/tutorial01/

The views/html files are different than the expected output since I made my own personalized edits!

## Endpoints

These are all the endpoints that I used throughout my project!

For context, http://127.0.0.1:8000 is the local port I used but that can change per user. Focus on the end-bit of each url.

- http://127.0.0.1:8000/polls/
- http://127.0.0.1:8000/polls/{question_id}
- http://127.0.0.1:8000/admin
- http://127.0.0.1:8000/admin/polls/questions
- http://127.0.0.1:8000/admin/polls/questions/{question_id}/change

## Models

Within the Django repo, you are given `models.py` that allows you to create Python objects that you want created into sql tables. This is done through the following two commands:

``` Bash
python manage.py migrate
python manage.py makemigrations polls
```

Which will look through the changes made to the repo's model, convert that new Python code into sql injections, and then uses those to update your database!

### Questions

The first model created for this project. It holds all info related to question:

- the question being asked (stored as a String)
- the published date (stored as DateTime)

Lastly, a method named `was_published_recently` is created to compare the published date. Returning a boolean on if the question was created more than a day ago.

### Choices

Questions need to have answers, and that's where this model ties in. The different 

### Model-Controller-View

After doing some research, I have found that Django follows a different architecture (Model-Template-View) to structure their projects. But I will relate what I have learned back to system that I am much more familar with!

- Model -> `models.py` since it direclty outlines how your data is organized and then relates that back to the databases using `manage.py`
- Controller -> 'views.py' because it recieves requests from the user, contains logic on what to do next, and usually returns a response
- View -> templates/polls/ since it contains all the `.html` files that direclty edit what the user is viewing

There are more parts that contribute into the cycle of user interactions to the databases and then back to the user as a view. One being `urls.py` handling the routing of different endpoints. Additionally, `manage.py` is used as an administration tool to call the Django API that allows you to create more questions within this project.

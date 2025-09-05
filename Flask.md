---
tags:
  - python
  - backend
references:
  - https://youtu.be/Z1RJmh_OqeA?si=a8QibtJ2_Zf37naO
date_created: 2025-07-18
date_modified: 2025-07-18
---
---
## 0. Installation

- Download and install python.
- Open up a project and run `pip3 install virtualenv`
- Then `virtualenv env` and `source /env/bin/activate`
- Finally `pip3 install flask flask-sqlalchemy`

---
## 1. Core Flask App Setup

This is a simple hello world flask application.

```python
from flask import Flask

app = Flask(__name__)


@app.route("/")
def index():
    return "Hello world"


if __name__ == "__main__":
    app.run(debug=True)
```

The application is run using a conditional block that ensures the server only starts when the script is executed directly. Debug mode is enabled to provide detailed error pages and auto-reload the server on code changes.

---
## 2. Templates & Static Files

Flask can render HTML files from a `templates` folder.

- Create a folder named `templates` in your project directory.
- Create a file inside it named `index.html`.
- Create another file named `base.html` for template inheritance.
- Create a folder named `static` for CSS, JS, and other static files. Inside `static`, create a `css` folder and a `main.css` file.

The `app.py` file is updated to render this template.

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route("/")
def index():
    # Renders the index.html file from the templates folder
    return render_template('index.html')


if __name__ == "__main__":
    app.run(debug=True)
```

**`base.html`** acts as a parent template.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link
      rel="stylesheet"
      href="{{ url_for('static', filename='css/main.css') }}"
    />
    <title>{% block head %}{% endblock %}</title>
  </head>
  <body>
    {% block body %}{% endblock %}
  </body>
</html>

```

**`index.html`** inherits from `base.html` and fills in the `body` block.

```html
{% extends 'base.html' %}

{% block head %}
Task Master
{% endblock %}

{% block body %}
<div class="content">
    <h1 style="text-align: center">Task Master</h1>
</div>
{% endblock %}
```

---
### 3. Database Integration with Flask-SQLAlchemy

Configure the app to use a database.

- In `app.py`, import `SQLAlchemy` and configure the database URI.
- The URI `'sqlite:///test.db'` tells SQLAlchemy to use a SQLite database file named `test.db`.
- Define a database model `Todo` which will correspond to a table in the database.

```python
from flask import Flask, render_template, url_for
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime

app = Flask(__name__)
# /// for relative path, //// for absolute path
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///test.db'
db = SQLAlchemy(app)

# Create a model for the database table
class Todo(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(200), nullable=False)
    date_created = db.Column(db.DateTime, default=datetime.utcnow)

    def __repr__(self):
        return '<Task %r>' % self.id

# ... rest of the app.py file
```

To create the database file and the `todo` table, open an interactive Python shell.

```bash
# In your terminal
$ python3
>>> from app import app, db
>>> with app.app_context():
...     db.create_all()
...
>>> exit()
```

A `test.db` file will appear in your project directory.

### 4. Implementing CRUD (Create, Read, Update, Delete)

#### Create & Read Tasks

Update the index route to handle form submissions (`POST`) and display all tasks from the database (`GET`).

**`app.py`**

```python
from flask import Flask, render_template, url_for, request, redirect
# ... other imports

# ... app and db setup

# ... Todo model

@app.route('/', methods=['POST', 'GET'])
def index():
    if request.method == 'POST':
        task_content = request.form['content']
        new_task = Todo(content=task_content)

        try:
            db.session.add(new_task)
            db.session.commit()
            return redirect('/')
        except:
            return 'There was an issue adding your task'

    else:
        tasks = Todo.query.order_by(Todo.date_created).all()
        return render_template('index.html', tasks=tasks)

# ... rest of the app
```

**`index.html`** needs a form to add tasks and a table to display them.

```html
{% extends 'base.html' %}

{% block head %}
<title>Task Master</title>
{% endblock %}

{% block body %}
<div class="content">
    <h1 style="text-align: center">Task Master</h1>

    {% if tasks|length < 1 %}
    <h4 style="text-align: center">There are no tasks. Create one below!</h4>
    {% else %}
    <table class="center">
        <tr>
            <th>Task</th>
            <th>Added</th>
            <th>Actions</th>
        </tr>
        {% for task in tasks %}
            <tr>
                <td>{{ task.content }}</td>
                <td>{{ task.date_created.date() }}</td>
                <td>
                    <a href="">Delete</a>
                    <br>
                    <a href="">Update</a>
                </td>
            </tr>
        {% endfor %}
    </table>
    {% endif %}

    <form action="/" method="POST" class="center">
        <input type="text" name="content" id="content">
        <input type="submit" value="Add Task">
    </form>
</div>
{% endblock %}
```

#### Delete Tasks

Create a new route to handle task deletion.

**`app.py`**

```python
# ... inside app.py

@app.route('/delete/<int:id>')
def delete(id):
    task_to_delete = Todo.query.get_or_404(id)

    try:
        db.session.delete(task_to_delete)
        db.session.commit()
        return redirect('/')
    except:
        return 'There was a problem deleting that task'

# ... rest of the app
```

**`index.html`** (update the delete link)

```html
<a href="/delete/{{ task.id }}">Delete</a>
```

#### Update Tasks

Create a new route and a new template for the update page.

**`app.py`**

```python
# ... inside app.py

@app.route('/update/<int:id>', methods=['GET', 'POST'])
def update(id):
    task = Todo.query.get_or_404(id)

    if request.method == 'POST':
        task.content = request.form['content']

        try:
            db.session.commit()
            return redirect('/')
        except:
            return 'There was an issue updating your task'
    else:
        return render_template('update.html', task=task)
```

**`index.html`** (update the update link)

```html
<a href="/update/{{ task.id }}">Update</a>
```

**`update.html`** (new file in `templates` folder)

```html
{% extends 'base.html' %}

{% block head %}
<title>Update Task</title>
{% endblock %}

{% block body %}
<div class="content">
    <h1 style="text-align: center">Update Task</h1>

    <form action="/update/{{task.id}}" method="POST" class="center">
        <input type="text" name="content" id="content" value="{{task.content}}">
        <input type="submit" value="Update">
    </form>
</div>
{% endblock %}
```

### 5. Deployment to Heroku

- Sign up for a free Heroku account and install the Heroku CLI.
- In your terminal, run `heroku login`.
- Install a production-ready web server: `pip3 install gunicorn`.
- Freeze your project's dependencies into a `requirements.txt` file: `pip3 freeze > requirements.txt`.
- Create a `Procfile` (with a capital P, no extension) in your root project directory with the following content:

**`Procfile`**

```
web: gunicorn app:app
```

This tells Heroku to serve the `app` object from your `app.py` file using the `gunicorn` server.

- Initialize a git repository and deploy.

```bash
git init
git add .
git commit -m "Initial commit"
heroku create
git push heroku master
```

- Your application is now live. You can open it by running `heroku open`.


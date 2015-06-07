# Flask-Register

### Usage:

#### 1.Init RegisterManager
``` python
...
from flask.ext.register import RegisterManager
...

...
signup = RegisterManager(app)
signup.save_redirect_view('index') # A name of view function where you want redirect.
...
```

#### 2.Configurate for RegisterManager
``` python
...
REGISTER_ENABLED = True/False
...
```

#### 3.Use RegisterManager decorator with view function.
``` python
...
from app import signup
from flask.ext.register import register_required
...

...
# Option
# If doesn't use this code in `before_request`
# Register link of templates will show all time, but
# clients can't use the view.
@app.before_request
def bef_req():
	...
	g.register_form = signup.is_enabled()
	...
...

...
@app.route('/register')
@register_required
def register():
	pass
...
```

#### 4.Get a piece of state that can show a Link in template.
This is an option, if doesn't use `register_form`,
Register link will show all time, but clients can't use
the view.
``` html
<nav>
	<a href="{{ url_for('index') }}">Home</a>
	{% if g.register_form %}
	| <a href="{{ url_for('register') }}">Register</a>
	{% endif %}
</nav>
```

# License
MIT License


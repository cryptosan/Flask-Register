# Flask-Register

### Usage:

Init RegisterManager
``` python
...
from flask.ext.register import RegisterManager
...

...
signup = RegisterManager(app)
signup.save_redirect_view('index') # A name of view function where you want redirect.
...
```

Configurate in `config.py`
``` python
...
REGISTER_ENABLED = True/False
...
```

Use RegisterManager decorator with view function.
``` python
...
from app import signup
from flask.ext.register import register_required
...

...
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

Get a piece of state that can show a Link in templates
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


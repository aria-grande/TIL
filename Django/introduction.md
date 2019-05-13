# Django
Python 기반의 web framework.

## Authentication
https://developer.mozilla.org/ko/docs/Learn/Server-side/Django/Authentication

- [로그인 template customizing](https://developer.mozilla.org/ko/docs/Learn/Server-side/Django/Authentication#Login_template)
Create a new HTML file called /locallibrary/templates/registration/login.html. give it the following contents:
```python
{% extends "base_generic.html" %}

{% block content %}

{% if form.errors %}
  <p>Your username and password didn't match. Please try again.</p>
{% endif %}

{% if next %}
  {% if user.is_authenticated %}
    <p>Your account doesn't have access to this page. To proceed,
    please login with an account that has access.</p>
  {% else %}
    <p>Please login to see this page.</p>
  {% endif %}
{% endif %}

<form method="post" action="{% url 'login' %}">
{% csrf_token %}

<div>
  <td>{{ form.username.label_tag }}</td>
  <td>{{ form.username }}</td>
</div>
<div>
  <td>{{ form.password.label_tag }}</td>
  <td>{{ form.password }}</td>
</div>

<div>
  <input type="submit" value="login" />
  <input type="hidden" name="next" value="{{ next }}" />
</div>
</form>

{# Assumes you setup the password_reset view in your URLconf #}
<p><a href="{% url 'password_reset' %}">Lost password?</a></p>

{% endblock %}
```

## Form
https://developer.mozilla.org/ko/docs/Learn/Server-side/Django/Forms

## Custom Filter
Django offers template language and filters
https://docs.djangoproject.com/en/2.2/howto/custom-template-tags/

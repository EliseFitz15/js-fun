# Fun with Javascript

## Ember.js Intro

### Installing

In your root directory install ember globally with the following:
`npm install -g ember-cli@2.7`

**Note:** If you need to install node and npm you can find directions how to do so [here](https://docs.npmjs.com/getting-started/installing-node)

### Create a New Project

In your command line we can now quickly set up a new ember project:

`ember new todo-list`

Open up your new app in your text editor.


### Running a server

To start the server we can simply use the command:

`ember serve`

After a few seconds, you should see output that looks like this:

```
Livereload server on http://localhost:49152
Serving on http://localhost:4200/
```

(To stop the server at any time, type Ctrl-C in your terminal.)

Open http://localhost:4200 in your browser of choice. You should see an Ember welcome page and not much else. Congratulations! You just created and booted your first Ember app.

### Generating a Template

To create our first view let's generate a template to hold out HTML.

`ember generate template application`

**Note** the `application` template is always on the screen it's a default template. Other templates can them be linked and displayed through here.

Also notice that this template is a Handlebars file. Handlebars is a short hand for compiling our html and JS together.

Let's add the following to our `application.hbs`:

```
<h1> TO-DO List App </h1>

{{outlet}}
```

This outlet here is where other templates we create will be inserted on the same page.

### Define a Route

Ember comes with generators that automate the boilerplate code for common tasks. To generate a route, type this in your terminal:

`ember generate route todos`

Ember has created a number of things for us:

- A template to be displayed when the user visits `/todos`
- A Route object that fetches the model used by that template.
- An entry in the application's router (located in app/router.js).
- A unit test for this route.

Open the newly-created template in app/templates/todos.hbs and add the following HTML:

app/templates/todos.hbs
```
<h2>List of things to do today...</h2>
```

In your browser, open http://localhost:4200/todos. You should see the <h2> you put in the todos.hbs template, right below the <h1> from our application.hbs template.

Now that we've got the todos template rendering, let's give it some data to render.


### Add Data to Render in Template

We do that by specifying a model for that route, and we can specify a model by editing app/routes/todos.js.

```
import Ember from 'ember';

export default Ember.Route.extend({
  model() {
    return ['Catch all the Pokemon', 'Become a JavaScript Master', 'Get my React.js on', 'Hangout with Tomster', 'Seriously, Gotta catch 'em all'];
  }
});
```

In a route's model() method, you return whatever data you want to make available to the template. In this case we have given it a list of things we want to accomplish.

### Rendering our Javascript in our Template

Now we can tell Ember how to turn that array of strings into HTML.

In our `app/templates/todos.hbs` let's make the following update:

```
<ul>
  {{#each model as |todo|}}
    <li>{{todo}}</li>
  {{/each}}
</ul>
```

If we want to iterate through JS objects rather than just strings we could simply update the data form we are sending to the Template and the way we iterate through:

```
[{ item: 'Catch all the Pokemon', complete: false}, { item: 'Become a JavaScript Master', complete: true}, {item: 'Get my React.js on', complete: false}, { item: 'Hangout with Tomster', complete: true}];
```

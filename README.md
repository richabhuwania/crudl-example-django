# crudl django example
This is a [crudl](http://crudl.io/) example with [Django](https://www.djangoproject.com/) and [DRF](http://www.django-rest-framework.org/) for the REST-API as well as [Graphene](http://graphene-python.org/) for GraphQL.

## Requirements
* Node.js
* python
* virtualenv
* SQLite

## Installation
1. Create and activate a python **virtual environment**.

2. Clone this repository and cd into the new folder:

    ```
    $ git clone https://github.com/crudlio/crudl-example-django.git
    $ cd crudl-example-django
    ```

3. Install the python requirements:

    ```
    $ pip install -r conf/requirements.txt
    ```

4. Setup the database (SQLite) and add contents:

    ```
    $ python manage.py migrate
    $ fab init -f conf/fabfile
    ```

5. Start the django development server:

    ```
    $ python manage.py runserver
    ```

Open your browser and go to ``http://localhost:8000/crudl-rest/`` and login with one of the users.
You have 3 users (patrick, axel, vaclav) with password "crudl" for each one.

### Install crudl-admin (REST)
Go to /crudl-admin-rest/ and install the npm packages, then run watchify:
```
$ npm install
$ npm run watchify
```

### Install crudl-admin (GraphQL)
Go to /crudl-admin-graphql/ and install the npm packages, then run watchify:
```
$ npm install
$ npm run watchify
```

## URLs
```
/api/               # REST API (DRF)
/graphiql/          # GraphQL Query Interface
/admin/             # Django Admin (Grappelli)
/crudl-rest/        # Crudl Admin (REST)
/crudl-graphql/     # Crudl Admin (GraphQL)
```

## Notes
While this example is simple, there's still a couple of more advanced features in order to represent a real-world scenario.

### Authentication
Both the REST and GraphQL API is only accessible for logged-in users based on TokenAuthentication.
Authentication for GraphQL is done with a decorator wrapping the basic URL.

### Mutually dependent fields
When adding or editing an _Entry_, the _Categories_ depend on the selected _User_.
If you change the field _User_, the options of field _Category_ are populated based on the chosen _User_.

### Foreign Key, Many-to-Many
There are a couple of foreign keys being used (e.g. _Category_ with _Entry_) and one many-to-many field (_Tags_ with _Entry_).

### Relation with different endpoint
The collection _Links_ is an example of related objects which are assigned through an intermediary table with additional fields.
You can either use the main menu in order to handle all Links are an individual _Entry_ in order to edit the _Links_ assigned to this _Entry_ (which are shown using tabs).

### Autocompletes
We decided to use autocomplete fields for all foreign-key and many-to-many relations.

### Custom fields
With _Users_, we added a custom field _Name_ which is not part of the database or the API.
The methods _normalize_ and _denormalize_ are being used in order to manipulate the data stream.

### Custom components
XXX

### Superuser vs staff user
All 3 _Users_ are able to login to crudl (because is_staff is True). But only superusers (patrick, axel) are allowed to edit all objects. The third user (vaclav) is only able to see and edit his own objects. Besides, only superusers are able to change a users password (user vaclav has no permission to edit his own password).

### Initial values
XXX

### Validate fields and form
XXX

## Development
This example mainly shows how to use crudl. It is not intended for development on crudl itself.

Developing
==========

Create a new virtualenv and install the required libraries for
the default pyrebase + the testing tools.

```
mkvirtualenv -p python3 pyrebase-dev # if you have virtualenvwrapper installed
pip install -r requirements.txt -r requirements.dev.txt
```


From the Firebase project console, configure a cloud firestore database to use for testing purposes.

From the Firebase project settings, under service accounts, generate a new private key.

Prepare credentials:

```
cp ~/my_secret_firebase_service_account_key.json ./secret.json
cp ./tests/config.template.py ./tests/config.py
# Update the ./tests/config.py file with your test database info.
```

Note, the `databaseUrl` is not provided anymore, but here are some [instructions on how to find it](https://stackoverflow.com/questions/65601040/databaseurl-not-found-in-firestore-sdk-snippet).

Note that to make it easier to run the tests, they read/write to
`/pyrebase_tests/` on your firebase database. They should not mess
up the rest of the database.


Run the tests:

```
pytest -s tests
```

On MacOS you may need to fix the shebang in the pytest executable
to make it point to the correct python binary.

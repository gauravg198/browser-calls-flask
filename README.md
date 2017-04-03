<a href="https://www.twilio.com">
  <img src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg" alt="Twilio" width="250" />
</a>

# Browser Calls for Python - Flask

[![Build Status](https://travis-ci.org/TwilioDevEd/browser-calls-flask.svg?branch=master)](https://travis-ci.org/TwilioDevEd/browser-calls-flask)

Learn how to use [Twilio Client](https://www.twilio.com/client) to make
browser-to-phone and browser-to-browser calls with ease. The unsatisfied
customers of the Birchwood Bicycle Polo Co. need your help!

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/browser-calls/python/flask)!

## Quickstart

### Create a TwiML App

This project is configured to use a **TwiML App**, which allows us to easily set
the voice URLs for all Twilio phone numbers we purchase in this app.

Create a new TwiML app [here](https://www.twilio.com/user/account/apps/add) and
use its `SID` as the `TWIML_APPLICATION_SID` environment variable wherever you
run this app.


![Creating a TwiML App](http://howtodocs.s3.amazonaws.com/call-tracking-twiml-app.gif)

Once you have created your TwiML app, configure your Twilio phone number to use
it ([instructions here](https://www.twilio.com/help/faq/twilio-client/how-do-i-create-a-twiml-app)).
If you don't have a Twilio phone number yet, you can purchase a new number in
your [Twilio Account Dashboard](https://www.twilio.com/user/account/phone-numbers/incoming).

## Local development

This project is built using the [Flask](http://flask.pocoo.org/) web framework. It runs on Python 2.7+ and Python 3.4+.

1. To run the app locally, first clone this repository and `cd` into it.

1. Create a new virtual environment.
    - If using vanilla [virtualenv](https://virtualenv.pypa.io/en/latest/):

        ```bash
        $ virtualenv venv
        $ source venv/bin/activate
        ```

    - If using [virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/):

        ```bash
        $ mkvirtualenv browser-calls
        ```

1. Install the requirements.

    ```bash
    $ pip install -r requirements.txt
    ```

1. Copy the `.env.example` file to `.env`, and edit it including your credentials
   for the Twilio API (found at https://www.twilio.com/user/account/settings). You
   will also need a [Twilio Number](https://www.twilio.com/user/account/phone-numbers/incoming) and TwiML App SID you made above.

1. Run `source .env` to apply the environment variables (or even better, use [autoenv](https://github.com/kennethreitz/autoenv))

1. Run the migrations.

    ```bash
    $ python manage.py db upgrade
    ```

1. Modify seed data.

   We have provided an example of name and phone number in the seed data. In order for
   the application to send SMS notifications, you must edit this seed data providing
   a real phone number where you want the SMS notifications to be received.

   In order to do this, you must modify
   [this file](https://github.com/TwilioDevEd/browser-calls-flask/blob/master/manage.py#L25)
   that is located at: `project_root/manage.py`

1. Seed the database.

   ```bash
   $ python manage.py dbseed
   ```

1. Start ngrok

    To actually forward incoming calls, your development server will need to be publicly accessible.
    [We recommend using ngrok to solve this problem](https://www.twilio.com/blog/2015/09/6-awesome-reasons-to-use-ngrok-when-testing-webhooks.html).


   ```bash
   $ ngrok http 5000
   ```

    Once you have started ngrok, update your TwiML app's voice URL setting to use your ngrok hostname. It will look something like this:

    ```
    http://88b37ada.ngrok.io/support/call
    ```

1. Start the development server.

    ```bash
    $ python manage.py runserver
    ```

Once ngrok is running, open up your browser and go to your ngrok URL. It will
look like this: `http://88b37ada.ngrok.io`

That's it!

## Run the tests

You can run the tests locally through [coverage](http://coverage.readthedocs.org/):

1. Run the tests.

    ```
    $ coverage run manage.py test
    ```

You can then view the results with `coverage report` or build an HTML report with `coverage html`.

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.

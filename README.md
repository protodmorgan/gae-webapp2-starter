# GAE webapp2 starter
This is simple webapp2 template on Google App Engine

![](/sources/gae-webapp2-starter.png)

**Features**
- GAE
  - webapp2 framework
  - OAuth2 loging (Google)
- Bootstrap theme (todc)
- Gulp supported
- browserify

**file structure**

```
.
├── README.md
├── app.yaml                             # gae config app.yaml
├── appengine_config.py                  # load library
├── application                          # application
│   ├── __init__.py
│   ├── app.py                           # application entry point
│   ├── client_secret.json               # client_secret, download from Google Developers Console
│   ├── controllers
│   │   ├── __init__.py
│   │   ├── base.py                      # base class
│   │   └── error_handler.py             # error handler (404,403,500)
│   ├── models.py                        # datastore models
│   ├── secrets.py                       # helper to load webapp2_extras.sessions
│   ├── session-secret                   # webapp2_extras.sessions
│   ├── settings.py                      # application settings. ex: CLIENT_SECRETS, WEB_CLIENT_ID .etc
│   └── utils.py                         # utils functions
├── assets                               # assets
│   ├── javascript
│   │   └── index.js
│   └── stylesheet
│       ├── custom.css
│       ├── spinner.css
│       └── style.css
├── bower.json                           # bower.json
├── favicon.ico
├── gulpfile.js                          # gulpfile.js to build public
├── package.json                         # npm packages
├── public                               # auto generated by gulp
│   ├── css
│   │   └── main.css
│   ├── fonts
│   │   ├── glyphicons-halflings-regular.eot
│   │   ├── glyphicons-halflings-regular.svg
│   │   ├── glyphicons-halflings-regular.ttf
│   │   ├── glyphicons-halflings-regular.woff
│   │   └── glyphicons-halflings-regular.woff2
│   └── javascript
│       ├── bundle.js
│       ├── specs.js
│       └── vendors.js
├── requirements.txt                     # pip requirements install list
└── templates                            # gae templates
    ├── _head.html
    ├── base.html
    ├── errors
    │   ├── 403.html
    │   ├── 404.html
    │   └── 500.html
    └── index.html
```

## Getting Started
clone repo and install dependency.

```sh
# clone repo from github
$ git clone https://github.com/cage1016/gae-webapp2-starter

# install pip packages
$ pip -r requirements.txt -t lib

# install bower packages
$ bower install

# install npm packages
$ npm install

# build assets resources
$ gulp
```

### prepare _client_secret.json_ for Sign in

Create client id for web application

1. Click **APIs & Auth** > **credential**.
2. Click **Click new Client ID**.
3. Choose **Web application**.
4. modify **Authorized JavaScript origins**.

  ```sh
  http://localhost:8080
  ```

5. modify **Authorized redirect URIs**.

  ```sh
  http://localhost:8080/widget
  ```

6. Click **Create Client ID**
7. Download credential JSON file

Create Service Account

1. Click **APIs & Auth** > **credential**.
2. Click **Click new Client ID**.
3. Choose **Service Account**.
4. Key type : **P12 Key**
5. Click **Create Client ID**
**P12.Key** file will be downloaded. You have to convert `p12` to `pem` cause PKCS12 format is not supported by the PyCrypto library.

  ```sh
  (openssl pkcs12 -in xxxxx.p12 -nodes -nocerts > privatekey.pem)
  ```

Create Public API access

1. Click **APIs & Auth** > **credential**.
2. Click **Click new Key** in **Public API access** section
3. Click **Browser key**
4. Click **Create**

### modify settings

_application/settings.py_

replace `<web-client-id>`, `<developer=key>`, `<service-account-email>` your create earlier

replace `<site-name>`, `https://<project-id>.appspot.com`, `<site-owner>`

```python
# put client_secret.json in application folder
CLIENT_SECRETS = os.path.join(os.path.dirname(__file__), 'client_secret.json')

WEB_CLIENT_ID = '<web-client-id>'

DEVELOPER_KEY = '<developer=key>'

SERVICE_ACCOUNT_EMAIL = '<service-account-email>'

SITE_NAME = '<site-name>'
BASIC_SITE_URL = 'https://<project-id>.appspot.com'
SITE_OWNER = '<site-owner>'

ADMINS = [
  # email list
]
```

run

```sh
# execute gae project
$ dev_appserver.py .

# visit http://localhost:8080
```

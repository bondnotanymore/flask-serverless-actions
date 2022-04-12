# flask-serverless-actions

##Creating and deploying a single endpoint
Let's start by deploying a single endpoint.

First, create a new directory with a package.json file:
```
$ cd flask-serverless-actions

$ npm init -f
```

Then, install a few dependencies. We're going to use the serverless-wsgi plugin for negotiating the API Gateway event type into the WSGI format that Flask expects. We'll also use the serverless-python-requirements plugin for handling our Python packages on deployment.

```buildoutcfg
$ npm install --save-dev serverless-wsgi serverless-python-requirements
```

Create a virtual environment and activate it. I'm using Python3 in my serverless.yml, so I'm specifying that here as well:
```buildoutcfg
$ virtualenv venv --python=python3
$ source venv/bin/activate
```

Then, install the required package with ```poetry install```


Now, deploy your function:
```buildoutcfg
$ sls deploy
... snip ...
Service Information
service: serverless-flask
stage: dev
region: us-east-1
stack: serverless-flask-dev
api keys:
  None
endpoints:
  ANY - https://bl4r0gjjv5.execute-api.us-east-1.amazonaws.com/dev
  ANY - https://bl4r0gjjv5.execute-api.us-east-1.amazonaws.com/dev/{proxy+}
functions:
  app: serverless-flask-dev-app
```

**Note:** If serverless/ sls command is not identified, run the following commands and the try the previous step again:
```buildoutcfg
npm config set prefix /usr/local
sudo npm i -g serverless
```

##TESTING VIA CURL

Let's create a user:

```buildoutcfg
$ curl -H "Content-Type: application/json" -X POST ${BASE_DOMAIN}/users -d '{"userId": "alexdebrie1", "name": "Alex DeBrie"}'
{
  "name": "Alex DeBrie",
  "userId": "alexdebrie1"
}
```

We've created a new user! Now, let's retrieve the user with the GET /users/:userId` endpoint:

```buildoutcfg
$ curl -H "Content-Type: application/json" -X GET ${BASE_DOMAIN}/users/alexdebrie1
{
  "name": "Alex DeBrie",
  "userId": "alexdebrie1"
}
```

That's all folks! Let's figure out more on our own! Happy learning!
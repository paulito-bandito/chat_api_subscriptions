# GRAPHQL CHAT API

A simple GraphQL API that implements subscriptions built with Python and Ariadne (Schema-first API creation library for Python)

See the full article written by Alex Kiura, it has been archived as a PDF located in the project root. It is worth the read.

The original author had an incorrect `requirements.txt` so this is an updated version that fixes that.

# To Run this Example:

## Create your virtual environment

Create the virtual environment:

```bash 
python3 -m venv chat_api_env`
```

If you are using a Mac OS or Unix computer, activate the virtual environment as follows:

```bash
source chat_api_env/bin/activate
```
To activate the virtual environment on Windows, use the following command:

```bash
chat_api_env\Scripts\activate.bat
```

## Install the dependencies

Issue a `pip` command like so `pip install -r requirements.txt`. This will look at the list of requirements in the txt file in the project root and download them. 

## Run the Server.

We need to run the GraphQL editor to test out our functionality.

Use `uvicorn --reload --port=5000 --http=h11 --ws=websockets app:app` to run our server on port 5000. 

Open up a web browser and go to the URL `http://127.0.0.1:5000/`, and see the next section for testing our chat.

# To Test this example

So in your CQL editor located at `http://127.0.0.1:5000/` issue the following GraphQL commands: 1) Create Users, 2) Set up a Subscription, and 3) Send Messages.

## 1) Create Users

```bash
mutation {
  createUser(username:"user_one") {
    success
    user {
      userId
      username
    }
  }
}

```


```bash
mutation {
  createUser(username:"user_two") {
    success
    user {
      userId
      username
    }
  }
}

```

## 2) Set up a Subscription
So now we have our users, let's test the subscriptions by pasting this in to the GraphQL editor.

```bash
subscription {
  messages(userId: "2") {
    content
    senderId
    recipientId
  }
}
```

## 3) Send a message to test the Subscription
Now open a new GraphQL editor and create a new message to see if our subscription also gets updated. 

```bash
mutation {
  createMessage(
    senderId: "1",
    recipientId: "2",
    content:"Hello there"
  ) {
    success
    message {
      content
      recipientId
      senderId
    }
  }
}
```
You should see the original subscription being updated. 


# Appendix:

This README is just referencing the article written by , located here: https://www.twilio.com/blog/graphql-api-subscriptions-python-asyncio-ariadne

It's been archived as a PDF in the project root. 

Here are some highlights:

## Steps used to Create the basic structure: 
See the PDF in the project root for the full article!

Dependencies to install:

Create a directory called chat_api for our project and navigate to it.

```bash
mkdir chat_api
cd chat_api
```

Create the virtual environment:

```bash 
python3 -m venv chat_api_env`
```

If you are using a Mac OS or Unix computer, activate the virtual environment as follows:

```bash
source chat_api_env/bin/activate
```
To activate the virtual environment on Windows, use the following command:

```bash
chat_api_env\Scripts\activate.bat
```

To build this project we will need the following Python packages:

ariadne: Adds GraphQL support to python
uvicorn: An ASGI server
Let’s go ahead and install these packages in our new virtual environment:

```bash
pip install ariadne "uvicorn[standard]"
```
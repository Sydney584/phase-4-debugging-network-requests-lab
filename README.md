# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here


- Add a new toy when the toy form is submitted

  - How I debugged: I first submitted the new toy in the form & checked for any errors in my Dev Tools under Network as well as my console as it did not update as expected. Immediately received 500 error. 500 error means I need to check my Rails server log; I did check and found NameError (uninitialized constant ToysController::Toys): I updated create method in my Toys controller from Toys to Toy. Once updated I checked my Dev Tools again however I recieved a cors error. 
- Update the number of likes for a toy

  - How I debugged: I first clicked like on one of the toys in the browser & checked for any errors in my Dev Tools under Network as well as my console as it did not update as expected. I received this error VM201:1 Uncaught (in promise) SyntaxError: Unexpected end of JSON input at ToyCard.js:21. I also received this error in my terminal 
 
  ↳ app/controllers/toys_controller.rb:15:in 'update' unpermitted parameter: :id The end of JSON message and the js line number indicated to me that I might find the error there. It was missing the render json: toy for my fetch request. I updated and saved the code and the site was now able to updated the likes on my front and back end. 

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged: I received a 404 Network error and in my console received the message that the Delete Route was not found. I checked my routes in my config file and found :destroy was not added as a route. I updated and saved the :destroy route and my app now deletes perfectly. 
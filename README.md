# Technical test

## Introduction

Fabien just came back from a meeting with an incubator and told them we have a platform “up and running” to monitor people's activities and control the budget for their startups !

All others developers are busy and we need you to deliver the app for tomorrow.
Some bugs are left and we need you to fix those. Don't spend to much time on it.

We need you to follow these steps to understand the app and to fix the bug :

- Sign up to the app
- Create at least 2 others users on people page ( not with signup )
- Edit these profiles and add aditional information
- Create a project
- Input some information about the project
- Input some activities to track your work in the good project

Then, see what happens in the app and fix the bug you found doing that.

## Then

Time to be creative, and efficient. Do what you think would be the best for your product under a short period.

### The goal is to fix at least 3 bugs and implement 1 quick win feature than could help us sell the platform

## Setup api

- cd api
- Run `npm i`
- Run `npm run dev`

## Setup app

- cd app
- Run `npm i`
- Run `npm run dev`

## Finally

Send us the project and answer to those simple questions :

### What bugs did you find ? How did you solve these and why ?

Here's the bugs I fixed. I found these bugs would be the most important to fix for the app delivery or for a demo.

- In the project list page, clicking on a project crash the app:

  - `project.name` is undefined in ProjectDetails because `project` is an array.
  - Solution: modify the route `project/:id` in the project controller to return an object in the payload instead of an array by using the Mongoose method `findById` instead of `find`.

- Name not saved when creating users on the people page:

  - When creating a user, `username` is sent in the payload instead of `name`. Indeed the `User` model defines `name`, not `username`.
  - Solution: change the input value attribute to `values.name`.

- Impossible to sign in with a username containing capital letters:

  - The signin auth method converts the username to lowercase to check if the user exists.
  - Solution: don't convert the username to lowercase.

- Updating a user doesn't work.

  - The user is not updated because the submit method is not called.
  - Solution: change the button `onChange` attribute by `onClick`.

- Project doesn't appear in the list of projects after creation.

  - Solution: update the state of projects with the newly created project.

### Which feature did you develop and why ?

The feature I developed is the possibility to have several persons working on a project. I added this feature because it was easy to add and also because it feels like it's an essential feature to have for this app.

### Do you have any feedback about the code / architecture of the project and what was the difficulty you encountered while doing it ?

Feedback / possible enhacements:

- Using redux doesn't seem necessary. React context could be used instead, or a library like [Zustand](https://github.com/pmndrs/zustand)
- Use the data-fetching library react-query. It can simplify state management and bring easy cache managemement, optimistic update for example. The dev tools that comes with it is also an added benefits.
- Don't export function component without name.
- Instead of using custom made date function like `getMonths`, use a library like [date-fns](https://date-fns.org/) as working with date can lead to bug and edge cases that are already taken care of by libraries.
- Signup: no feedback if the user enter password not long enough. We should show the user what are the password requirements.
- On the login page, the signup button should be a link and not a button because it's confusing, it looks like you can sign up even though it's the login page.
- Password should be obscured when creating new users.
- When editing a user, the name is not editable, not sure if it's a feature or bug? Should we allow the user to change their name once he has created his account, or it could be possible by only one user in the company that has "super admin" rights.

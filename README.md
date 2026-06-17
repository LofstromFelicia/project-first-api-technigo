# First API

Replace this readme with your own information about the project. You can include things like:

- Brief description of the assignment
- How you approached the task, what tools and techniques you used, and how you planned it
- If you had more time, what would be next?
- How to run the project locally

## View it live
Every project should be deployed somewhere. Be sure to include the link to the deployed project so that the viewer can click around and see what it's all about.


## Getting Started with the Project

### Dependency Installation & Startup Development Server

Once cloned, navigate to the project's root directory and this project uses npm (Node Package Manager) to manage its dependencies.

The command below is a combination of installing dependencies, opening up the project on VS Code and it will run a development server on your terminal.

```bash
npm i && code . && npm run dev
```

## Instructions
It's time to create your own API!

This project follows on from that, but this time you should model your database using Mongoose models, and persist your data in the database.

It's up to you to decide what sort of data you'd like to store in your database and return from your API endpoints. In the repository, we've included some datasets you can use if you'd like:

** Golden globes nominations 2010-2019
** 500 book reviews
** Avocado sales and average prices from a selection of US states
** 1375 Netflix titles and some data about them
** 50 popular Spotify tracks and some data about the music type

If you'd like to build your own data set - feel free! You could write it yourself, or use AI to help you create some mock data to use. ChatGPT can help with this, just be specific and give it an example. You could also download a dataset from a site such as Kaggle).

In order to get all this data into your database, you'll need to write some code to generate the data - see the 'Making seed data' section further down for tips on how to do this.

Once you have the data stored, you will need to write appropriate RESTful endpoints to return the data and make use of Mongoose Queries to find and return the correct data given the route and any filter params passed.

Making seed data 🧞‍♂️
Seeding a database is a process in which an initial set of data is provided to a database when it is being installed or set up. In the videos for this week, we showed a way to generate a small amount of data, but in this project, some of the JSON files have thousands of rows, so we don't want to have it all in our server file.

Instead, we can load the JSON and iterate over it to generate a lot of entries in our database. Let's say we had a file called people.json, and a Person model and the person model has exactly the same property names as the objects in the JSON file. Then we could write something like this in our server file to seed the database from the JSON:

import data from './people.json'

const Person = mongoose.model('Person', {
  // Properties defined here match the keys from the people.json file
})

if (process.env.RESET_DB) {
  const seedDatabase = async () => {
    await People.deleteMany({})

    data.forEach((personData) => {
      new Person(personData).save()
    })
  }

  seedDatabase()
}
This whole process can be a little tricky and relies on your models having the same keys. Give it a try and if you run into issues, don't hesitate to ask your team, ask in Slack, or post your code on Stack Overflow to get some help!

## Goals
Your API should have at least 3 routes. Try to push yourself to do more, though!
The endpoint "/" should return documentation of your API using e.g. Express List Endpoints
A minimum of one endpoint to return a collection of results (array of elements).
A minimum of one endpoint to return a single result (single element).
Your API should use Mongoose models to model your data and use these models to fetch data from the database.
Your API should be RESTful.
Follow our guidelines on how to write clean code
Deploy your API and add a link to the Readme file of the repository

## Stretch goals
So you’ve completed the goals? Great job! Make sure you've committed and pushed a version of your project before starting on the stretch goals.

## Intermediate Stretch Goals
If you are doing any sort of manipulation after retrieving the data from the database. Try using mongoose to do these operations instead.
Accept filters via query parameters to filter (via mongoose) the data you return from endpoints which return an array of data.

## Advanced Stretch Goals
Try implementing 'pages' using .skip() and .limit() (instead of .slice()) to return only a selection of results from the array. You could then use a query parameter to allow the client to ask for the next 'page'.
Try to create an endpoint that uses mongoose's aggregate function which allows you to use the MongoDB aggregate pipeline. This is super-useful when doing more complex operations on database data, and a lot faster!
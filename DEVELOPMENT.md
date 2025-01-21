# Development Instructions <!-- omit in toc -->

This is a guide to setting up the development environment for this project as well as running and testing it.

- [Setup](#setup)
  - [Make sure you have Mongo running on your computer](#make-sure-you-have-mongo-running-on-your-computer)
  - [Open the project in VS Code](#open-the-project-in-vs-code)
  - [Seeding the Database](#seeding-the-database)
- [Running the project](#running-the-project)
  - [MongoDB in VS Code](#mongodb-in-vs-code)
- [Testing and Continuous Integration](#testing-and-continuous-integration)
  - [Testing the server](#testing-the-server)
  - [GitHub Actions](#github-actions)

## Setup

Clone your repository using your method of choice.

### Make sure you have Mongo running on your computer

For all of this to work, it's critical that you have Mongo installed
and working. This should be true for all the lab computers, but if you want
to also work on your own computer you will need to set it up there as well.

If you're unsure if it's set up and working correctly, try running `mongo` or `mongod` or `mongosh`.
If your MongoDB server isn't running you'll likely get an error
message like:

```text
Error: couldn't connect to server 127.0.0.1:27017, connection attempt failed: SocketException: Error connecting to 127.0.0.1:27017 :: caused by :: Connection refused :
```

(Type `exit` to exit out of the `mongo` tool.)

### Open the project in VS Code

Launch Visual Studio Code, and then choose `File -> Open Folder…`. Navigate to your clone
of the repo and choose `Open`.

You may see a dialog that looks like this if you don't already have the recommended extensions:

![Dialog suggesting installation of recommended extensions](https://user-images.githubusercontent.com/1300395/72710961-bf767500-3b2d-11ea-8ea4-fbbd39c78da5.png)

Don't worry if you don't get the dialog, it is probably because you already have them all installed.

Like in previous labs, click "Install All" to automatically install them.

### Seeding the Database

To give yourself some data to work with instead of starting with an empty database in our development environment, you need to 'seed' the database with some starter data. Seed data and the seed script are stored in the top level directory `database`. To seed the database, move into that directory and run `./mongoseed.sh` (or `.\mongoseed.bat` on Windows). This will take each of the JSON files in `database/seed/` and insert their elements into the `dev` database.

These scripts also drop the database before seeding it so it is clean. You should run this after first cloning the project and again anytime you want to reset the database or you add new seed data to the `database/seed/` directory.

:exclamation: You'll want to create your own seed files and add them to the
`database/seed/` directory for new types used by your project. There
are nice tools like
[next.json-generator.com](https://next.json-generator.com/) that you
can use to easily generate sophisticated seed data for your project.

## Running the project

- The **run** Gradle task (`./gradlew run` in the `server` directory) will still run your Javalin server (a.k.a., the _server side_ of your application), which is available at localhost:4567.
- The **build** task will still _build_ the server (including running Checkstyle
  and all the tests), but not run it.

To recap, **here are the steps needed to _run_ the project**:

1. Go into the `server` directory and enter `./gradlew run`.

### MongoDB in VS Code

We have included the [MongoDB for VS Code](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode) in the recommended extensions. This extension allows you to view and edit things in the Mongo database.

<details>
<summary>Expand for setup instructions</summary>

When installed you will see a new icon in the sidebar, click it and click "Add Connection".

![Screenshot of the Mongo Extension pane](https://user-images.githubusercontent.com/1300395/109005040-1f174c00-766f-11eb-85fb-0de47b22e4ae.png)

That will open a new tab with some options. Click "Open form" under "Advanced Connection Settings"

![image](https://user-images.githubusercontent.com/1300395/109006193-6c47ed80-7670-11eb-8b28-a740f9088d4f.png)

You can leave all the default settings and click the green "Connect" button to add the connection.

![image](https://user-images.githubusercontent.com/1300395/109006728-fabc6f00-7670-11eb-9f15-55a39f7b9674.png)

You will then have the MongoDB server in the sidebar.

</details>

You can explore the databases and collections here. You can click a record to view and edit it.

![Screenshot of displaying the users in the sample MongoDB database in VS Code](https://user-images.githubusercontent.com/1300395/109005447-91882c00-766f-11eb-994e-9a326deee21b.png)

## Testing and Continuous Integration

There are numerous testing options we will use in this course, but for now, you should definitely add: JUnit tests for your server code. We will add other types of tests as we progress throughout the semester.

### Testing the server

From the `server` directory, `./gradlew test` runs the server tests once.

- It generates a report you can find in `server/build/reports/tests/test/index.html`.
- If you use `./gradlew test jacocoTestReport` it also generates a coverage
  report.
  - You can find the report `server/build/jacocoHtml/index.html`, in addition
    to the regular report generated by the `test` task.
  - It will fail if any of the the test coverage metrics is under 80%.
- `./gradlew check` will run both the tests and Checkstyle, which will look
  for style issues in your Java code. The GitHub Actions are set to use
  `./gradlew check`, and will fail if Checkstyle finds any violations, so
  you want to run that locally as well so you're not surprised when you push
  your changes to GitHub.

In addition to these automated server tests, you might want to manually explore the requests and different parameters at the API level. To see what is happening and explore your API, you can use [Thunder Client](https://www.thunderclient.com/). There are more instructions about how to do this in [here](THUNDER_CLIENT.md).

### GitHub Actions

There are a couple of GitHub Actions workflows set up in this repo:

- [Server Java](./.github/workflows/server.yml) - JUnit tests for the server (`gradle-build`)
- [Code Quality/Security](./.github/workflows/codeql.yml) - Checks for code security (`CodeQL / Analyze (java-kotlin)`)
  
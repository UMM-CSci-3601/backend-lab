# CSci 3601 - Backend Lab

In general, we expect you to create a new branch for each task you are completing for the lab. Remember to *commit your changes after each task*, [giving appropriate credit to all co-authors](https://docs.github.com/en/github/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-with-multiple-authors#creating-co-authored-commits-on-github) involved with the work and describing what was done. Frequently stage changes that belong together, commit the changes (with a [meaningful commit message](https://cbea.ms/git-commit/) that includes co-authorship as described earlier), and push your changes to GitHub.

## Lab Goals

- Understand the structure of the queries (HTTP requests) that the server expects
- Understand how the query determines the action taken by the server
- Understand the format of the data in the database
- Understand the format of the responses that the database gives to the server
- Become comfortable navigating and writing the Java code for the server
- Become familiar with and be able to write tests for the server code
- Become comfortable using Thunder Client and the MongoDB extension in VS Code

You'll be exploring ways to filter parts of a simple to-do list using a series of different HTTP requests sent to a server that will communicate with a database to give a response. The server will be able to handle HTTP requests, where a client (or a user) can visit a URL such as `http://localhost:4567/api/users` and the server will respond with JSON-formatted text containing all the users the server knows about, e.g.,

```json
[
  {
    "_id":"588935f57546a2daea44de7c",
    "name":"Connie Stewart",
    "age":25,
    "company":"OHMNET",
    "email":"conniestewart@ohmnet.com"
  },
  {
    "_id":"588935f5597715f06f3e8f6c",
    "name":"Lynn Ferguson",
    "age":25,
    "company":"NIQUENT",
    "email":"lynnferguson@niquent.com"
  },
  {
    "_id":"588935f51c55b55c75a84848",
    "name":"Roseann Roberson",
    "age":23,
    "company":"OHMNET",
    "email":"roseannroberson@ohmnet.com"
  },
  ...
]
```

You will construct HTTP requests to send to the server. You will make the server give back the correct response. In a "real" system you'd have a web client that you use to construct the HTTP requests, and you would want to display the results nicely as part of the application web interface (like the nicely formatted list of e-mails in GMail). To keep this lab simple, however, you'll just view the "raw" JSON that the client receives from the server.

The overarching task of this lab is to implement the desired server functionality. The details are in [LABTASKS.md](./LABTASKS.md).

## Setup

### Clone the project in GitKraken

1. [ ] First, Open [GitKraken][gitkraken]. If you already have a project open, close it or open a new tab.
2. [ ] Click "Clone a repo", select "GitHub.com" and find this repo in "Repository to Clone"
3. [ ] Select where to put it and clone it
4. [ ] You can then click "Open Repo" from the notification that appears to open the repo

### Open the project in VS Code

Launch Visual Studio Code, and then choose `File -> Open Folder…`. Navigate to your clone
of the repo and choose `Open`.

You may see a dialog that looks like this if you don't already have the recommended extensions:

![Dialog suggesting installation of recommended extensions](https://user-images.githubusercontent.com/1300395/72710961-bf767500-3b2d-11ea-8ea4-fbbd39c78da5.png)

Don't worry if you don't get the dialog, it is probably because you already have them all installed.

Like in previous labs, click "Install All" to automatically install them.

### JSON viewer browser extension

If you use Chrome, you may find it helpful to install the [JSONVue][jsonvue-chrome] extension. This will make JSON in the browser look pretty and actually be readable when you visit the different API endpoints.

If you use Firefox, this functionality is built-in, so there is no need to install an extension.

## Running Your project

We use the [Gradle][gradle] build tool to build and run our web application. Gradle is a powerful system for defining, managing, and running tasks that allows us to easily build and test our full web application.

We will be using Gradle from the terminal. You can do this either with the terminal app or the terminal built into VS Code.

From the project directory, you will need to change into the `server` directory with

```bash
cd server
```

From the server directory you can use Gradle to run the server:

```bash
./gradlew run
```

Your server should now be running on port 4567, the port we've configured Javalin to
run on.
Visit it at [http://localhost:4567/api][local] in your web browser.

The server will continue to run indefinitely until you stop it. You can
stop it by typing `Control-C` (often written `^C`) in the terminal where
it's running.

## Testing Your Project

There's very little meaningful logic in the client component of this
project so we're not going to worry about testing the client here.
We'll begin testing the client when we introduce Angular in subsequent
labs.

The server-side portion of this project will be tested using JUnit.
Server-side tests are located in the `src/test/java` directory.

To run your server-side tests: while in the `server` directory, run:

```bash
./gradlew test
```

This will run all tests and output info about the run to a test report "website". To see the report open the file in your browser:

```text
server/build/reports/tests/test/index.html
```

It will look something like this:

![image](https://user-images.githubusercontent.com/1300395/107262491-3cf57780-6a06-11eb-9e5b-68d4491cde47.png)

These test reports are especially helpful when a test fails because you will get the full stack trace there.

When a test fails, you will get a notice in the terminal that there were failing tests along with a path to the report. You can copy that path into your browser to see the report.

## Checking your code coverage

We have [the JaCoCo (Java Code Coverage) plugin set up in Gradle](https://docs.gradle.org/current/userguide/jacoco_plugin.html)
so you can see how well your tests cover (i.e., exercise) your code. The command

```bash
./gradlew check
```

will run the tests followed by the test coverage report generator. This report is a "website" like the one from JUnit above. To see the report open the file in your browser:
Navigate to `server > build > jacocoHtml` and copy the path of `index.html` by right-clicking on it and selecting `Copy Path`.

Paste this path into your browser's navigation bar. The path should end with:

```text
server/build/jacocoHtml/index.html
```

If you generate and look at that report at the start of the lab, you'll see that you start
with 100% coverage of all the `user` files.
You'd like to keep it that way, so check your
code coverage after major stories are finished and look for areas that you're not yet testing. You also want to maintain high test coverage
as you introduce your `todo` code.

:bangbang: `./gradlew check` will fail (and thus block your ability to
merge in a pull request) if your test coverage ever falls below 80%,
so keep an eye on it and take action if it starts to slide down.

:pushpin: The `Main.java` and `Server.java` files are excluded from
the test coverage. They're hard to test without actually generating
HTTP requests, and are mostly configuration rather than "logic", so
we've chosen to not over-complicate the project with attempts to test
that code. You are not obliged to provide any coverage for that. You
should make sure your tests cover things like your `ToDoController` and the like, though.

## Database Instructions

We will be using MongoDB for this lab and future labs. To give yourself some data to work with instead of starting with an empty database in our development environment, you need to 'seed' the database with some starter data. Seed data and the seed script are stored in the top level directory `database`. To seed the database, move into that directory and run `./mongoseed.sh` (or `.\mongoseed.bat` on Windows). This will take each of the JSON files in `database/seed/` and insert their elements into the `dev` database.

Take a look at [DEVELOPMENT.md][development] for more on setting up Mongo and using MongoDB in VS Code.

## Live updates for Gradle test or run

By default, if you're running the server with `./gradlew run` and make changes
to your Java code, you have to stop the server (with `^C`) and restart it for
those changes to take effect. Similarly, if you make changes and want to
see if `./gradle test` or `./gradle check` passes, then you have re-run those
commands by typing them in again.

Happily, Gradle gives us the `--continuous` (or `-t` for short) flag to simplify
these use cases. If, for example, you enter `./gradlew --continuous run`, then
Gradle will automagically notice when relevant files have changed, recompile, and
re-run the project. Similarly, you can have `./gradlew --continuous check` running
in a terminal and it will automatically re-run the checks whenever you save changes.

:bangbang: Make sure the terminals running continuous Gradle tasks are visible so
you can see if, for example, tests fail or the project doesn't even compile anymore.
Otherwise you can end up doing a lot of work that builds on broken code.

## Continuous Integration with GitHub Actions

[GitHub Actions][ghactions] is a Continuous Integration tool that performs
builds of your project every time you push to GitHub.
This is very helpful, as it makes keeping track of your testing
over the lifetime of a project very easy. Having a build/test
history makes it easy to find where, or when, your project broke,
which makes it a lot easier to figure out *why* it broke and get
it fixed and building successfully again.

GitHub Actions is built into GitHub and free to use on open source projects (like ours).

We've done the hard part of setting up the config files for GitHub Actions so it will work automatically. You can find the tests in the "Actions" tab of the GitHub repo.

## Go do the lab

Now that you're all set up, you should be ready to head over
to [LABTASKS.md][labtasks], where most of the actual work of the lab is described.

## Resources

- [Getting started in Javalin][javalin-io]
- [Javalin tutorials](https://javalin.io/tutorials/)
- [Testing Javalin](https://javalin.io/tutorials/testing)
- [Mockito testing in Javalin](https://javalin.io/tutorials/mockito-testing)
- [Best practices for REST interface design][rest-best-practices]
- [HTTP Status Codes][status-codes]
- [More resources](./RESOURCES.md)

[javalin-io]: https://javalin.io
[gradle]: https://gradle.org/
[jsonvue-chrome]: https://chrome.google.com/webstore/detail/jsonvue/chklaanhfefbnpoihckbnefhakgolnmc?hl=en
[labtasks]: LABTASKS.md
[development]: DEVELOPMENT.md
[local]: http://localhost:4567/
[rest-best-practices]: https://medium.com/@mwaysolutions/10-best-practices-for-better-restful-api-cbe81b06f291

[status-codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
[ghactions]: https://github.com/features/actions
[gitkraken]: https://www.gitkraken.com/git-client

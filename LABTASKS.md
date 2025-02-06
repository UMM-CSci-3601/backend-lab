# Lab Tasks <!-- omit in toc -->

- [Notes on notation and structure](#notes-on-notation-and-structure)
- [Exploring the project](#exploring-the-project)
- [Exploring the server](#exploring-the-server)
  - [Use Thunder Client to explore API output](#use-thunder-client-to-explore-api-output)
- [Use GitHub Projects to support Agile development](#use-github-projects-to-support-agile-development)
  - [Setting a milestone](#setting-a-milestone)
  - [Creating a GitHub Projects board](#creating-a-github-projects-board)
  - [Making sure your project is linked to your repository](#making-sure-your-project-is-linked-to-your-repository)
  - [Using the project board](#using-the-project-board)
- [The epics/features of the coding part of this lab](#the-epicsfeatures-of-the-coding-part-of-this-lab)
  - [Tasks you need to do](#tasks-you-need-to-do)
  - [Tasks you should do for the possibility of full credit](#tasks-you-should-do-for-the-possibility-of-full-credit)
- [Questions](#questions)

## Notes on notation and structure

- Questions that you need to answer (as a group!) are indicated with question mark symbols (:question:).
- The [Questions](./LABTASKS.md#questions) section is at the end of this document.
- Tasks that specify work to do without a written response will be bulleted.

Responses to questions should be submitted as specified below (in the [QUESTIONS](./LABTASKS.md#questions) section).

If you're ever confused about what you need to do for a given task, ask.
Similarly, if you're just not sure what's going on or what something does, or
how it does it, please ask! There's a _lot_ going on here, and if you're not
confused now and then you're probably not paying attention. :smile:

Before completing these lab tasks, make sure you have read through [`README.md`](./README.md) and completed the following:

- [ ] 1. Set up your project: [`README.md`](./README.md#setup)
- [ ] 2. Run your server: [run configuration](./README.md#running-your-project)
- [ ] 3. Run your server tests: [testing your server](./README.md#testing-your-project)
- [ ] 4. Check the rubric for the assignment to be sure you understand how you will be graded on your lab work

## Exploring the project

Look over the directory structure of the project before you start
making changes to it, and consider the various tools that we are
using to manage our project.

:question: Answer questions _1_, _2_, and _3_ [QUESTIONS](./LABTASKS.md#questions)

## Exploring the server

Study the server (Java) code in the project you have cloned.
Run it according to the instructions in the
[README](./README.md), including running the JUnit tests.

:question: Answer questions _4_ and _5_ [QUESTIONS](./LABTASKS.md#questions)

> Pro-tip: Searching the Internet or using AI tools to gain additional
> knowledge or support your conjectures about how something works is
> great! It's important that you think about how everything
> fits together and works, though, so don't use these tools as a
> replacement for building your understanding! Blindly pasting
> in answers that you don't really understand will eventually catch
> up with you and create problems.

Look at the tests in `server/src/test/java/umm3601.user` as they can
provide useful information about the intention of various
functions called by `Server` via the `UserController` class.

You should make sure you run the JUnit tests, and it would be
good to deliberately modify some of the tests and see what
happens when they break. (But make sure you restore them to
their passing state when you're done.)

### Use Thunder Client to explore API output

Thunder Client is a tool for debugging the server API output from VSCode.
It aids in checking what the server gives us when we make requests to it, which can be
really helpful when you're trying to debug what your server gives you.

To use Thunder Client (once it's installed), open it from the sidebar.
The icon is a circle with a lightning bolt in the middle.

<img src = "https://user-images.githubusercontent.com/32685970/214179360-2ab176da-dc4f-43f8-8519-4ade1660ef89.png" alt = "Thunder Client in VS Code sidebar" height = 300 />

This should add a button in the top of the sidebar labelled `New Request`, click it.

![Thunder client startup screen](https://user-images.githubusercontent.com/32685970/214179462-d89c738c-7ab3-4ede-99a8-a3c240169884.png)

This should open a window with two columns. In the top of the left column,
there should be a URL bar with a url, (by default, it's `https://www.thunderclient.com/welcome`).
Change that to `http://localhost:4567/api/<the-route-you-want-to-test>` (ie. `http://localhost:4567/api/users`), then press send.

![Thunder client usage](https://user-images.githubusercontent.com/32685970/214179602-528f347b-b825-4446-9c91-d6671d8ad0bb.png)

The response will be on the right column. You can also change the query parameters from this window.

:question: Answer question _6_ [QUESTIONS](./LABTASKS.md#questions)

## Use GitHub Projects to support Agile development

We'll be using GitHub Projects to augment the standard GitHub issues
system with nifty powers to aid in Agile estimating,
planning, tracking, and development. The next two sections
describe the software development tasks you need to complete
for this lab, which all take the form of augmenting the server API with new functionality.
Before you actually start _coding_ on any part of the lab, you
should spend some time using issues and GitHub Projects to capture and estimate
issues and do some planning.

### Setting a milestone

- [ ] 1. Go to the `Issues` tab for your repository
- [ ] 2. Near the green `New issue` button, there is a button-like thing that says `Milestones` (click it)
- [ ] 3. Click the green `New milestone` button
- [ ] 4. Create a milestone for the lab that uses the lab's due date
    1. If you'd like to make multiple, smaller milestones, you may do so
    2. You can write in other information if you'd like, but at least include the one milestone for the lab's due date

Once you have created a milestone, you will be ready to create a GitHub Projects board to act as your visual workspace that is connected to your GitHub repository.

> In future labs and the project, you'll need to create several epics, one for each major feature; implementing most epics will have at three parts that together "slice the cake":
>
> - Implementing the server-side functionality (e.g., adding support for a new API endpoint
>     to the Javalin server code and writing JUnit tests for that functionality).
>
> - Adding the client-side functionality that allows users to access that new server-side work, (e.g.,
>     adding elements including Angular components to the website that allow a user
> to find todos with certain filters activated and writing Karma tests for the components).
>
> - Creating end-to-end (E2E) tests in Cypress that check the functionality from the client all the way through
> to the database and back (e.g., using automated tests to check that when a user selects the checkmark by the
> category filter, the correct query parameters are set and only todos of the correct category are visible).
>
> Since you won't need to do any
> work on the client side in this lab, you won't _really_ slice the cake here, but you should
> be aware that it will be important in the future for your issues to fully slice the cake. In the future, for each epic you should add the issues (tasks) that you think you'll need to complete to provide a full version of this feature. We will give you instructions about how to do that for future labs. For this lab, you will focus on just the
> server-side aspects (testing and implementing server-side functionality).
>
> :warning: One thing you should **not** do is create separate tasks for things like unit tests
> or refactoring. Those activities should be "baked in" to your work flow, and not considered
> separate (and therefore to some degree optional) activities.

### Creating a GitHub Projects board

- [ ] 1. Click the `Projects` tab on your GitHub repository
- [ ] 2. Select the green `+ New Project` button
- [ ] 3. In the popup dialog, choose the `Feature release` template
- [ ] 4. Use the text box at the top of the popup dialog to give your project a reasonable name
- [ ] 5. Click the green `Create` button
- [ ] 6. Create drafts for each lab task in the coding part of the lab
  1. Select the next available text box on the project board
  2. Type the name of your task and press enter
  3. Repeat until all of your tasks have been entered as drafts
  Your screen should look something like this:
  ![Image](https://github.com/user-attachments/assets/2a4e044d-adfb-4842-a35d-0232dab04f80)
- [ ] 7. Now it is time to convert your drafts to issues and link them to your repository
  1. Hover over your next unconverted draft task and click the down arrow on the left of the line (visible near the first issue listed in the image below)
  2. Select `Convert to issue` from the dropdown menu
  3. Search for _your_ repository in the dropdown menu and select it ( :warning: Be careful to choose _your_ repository)
  4. Repeat this for each of your drafts so each of them now has a green circle icon to the left of the title
  Your project board should look something like this:
  ![Image](https://github.com/user-attachments/assets/b4015b48-78fd-40b7-a360-62c08b15fa1f)

### Making sure your project is linked to your repository

GitHub has somewhat inconsistent behavior as far as whether or not linking of the GitHub Project to your specific repository actually happens automatically or not. Since we want to be sure you are having a good experience using GitHub Projects, we are providing some guidance about how to be sure the GitHub Project you made is linked to _your_ team's repository.

- [ ] 1. Navigate back to your repository
- [ ] 2. Click the `Projects` tab on your GitHub repository
- [ ] 3. You should now see the project you just made
- [ ] 4. Select the `Link a Project` button
- [ ] 5. Make sure your project has a checked box in the dropdown
- [ ] 6. Now go to the `Issues` tab in you repository and make sure you have all the issues you added to your project

### Using the project board  

The view that you see will have several views, each focused on a
different way of thinking about the state of your project.

If you haven't already assigned estimates as you went along, now is a good time to think about how difficult you think each task will be and put estimates on each issue.
Once you've created and estimated all the issues, you
should think about which ones you think you can reasonably
do in this lab. This could be all of them, but it doesn't
have to be. You can always add issues to this epic as
things progress, and in general customers would rather see
the set of issues you expect to complete in this epic
_increase_ rather than _decrease_, so being conservative in
your initial planning is probably a Good Thing.

You should move the issues you really expect to do into the `Ready`
track, leaving all the other issues (that you may
or may not do) in the `Backlog` track.

You'll then need to keep an eye on your board throughout the
lab, using it to guide your decisions about what to work on,
updating issues as you make progress, etc. When you start work
on an issue, move it to the "In progress" track.

Whenever you sit down to work on the project, you should be
clearly working on a specific issue. If you feel like there's
something that _needs_ to be done but isn't in an issue, you
should make an issue for that before you start working on it.

When you start work on a new issue, you should create a
feature branch for that issue, and commit your work on that
issue to that branch. Commit messages should refer to that
issue (by number, e.g., `Issue #8`) so GitHub can auto-link
the commits to that issue for you.

When you feel like an issue is complete

- Move that card to the `In review` track
- Issue a Pull Request from your feature branch onto your master branch

Then step away from that issue for a while,
either by working on a different part of the lab, or by
doing something unrelated to Software Design. Then come back
back to that _as a team_ and review the requirements
described in the issue and compare them to the functionality
you implemented. Is the issue _done done_? Are there solid
and complete tests that back up the work? Can you break it?
Have you tried? Would you bet your career (or at least your
next raise) on this working in a customer demo or out in the
field?

If you find bugs, document them, either in the existing issue, or through new issues. Then go back to working in
the feature branch for that issue, and repeat the whole
process.

Once the issue passes review, you should

- Merge the associated feature branch into master by accepting the (perhaps modified) pull request
- Move the issue to the `Done` track (or, fee free to create more tracks as you see fit)
- There are ways to automate the moves through the tracks based on what's happening in GitHub, but we won't look at that in detail for this lab.

Now, you are ready to get started working on the coding part of this lab!

## The epics/features of the coding part of this lab

The initial server (Java) code demonstrates reading in a
collection of (randomly generated) user data, and making it
available (with filtering requested through the query).

Your goal in this lab is to use test-driven development (TDD) to
extend the server's API to support serving 'to-do' data in such a way that lets you see the correct responses. Write JUnit tests for the server functionality you add.

There is a file `data/todos.json` that has several hundred randomly
generated "to-do"s, each of which has:

- A unique `_id`
- An `owner`
- A `status` (which is a boolean - is the task completed or not)
- A `body` that describes the task
- A `category`

Below are the various features we'd like to see you implement in this lab. You should
create an epic for each of the features listed below, adding at issues as appropriate.

### Tasks you need to do

At the very least (necessary to get 85% of the coding part of the lab)
you should implement (and create meaningful server-side tests for) the following features:

- List all the todos
  - [ ] Implement an `api/todos` server-side endpoint, which returns all the to-dos
- List a single todo by ID
  - [ ] Implement an `api/todos/58895985c1849992336c219b` server-side endpoint, which
        returns the single todo with the given `_id`. It should return a 404
        (use the Javalin `NotFoundResponse` class) if there is no todo with the
        specified `_id`.
- Support limiting the number of todos that are displayed
  - [ ] Implement an `api/todos?limit=7` API endpoint, which lets you specify the maximum
        number of todos that the server returns.
- Support filtering todos by their status (either complete or incomplete)
  - [ ] Implement an `api/todos?status=complete` (or `incomplete`) endpoint which lets you
        filter the todos and only return the complete (or incomplete) ones
  - [ ] Note that the "database" stores the status as a boolean, but the endpoint uses
        "complete" and "incomplete". You'll have to implement the (simple) logic that
        transforms the endpoint "language" into the database terminology.
- Support searching for todos whose _bodies_ contain a given string
  - [ ] Implement an `api/todos?contains=banana` endpoint which lets you search for to-dos
        whose _bodies_ contain (anywhere) the given string (in this case "banana").

### Tasks you should do for the possibility of full credit

To get full (100%) credit on the coding part of the lab you should
implement (and create meaningful tests for) these additional features:

- Filter todos by owner
  - [ ] Implement the endpoint `api/todos?owner=Blanche` which returns just the to-dos
        owned by Blanche
- Filter todos by category
  - [ ] Implement the endpoint `api/todos?category=groceries` which returns just the to-dos
        in the `groceries` category
- Allow for ordering/sorting of todos by a particular attribute
  - [ ] Implement the endpoint `api/todos?orderBy=owner` (or `body`, `status`, or `category`)
        which sorts the returned to-dos alphabetically by the specified field

For full credit you also need to support arbitrary combinations
of these filters, e.g.,

```http
api/todos?owner=Blanche&status=complete&limit=12&orderBy=category
```

which would return the first 12 completed to-dos owned by
Blanche ordered by category.

:bangbang: If you have a combination of `limit` with other filters,
make sure you do the limiting step **last** so you don't miss any items.
If you limit first to, say, 10 todos, then you might get down to the
requested 10 todos, but then have later filters bring that down to 7
or 5 or even zero. So make sure you limit **last**!

---

## Questions

Write up your answers to these questions in a Google Doc and turn that in via Canvas on the assignment for this lab.

:bangbang:

- [ ] **Make sure that everyone in your group has edit privileges on the document.**
- [ ] **Make sure that the link you turn in gives us at least comment privileges.**
- [ ] **Include the URL of the GitHub repository for your group at the top of the
      GDoc. This will make it easier for us to figure out which team is "Snoozing Llamas".**

:bangbang: Make sure that your answers address the _purpose_ of
these tools. Don't just tell us _what_ something does, indicate
_why_ we'd want to have it.

- [ ] :question: _1_ What is the purpose of `.gitignore`?
      ([Maybe search for `.gitignore`?](https://www.google.com/search?q=.gitignore))

- [ ] :question: _2_ What role is Gradle playing in the
      project, and what is the purpose of `build.gradle`?

- [ ] :question: _3_ What is the purpose of Github Actions?

- [ ] :question: _4_ Explain what an _endpoint_ is (also often called a _route_). (You might look at the
      [Javalin](https://javalin.io/documentation#endpoint-handlers)
      documentation for some help here.)

- [ ] :question: _5_ What is the purpose of `umm3601.Server` class?
      What is the purpose of the `umm3601.user.UserController` class?
      Explain what happens when a user accesses each of the
      following URLs:

  - [ ] :question: The page `api/users`
    - <http://localhost:4567/api/users>
  - [ ] :question: The page `api/users?age=25`
    - <http://localhost:4567/api/users?age=25>
  - [ ] :question: The page `api/users/588935f5de613130e931ffd5`
    - <http://localhost:4567/api/users/588935f5de613130e931ffd5>

:bangbang: Have your project running (see the README), and use these links -- they should actually work and generate results from your server.

- [ ] :question: _6_ Describe what happens when you filter users by age in the client.

  - [ ] What exactly is the request that is sent to the server?
  - [ ] How does the server react to the request?
  - [ ] What reply does the database send back to the server?
  - [ ] What is the response to the client (What information is included in the response can you see in Thunder Client)?

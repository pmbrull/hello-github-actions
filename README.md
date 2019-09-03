## Welcome to "Hello World" with GitHub Actions

This course will walk you through writing your first action and using it with a workflow file. 

### Step 1: Create a Dockerfile with an ENTRYPOINT

You'll notice at the end of the Dockerfile, we refer to an entrypoint script.

```Dockerfile
ENTRYPOINT ["/entrypoint.sh"]
```

The `entrypoint.sh` script will be run in Docker, and it will define what the action is really going to be doing.

### Step 2: Add the action's script

An entrypoint script must exist in our repository so that Docker has something to execute. Create this new file in `./action-a/`:

```bash
#!/bin/sh -l

sh -c "echo Hello world my name is $MY_NAME"
```

Next, we'll define a workflow that uses the GitHub Action.

### Workflow Files

Workflows are defined in special files in the `.github/workflows` directory, named `main.yml`.

Workflows can execute based on your chosen event. For this lab, we'll be using the `push` event.

We'll break down each line of the workflow in the next step.

### Step 3: Add a workflow file

First, we'll add the bones of the workflow. We'll add the action itself in a later step:

Create a file titled `.github/workflows/main.yml` with the following content:

```yml
name: A workflow for my Hello World file
on: push
```

Here's what it means:

* `name`: A workflow for my Hello World file gives your workflow a name. This name appears on any pull request or in the Actions tab. The name is especially useful when there are multiple workflows in your repository.
* `on`: `push` indicates that your workflow will execute anytime code is pushed to your repository, using the `push` event.

Next, we need to specify a job or jobs to run.

### Actions

Workflows piece together jobs, and jobs piece together steps. We'll now create a job that runs an action. Actions can be used from within the same repository, from any other public repository, or from a published Docker container image. We'll use an action that we'll define in this repository.

### Step 4: Use an action in your workflow

Append the following content to `.github/workflows/main.yml`:

```yml
jobs:
  build:
    name: Hello world action
    runs-on: ubuntu-latest    
    steps:
    - uses: actions/checkout@master
    - uses: ./action-a
      env:
        MY_NAME: "Mona"
```

We just added an action block to your workflow file! Here are some important details about why each part of the block exists and what each part does.

* `jobs`: is the base component of a workflow run.
* `build`: is the identifier we're attaching to this job.
* `name`: is the name of the job, this is displayed on GitHub when the workflow is running.
* `steps`: the linear sequence of operations that make up a job.
* `uses actions/checkout@master` uses an action called checkout to use a copy of our code repository.
* `uses: ./action-a` uses an action named `action-a` by referencing the path to the action's directory, relative to our repository.
* `env`: is used to specify the environment variables that will be available to your action in the runtime environment. In this case, the environment variable is `MY_NAME`, and it is currently initialized to `"Mona"`.

### Your action is about to be triggered!

Your repository now contains everything it needs for the action to be defined (in the `./action-a/` folder) and everything it needs to be triggered (in the `./github/main.yml` file).

The action will run anytime a commit is recognized on the remote repository.

### Seeing your Action in action

You can see the action status reported below, or you can click the "Actions" tab in your repository. From there you will see the actions that have run, and you can click on the action's "Log" link to view details.
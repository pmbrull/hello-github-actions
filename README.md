## Welcome to "Hello World" with GitHub Actions

This course will walk you through writing your first action and using it with a workflow file. 

**Ready to get started? Navigate to the first issue.**


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
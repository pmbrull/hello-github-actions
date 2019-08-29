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

Now, stage and push.
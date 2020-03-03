# Publishing Documentation via CI

The "Publish" button in Studio is a quick and convenient way to publish changes (e.g, updating documentation), but if you are working with a whole team of people, it can become cumbersome to publish manually. To solve this problem, we have a handy CLI package which can automate publishing changes happening via Git.

Start by installing the @**stoplight/cli** package from NPM:

```bash
npm i -g @stoplight/cli

stoplight -h
# The stoplight command should now be available globally
```

Make sure you are in the root directory of the git repository associated with this project.

```bash
cd directory/to/analyze
```

And then run the **analyze** command, passing in the secret token associated with this project (the project token can be found in the project settings publish section).

This will analyze all the design-related files in the project directory, and send the information to Stoplight.
```bash
$ stoplight analyze --token {project-token}
```

> You can add the '--dry-run' flag to the analyze command to see what will be sent to Stoplight, without actually sending the data.

To find your project's CI token, head to the project settings (cog wheel at the top-right of the Studio screen) in your browser, and select the "Publish" option from the sidebar.
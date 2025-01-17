---
title: Tutorial
sidebar: Docs
showTitle: true
---

This tutorial explains the development workflow and best practices, using an example 'Hello World' plugin. We'll go from zero to submitting your plugin to the official PostHog repository.

It's important to note PostHog Cloud users can only use plugins which have been added to [our official integration library](/integrations). Want to add your plugin to our library? All you need to do is [submit it to us for review](#submitting-your-plugin).

## Prerequisites

You will need:

1. A self-hosted PostHog instance (or a local development environment)
2. Some knowledge of JavaScript (or TypeScript)

## The plugin

Every plugin begins with either the PostHog plugin [source editor](#using-the-plugin-source-editor), or a new GitHub repository. In both cases, our plugin source code will look like this:

```js
/* Runs on every event */
export function processEvent(event, meta) {
    // Some events (like $identify) don't have properties
    if (event.properties) {
        event.properties['hello'] = `Hello ${meta.config.name || 'world'}`
    }
    // Return the event to ingest, return nothing to discard  
    return event
}
```

And our config would look like:

```js
[
  {
    "key": "name", // name of key to be accessed using meta. Check value using `meta.config.name`
    "name": "Person to greet",
    "type": "string",
    "hint": "Used to personalise the property `hello`",
    "default": "",
    "required": false
  }
]
```

For information on what code to write and what special functions to use, check out [the overview](/docs/plugins/build/overview) and [the developer reference](/docs/plugins/build/reference).

### Using the plugin source editor

Go to Plugins -> Advanced tab -> Plugin editor -> Start coding.

![Plugin editor location](../../../images/plugins/plugin-editor-location.png)

Then, click on "Edit Source", copy your code and config into the editor, and you're ready to [test the plugin.](#testing)

### Using a GitHub repository

We have a [GitHub template (GH login required)](https://github.com/PostHog/posthog-plugin-starter-kit/generate) which helps you create a new repository with all the right files. There are only two files which make up the entire plugin: the `index.js` and `plugin.json`. Your code goes into `index.js`, and your configuration goes into `plugin.json`.

Other than this, there's the `index.test.js` file for tests, and `package.json` for package dependencies and metadata.

Remember to update `package.json` with the appropriate metadata, like name, description, and maintainer.

Once you've written the code in this new repository, you can run it by installing it locally in PostHog. [See testing for more information.](#testing)

#### Plugin naming conventions

When creating your repository, follow the naming convention of `posthog-<plugin-name>-plugin`. For example, the hello world plugin repository would be called `posthog-hello-world-plugin`.

### Converting a source plugin to a GitHub repository

If you wish to submit your plugin to the official repository, you need to convert it into a GitHub repository. The easiest way to do this is to start with [the plugin template](https://github.com/PostHog/posthog-plugin-starter-kit/generate) and copy your source code into `index.js` and your config into the config field of `plugin.json`. Then update `package.json` with the appropriate metadata, like name, description, and maintainer.

[See submission instructions](#submitting-your-plugin) for how to submit the plugin to the PostHog Repository.

## Testing your plugin

For now, the best way to test plugins is to install them locally. 

- If you're writing a plugin in the Plugin source editor, this is as easy as clicking "Save".
- If you're writing a plugin in a GitHub repository, install it locally using the "Install Local Plugin" option in the Advanced Tab.

![Install plugin location](../../../images/plugins/install-plugin-location.png)

This allows you to tweak your plugin and see that everything works fine.

## Debugging your plugin

Plugins can make use of the JavaScript `console` for logging and debugging. 

These logs can be seen on the 'Logs' page of each plugin, which can be accessed on the 'Plugins' page of the PostHog UI.

## Publishing your plugin

There are four ways to use plugins you build:

1. Publish the plugin to `npm` and install it with the url from `npmjs.com` 
1. You can add it via its repository URL (e.g. GitHub/GitLab)
1. Reference the location of the plugin on your local instance (e.g. /Users/yourname/path/to/plugin)  

    This can be configured in 'Settings' -> 'Project Plugins'.
1. Submit it to the official plugin library. [See below](#submitting-your-plugin). 

Please note that PostHog Cloud users can only use plugins which we have checked and made available via the [official plugin library](/integrations).

## Documentation

If you wish to, you can contribute back to the PostHog community by submitting your plugin to the [official library](/integrations). This means everyone else can use your plugin, including users* on PostHog Cloud!

Before you can submit a plugin to our [official integration library](/integrations), it's important to create some basic documentation by making a README.MD in your GitHub repo. 

You can structure your documentation however you wish, but as a minimum each plugin submitted to PostHog should address the following points:

- What does your plugin do?
- What steps must users take to enable your plugin correctly?
- What configuration options exist within your plugin?
- What requirements does your plugin have?
- Does your plugin need a specific version of PostHog?

## Submitting your plugin

Publishing a plugin enables you to use it on your own, self-hosted instance of PostHog. But you can also submit your plugin to our integration library so that it can be used by other users, including those on PostHog Cloud. 

If you built a plugin inside the PostHog editor, first [convert it to a GitHub repository](#converting-a-source-plugin-to-a-github-repository)

To submit, [email your plugin GitHub URL to hey@posthog.com](mailto:hey@posthog.com?subject=Submit%20Plugin%20to%20Repository&body=Plugin%20GitHub%20link%3A)

Once we get your email, we review the plugin to ensure it's secure, performant, and adheres to best practices. Then, we add it to our official repository and make it available for everyone to use.

## Additional resources

1. Check out [the developer reference docs](/docs/plugins/build/reference) for more information on special functions.
2. Join the [#Contributing channel in our community Slack group](/slack) to ask questions, get support and collaborate with others.

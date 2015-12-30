---
layout: post
title: Lessons in devops
tags: devops
---

For the last 6 months or so I have been responsible for the build & deploy of a product at our company. Below is some of the things I have learned and I think is useful for any project.

## Background

Some key facts:

* We use GIT for our source control
* We use Nant to build, run tests, and package our software
* We use Jenkins and Puppet for continuous integration, deployment and configuration

We have a Jenkins job that continuously polls GIT for new commits and runs our CI. If new commits are found, it runs all the unit tests. If tests pass, we tag (copy the version number and git revision hash) and package our binaries, and copy them to our puppet environment. We then provision a VM and deploy/configure our software using puppet, validate our deployment using the [/status] page (explained in a bit), and run any acceptance tests. If the acceptance tests pass, we run another deployment to our dev environment.

## Jenkins Build Flow

It is a good idea to break down various parts of your CI into multiple jobs. Such as one to package your software and one to run acceptance tests. This allows you, for example, to run acceptance tests independently without having to re-package your software. You then have to just order your jobs.

Out of the box, Jenkins comes with the ability to trigger new builds as part of a job. I did this earlier but found that [Build Flow plugin] to be a better tool. Here are my reasons for recommending it:

* Your entire process is done in one job. Instead of job A calling job B calling job C, it's a job X calling A, then B, then C.
* I found it easier to reference build artifacts between jobs this way. Before, job B and C would copy the "latest successful build" artifacts of job A (you can imagine this leading to a race condition where a new successful build is done between job B and C). Now job B and C would receive the artifact reference by build parameters.

I only used the basic functionality, but I know other teams use more advanced features.

## /status

We actually did two iterations of our product. The first iteration I took a more hands-off approach. One thing that would have made my life easier early on was a status page to know whether everything is working correctly. The development team had more pressing (and interesting) problems to deal with, and I didn't push hard enough. *This was a mistake*. Because it was manual process to validate that the code deployed actually work, it wasn't done. We learned much later that what we deployed wasn't working, **at all**, and at a much more critical time. This was stressful.

This mistake was not repeated for the second iteration as I took a "more dev-y less op-y" role.

A status page should check all your external key dependencies (is the database up? Can you authenticate? Can you write logs?) and report back any errors. Even if your status page is nearly empty, it still brings value - can all your binaries be loaded? Did you configure IIS correctly? A status page is low hanging fruit and brings in so much value.

## settings

In all likelihood you have a settings files. If you use a configuration management tool like Puppet (we use [Puppet Hiera][hiera]), then you know you need to update the hiera configurations before you deploy.

This is not always done.

It's often easy to add a new configuration setting to a project and forget about the deployment aspect. For us, adding a new setting required changing four places: the hiera configuration for the acceptance test, dev, and qa environment, and a release note for another team to add the configuration setting to prod.

We use JSON as our application's setting file. In our /status page, we are adding validation (using [JSON schema][json-schema]) to make sure that all our required settings are there and no additional settings exist (for example, we have a configuration setting that we no longer need). The key here is adding it to the /status page will fail the deployment if we forget a configuration setting. This means we pick up errors at deployment time, not runtime.

## Acceptance test

I'll hang my head in shame and admit that this is one of the last thing I tackled. So you finally deployed something that the [/status] page says is all fine and dandy, Awesome! Does it work? That's a dev team problem ;)

Except it isn't :'(

This step is difficult for a number of reasons. Software is complicated, has dependencies, and what should be in acceptance tests? For me, I decided to keep things simple. Work with the dev team to map out [happy path scenarios] and find ways to verify that things were done successfully. Eventually we may hit situations where this can't be done (reliably, or at all), but we'll cross that bridge when we get there.

## Closing thoughts

When you are in that thin layer between devs and prod/various environments, issues go to you first. We often take for granted how easy it is to place a breakpoint, or check the log, or get a nice stack trace in Visual Studio when things go badly. When things do go badly in dev/qa environments, and you had to do something silly to debug it, raise it as an issue. Catch and resolve them as quickly as possible before the issue hits production - where it may be much more difficult to debug because you don't have access to the machine.

[hiera]: https://docs.puppetlabs.com/hiera/latest/
[json-schema]: http://json-schema.org/
[happy path scenarios]: https://geeking.glassdoor.com/testing-beyond-the-happy-path/
[Build Flow plugin]: https://wiki.jenkins-ci.org/display/JENKINS/Build+Flow+Plugin
[/status]: #status

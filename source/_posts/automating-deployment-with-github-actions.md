---
title: Automating Deployment with GitHub Actions
date: 2020-04-14 17:43:15
tags:
- OSS
- Web
---

This blog used to be automatically built and deployed via CircleCI. I had spent the time setting up the pipelines so that I could ensure that deployment of new versions was as easy as merging a pull request. I was happy with the results, and everything was working. This continued for a few years, and I didn't even consider making changes to the workflow. Eventually, however, I began receiving emails informing me that my implementation based on Version 1 of the CircleCI configuration system would need to be migrated to the latest-and-greatest Version 2 of their system. At this time I was in the middle of a busy season in my life, and despite good communication from the Circle CI team and what I'm sure is a very usable Version 2 system I never managed to get around to migrating my configuration. Eventually my inaction led to the deactivation of the integration I had set up. I want to be _very clear_ that this is *not* CircleCI's fault, it is mine and mine alone.

At the time of writing this deactivation happened a few years ago. In the meantime I've still been writing and publishing, deploying manually. Luckily my build and deploy workflow is simple: a single node command to build, and an rsync command to deploy. Still, I always had intended on re-automating those steps. I am a proponent of the power of automation in my professional circles, I ought to practice what I preach in my personal projects as well as my professional ones.

I've been putting this off for a long time, for no reason other than I wasn't sure what system I wanted to use. Since I had last done the research around providers of CI services the landscape has changed dramatically, and I'd been exposed to a number of them. I've used CircleCI, Bitrise, GitLab's CI system, Jenkins, and some very rudimentary home-rolled `bash` scripts. A notable gap in my stable of experiences was GitHub Actions. I'd heard positive testimonials, so when I finally got around to setting up a more sustainable deployment system I decided to take the opportunity to fill that gap and explore GitHub Actions.

Right away, the GitHub Actions model provided some attractive attributes:

1. Price. Since I operate this blog as an open-source project, using [GitHub Actions is free!](https://help.github.com/en/actions/getting-started-with-github-actions/about-github-actions#about-billing-for-github-actions)

2. Integration with GitHub. Somewhat obvious, but having a one-stop-shop for my entire writing and development workflow is attractive and minimizes the number of systems I need to keep track of over time.

3. Simplicity. I want to focus on writing my content, not building CI systems. I know that being well-versed in DevOps topics makes me a more well-rounded professional, but for something as simple as this blog I'm highly attracted to a CI system that will get out of my way.

Having decided on using GitHub actions, I started by creating a directory in the root of my project: `.github/workflows/`, as specified in [this documentation.](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow#creating-a-workflow-file) I began by giving my workflow a name: `Node.js CI`. I only wanted this workflow to run when code hits my `master` branch, so I used the `on:` specification: 

```
on:
  push:
    branches:
      - master
```

Now that I had specified when to run, I needed to describe what actions to take. I decided to split my process into two jobs: one for generating static HTML files from the markdown files that I actually edit, and another for pushing these generated files to the server hosting this site. To build, I used the following configuration:

```
build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x]
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - run: |
        npm install
        ./node_modules/hexo-cli/bin/hexo generate
    - name: Archive production artifacts
      uses: actions/upload-artifact@v1
      with:
          name: public
          path: public
```

This specification tells GitHub Actions via the `runs-on` statement to use Ubuntu, then specifies that Node.js version 12 should be used for the build process. I chose these settings to match my development environment. The `steps` portion of the configuration file begins with a `uses` command, which takes advantage of the GitHub-provided checkout action to obtain the latest version of the source code. I follow this up using the `setup-node` action to automatically configure the ubuntu environment for use with Node.js. After that, I invoke `run`, passing down a pair of commands which will be run in the ubuntu container. These commands install dependencies based on the packages specified in `package.json`. The command that follows generates the HTML site content from the source markdown, placing it in the `public/` directory. The final set of commands in the building process takes the production artifacts created by the run command from under the `public/` directory and uploads them to the GitHub artifact system, enabling them to be downloaded later by the publish job.

The publish job starts up when the build job finishes, and is configured as seen here:

```
publish:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Download build result
        uses: actions/download-artifact@v1
        with:
          name: public
      - name: Make timestamp
        shell: bash
        run: |
          date > public/deploy_timestamp.txt
      - name: rsync deployments
        uses: burnett01/rsync-deployments@4.0
        with:
          switches: -r
          path: public/
          remote_path: /srv/www/elijahverdoorn.com/
          remote_host: ${{ secrets.REMOTE_IP }}
          remote_user: ${{ secrets.REMOTE_USER }}
          remote_key: ${{ secrets.REMOTE_KEY }}
```

Similar to the build job, I use Ubuntu to run the publish job. In order to ensure that the publish job runs after the build job, and not in parallel, I use `needs` and name the build job as a prerequisite for the publish job. This is critical, since without a successful build job we won't have any artifacts saved to publish. Since we know that these artifacts have been saved and stored, we start by using the `download-artifact` action to grab the result recorded by the previous job. I wanted to make sure that I had a record of when the code was last deployed, so I added a timestamp file to the process by calling the standard unix `date` command, piped into a file under the `public/` directory. This entire directory will be uploaded to the webserver hosting my site. In this way I have a convenient, if crude, way of checking to ensure that deployments succeeded. I then use a community developed action, `rsync-deployments` to push the contents of the `public/` directory to my server. The sensitive information needed to complete the rsync process is set in the GitHub web UI, and is accessed as simple key-value pairs in the actions specification by calling `secrets.KEY`. In the case of my rsync deployment process I just needed the IP address of the server, a user on said server, and an SSH key.

Once I had all this in place, getting a first deployment was as simple as committing the configuration file and pushing to my `master` branch. The Actions workflows kicked right in, running as expected and publishing a new version of my site in under a minute. I confirmed this deployment by checking that the timestamp file that I had set up had changed, pleased to find that it was successful.

This was a resounding success as far as I'm concerned. The process took me about an hour from start to finish, I was impressed by the documentation provided by GitHub and especially thankful for the community packages that were provided. I'm happy to say that I've now had exposure to the GitHub Actions system, and will keep it in the forefront of my mind going forward as a strong candidate for any occasion where I need to automate actions within a GitHub-based project.

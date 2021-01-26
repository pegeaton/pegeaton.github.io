---
date: 2021-01-15T1:12:00-00:00
description: "Ninja GitHub Acions"
featured_image: "/images/chapter-1/sunset-gloucester.jpeg"
tags: ["GitHub", "Github Actions", "ModernAppsNinja"]
title: "Part 1: GitHub Actions in the Modern Apps Ninja Repository"
---
In this blog series, we explore automated workflows supporting the Modern Apps Ninja program. Modern Apps Ninja program administrators and members are encouraged to explore automation and CI/CD to improve the delivery of content and provide experiential learning for community members. The series outline follows:  

* Part 1 introduces the Modern Apps Ninja GitHub Repository, GitHub Actions, the GitHub Actions Marketplace, and demonstrates GitHub Actions Ecosystem workflows as leveraged by the Modern Apps Ninja administrators.
* [Part 2](../chapter-2/) hands-on walk-through and exploration of creating a GitHub Actions.
* [Part 3](../chapter-3.md) explores a more complex GitHub Actions workflow, written to support Modern Apps Ninja member registration; handling secrets and environment variables.

---

### Modern Apps Ninja Community and Repository
The [Modern Apps Ninja](https://modernapps.ninja/) learning community consists of students and professional cloud native practitioners, learning and working together to apply new cloud native technologies skills. A collaborative, community-driven approach to developing and curating content is fundamental to the program mission.  Community members develop the key content, including courses, labs and hackathons focused on modern applications and application platforms.  Experiential learning opportunities are embedded throughout courses and on-going administration of the program.

### GitHub
[GitHub](https://github.com) is more than a source code control system, it is truly a collaboration platform. GitHub is well documented and there are many different tutorials to help you get started.  One of my favorites is the [GitHub Learning Lab](https://lab.github.com/). Check it out, create a GitHub account, and join the [Modern Apps Ninja](https:https://modernapps.ninja/) community!

### Modern Apps Ninja GitHub repository
The content, membership, and overall [Modern Apps Ninja](https://modernapps.ninja/) program is supported through GitHub.  The [Modern Apps Ninja GitHub repository](https://github.com/ModernAppsNinja/modernappsninja.github.io) is a public repository available for anyone to view; the repository contains lab guides, course content, and administrative materials.

<!--
![repoTop](/images/chapter-1/modernapps-top-level.png)
-->
{{< figure src="/images/chapter-1/modernapps-top-level.png" title="ModernAppsNinja Repository" >}}

In addition, the [modernapps.ninja](https://lms.modernapps.ninja/) site is the frontend for the modernapps.ninja learning management system (an edX platform) used to support delivering some of the free courses. The power of leveraging multiple systems is demonstrated throughout the site and course work.

### The need for automated workflows
Automation is necessary to ensure consistent operations and rapid delivery of software supporting the program. Workflows are used to improve quality and efficiency when delivering code to production. For example, the site https://modernapps.ninja/ is fully automated and automatically generated from GitHub. The automation helps with standardization efforts and testing. While there are many CI/CD supporting technologies (Tekton pipelines, Jenkins, etc.) the use of GitHub Actions has a number of benefits, even at the most basic, free subscription level, including:
* 2,000 Actions minutes/month are free for public repositories
* 500MB of GitHub Packages storage free for public repositories
* fully integrated into GitHub
* GitHub Actions workflow run on GitHub hosted virtual machines or self-hosted machines

As students and practitioners of Cloud Native technologies, members often contribute lab guides for a variety of technology areas. Contributors submit content to the GitHub repository and are engaged in continuous integration processes. Contributions take many different forms including creating issue tickets, resolving issues, making pull requests, creating GitHub Actions to support CI/CD, technical writing, and code development.
Experiential learning is a key principle of the program; providing members an opportunity to advance not only their cloud native knowledge but practice skills by actively engaging in the community.

---

## GitHub Actions
[GitHub Actions](https://docs.github.com/en/free-pro-team@latest/actions) are powerful workflow tools built right into GitHub. GitHub Actions workflows are used to automate execution of tasks triggered by events within a repository. GitHub Actions support many different types of event which trigger workflows, including push, pull_request, issues, etc.
![diagramDirectory](/images/chapter-1/diagramDirectory.png)
<!--
{{< figure src="/images/chapter-1/diagramDirectory.png" title="Repository Diagram" >}}
-->
GitHub Actions are located in a subdirectory within a repository. Many different types of events within the repository can trigger an action to runner.
Workflows are located in a .github/workflows directory within a repository; the definition file uses YAML syntax.  The workflow YAML file definitions have an enormous set of options to support CI/CD pipelines. For example, there are many different event types to trigger execution, including push, pull-requests, issue creation, etc.

Let's take a look at the structure of a simple GitHub Actions workflow that does two things: (1) runs a bash command to echo the classic "Hello World!" statement and (2) runs a go program to display "Hello World!".  
<!--
![hello-action](/images/chapter-1/hello-action.png)
-->
{{< figure src="/images/chapter-1/hello-action.png" title="hello-action" >}}
As you can see in the hello-action graphic above, the file contains:
* the name of the GitHub Actions: hello-sample
* the event type: push (when a commit is made in this repository the workflow will run -- event type identifies the trigger for execution)
* jobs: name of the jobs to be queued for execution (in this case only a single job)
* the job name: echo-hello
* runs-on: ubuntu-latest - indicates the type of machine and version to be used for executing the job
* uses: checks out the repository (or download and install packages)
* run: indicates code to execute

We continue to dive deeper into the power and flexibility of the workflow in subsequent articles.

---

## GitHub Marketplace: An Ecosytem of GitHub Actions
The [GitHub Marketplace](https://github.com/marketplace) provides a venue for creators to share GitHub Actions with the GitHub community.

The following graphics show examples of GitHub Actions for secrets.
### GitHub Marketplace Secrets Example
<!--
![marketplace-secrets](/images/chapter-1/github-actions-marketplace-secrets.png)
-->
{{< figure src="/images/chapter-1/github-actions-marketplace-secrets.png" title="GitHub Actions Marketplace" >}}

The marketplace contains a variety of contributions supporting the [hugo](https://gohugo.io/) framework (static website generator).

### GitHub Actions in the Modern Apps Ninja repository
There are many advantages and reasons to use open source contributions:
* standing on the shoulders of giants; leverage the work of others on already solved problems rather than re-inventing the wheel
* providing opportunities for learning
* improving software quality by exposing code to a broad community finds bugs more quickly
* focusing development on what is important to community members

The deployment of the modernapps.ninja website leverages a [hugo](https://gohugo.io/) github actions contribution by peaceiris.

<!--
![peaceiris](/images/chapter-1/marketplace-hugo-peaceiris.png)
-->
{{< figure src="/images/chapter-1/marketplace-hugo-peaceiris.png" title="peaceiris GitHub Actions Contributions" >}}

Here is a screenshot of the GitHub Actions description for the hugo build.

<!--
![hugo-build](/images/chapter-1/hugobuild.png)
-->
{{< figure src="/images/chapter-1/hugobuild.png" title="Hugo GitHub Actions Build File" >}}

As we begin to use GitHub Actions in a production environment, the workflow is a little more complex. Notice the following:
* this workflow is triggered by a push to the main branch of the ninja repository (not on push to other branches)
* a specific ubuntu version is specified as the build machine type; this ensures the repository is run on a matching os version
* the uses: checkout ensures subdirectories in the repository are loaded
* the uses: ensures the latest version of the hugo package is downloaded and installed
* github_token is specified for authentication

## Summary

Modern Apps Ninja program uses GitHub Actions in the repository to support the software lifecycle of program assets. This is all great, but GitHub Actions workflows are code so we need to consider versioning, troubleshooting and test the code. Stay-tuned - part 2 covers these areas as we step through building and testing a workflow.

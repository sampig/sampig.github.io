---
layout: post
title: "Learning Agile: An Introduction to CI/CD"
date: 2019-08-15 12:15:00 +0200
category: tutorial
tagline: ""
tags: [Software Engineer, Agile]
abstract : "Learning Note: an introduction to CI/CD."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Continuous Integration](#continuous-integration)
* [Continuous Delivery](#continuous-delivery)
* [Continuous Deployment](#continuous-deployment)
* [Differences Between two CDs](#differences-between-two-cds)
* [Cost and Gain](#cost-and-gain)
* [Summary](#summary)
* [References](#references)


# Introduction

CI/CD are practices of modern software engineering. CI is short for Continuous Integration, and CD is short for either Continuous Deployment or Continuous Delivery.

Continuous Integration is the process of automatic compiling, building and testing for the preparation of release.
Both of CDs are similar, but still there are some differences. Continuous Delivery is an extension of continuous integration to also focus on building and testing to make releasing more reliable. Continuous Deployment is a process more closed to release. It mainly focuses on automated deployment.


# Continuous Integration

Continuous Integration (CI) is the practice of automated integration of code changes. The process contains automatic detecting, merging, building and testing.

Continuous Integration helps to scale up headcount and delivery output of engineering teams. It allows developers to work independently on features in parallel. When they are ready to merge these features into the end project, they can do independently and rapidly. On the other hand, frequently merging small pieces of code is also a good way to avoid future conflicts. Running regular integration testing is crucial to maintaining software consistency.

CI enables better transparency and insight into the process of software development and delivery. Furthermore, it can bring benefits to the overall organization by enabling scaling, improving the feedback loop, enhancing communication, adoption and installation.

CI best practices include Test Drive Development (TDD), pull requests and code review.


# Continuous Delivery

Continuous Delivery (CD) is a follow-up to CI. It automatically gets source code changes and runs them through building, testing, packaging and other related processes to make sure all the new changes can be released and be ready to be delivered to customers at any given time in a sustainable way.

Continuous Delivery is challenging the traditional means of releasing code. In theory, with CD, codes can be released at any frequencies such as daily, weekly, fortnightly or other requirements. But the goals of CD are automation, efficiency, reliability, reproducibility and verification of quality for the releases. It would be better and easier for bug fixing to release with smaller batches.


# Continuous Deployment

Continuous Deployment (CD) is a release process that uses automated testing to validate if changes to a codebase are correct and stable for immediate autonomous deployment to a production environment. An important thing is that continuous deployment does make sure every deliverable is validated to be deployable. It doesn't mean that every deliverable is always deployed.

Continuous deployment is an excellent way to accelerate the feedback loop with customers and take pressure off the team. Developer can focus on building software and they can see their work go live minutes after they have finished working on it.

Continuous Deployment best practices include Test Drive Development (TDD), single method of deployment and containerization.


# Differences Between two CDs

Continuous Delivery and Continuous Deployment are similar and easy for people to get confused, because they are both abbreviated as CD and share some operations.

Continuous delivery focuses on building the code to be released more quickly, but it doesn't define what and when will be released for production.
Continuous deployment focuses on putting all the changes straight into production. With all the testing and delivery automated, deployment is transformed into a stream rather than a batch of changes to integrated code.

In the delivery phase, developers will review and merge code changes that are then packaged into an artifact. This package is then moved to a production environment where it awaits approval to be opened for deployment. In the deployment phase, the package is opened and reviewed with a system of automated checks. If the checks pass, the package can be automatically deployed to production.


# Cost and Gain

Here are some requirements and benefits of CI/CD from Atlassian.

> <b>Continuous integration</b><br/>
> What you need (cost)<br/>
> <ul>
>     <li>Your team will need to write automated tests for each new feature, improvement or bug fix.</li>
>     <li>You need a continuous integration server that can monitor the main repository and run the tests automatically for every new commits pushed.</li>
>     <li>Developers need to merge their changes as often as possible, at least once a day.</li>
> </ul>
What you gain
> <ul>
>     <li>Less bugs get shipped to production as regressions are captured early by the automated tests.</li>
>     <li>Building the release is easy as all integration issues have been solved early.</li>
>     <li>Less context switching as developers are alerted as soon as they break the build and can work on fixing it before they move to another task.</li>
>     <li>Testing costs are reduced drastically – your CI server can run hundreds of tests in the matter of seconds.</li>
>     <li>Your QA team spend less time testing and can focus on significant improvements to the quality culture.</li>
> </ul>
> <b>Continuous delivery</b><br/>
> What you need (cost)<br/>
> <ul>
>     <li>You need a strong foundation in continuous integration and your test suite needs to cover enough of your codebase.</li>
>     <li>Deployments need to be automated. The trigger is still manual but once a deployment is started there shouldn't be a need for human intervention.</li>
>     <li>Your team will most likely need to embrace feature flags so that incomplete features do not affect customers in production.</li>
> </ul>
> What you gain<br/>
> <ul>
>     <li>The complexity of deploying software has been taken away. Your team doesn't have to spend days preparing for a release anymore.</li>
>     <li>You can release more often, thus accelerating the feedback loop with your customers.</li>
>     <li>There is much less pressure on decisions for small changes, hence encouraging iterating faster.</li>
> </ul>
> <b>Continuous deployment</b><br/>
> What you need (cost)<br/>
> <ul>
>     <li>Your testing culture needs to be at its best. The quality of your test suite will determine the quality of your releases.</li>
>     <li>Your documentation process will need to keep up with the pace of deployments.</li>
>     <li>Feature flags become an inherent part of the process of releasing significant changes to make sure you can coordinate with other departments (Support, Marketing, PR...).</li>
> </ul>
What you gain<br/>
> <ul>
>     <li>You can develop faster as there's no need to pause development for releases. Deployments pipelines are triggered automatically for every change.</li>
>     <li>Releases are less risky and easier to fix in case of problem as you deploy small batches of changes.</li>
>     <li>Customers see a continuous stream of improvements, and quality increases every day, instead of every month, quarter or year.</li>
> </ul>


# Summary

CI/CD are three phases of an automated software release pipeline. They take software from idea to delivery to the end users.
Continuous Integration is the first step in the process. Integration covers the process of merging changes from different developers into a shared main code repository.
Continuous Delivery is the second step. It is responsible for automated packaging an artifact to be delivered to end users.
Continuous Deployment is the final step. It is responsible for automatically deploying and distributing the software to end users.

It is useful and helpful to try to use CI/CD in your project. Why don't you search some CI/CD tools online and try them soon?


# References

1. [Continuous integration vs. continuous delivery vs. continuous deployment](https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment){:target="_blank"}
2. [What is CI/CD - all you need to know](https://codilime.com/what-is-ci-cd-all-you-need-to-know/){:target="_blank"}
3. [What is Continuous Integration](https://www.atlassian.com/continuous-delivery/continuous-integration){:target="_blank"}
4. [Continuous Deployment](https://www.atlassian.com/continuous-delivery/continuous-deployment){:target="_blank"}

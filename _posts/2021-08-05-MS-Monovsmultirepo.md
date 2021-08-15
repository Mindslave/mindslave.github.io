---
title: "Microservices: Mono- vs Multi-Repo"
author: Marius Kimmina
date: 2021-03-08 14:10:00 +0800
categories: [DevOps]
tags: [microservices]
published: false
---

Every organization that wants to adapt a microservice architecture has to inevitably decide to structure their code in either a large Monorepo or in many smaller repositorys, often called multi or poly repository. Not an easy decision to make by any means, that's why this article exists, to help you make an educated decision for your situation. Every organization is unique and what works for one may not work another, that also applies to choosing between monorepo and multiple repositories. 

![image](/assets/images/microservices/MonoVsPolyRepo.png "Mono vs Poly Repo")

Let's first have an overview of the two approaches:

* **Monorepo:** all your code lives in one big repository, all your (micro)services all your libarrys, your scripts, your tests - every piece of code that you have goes into this one repository. To me this first sounded ridicilous and I thought there is no way that any serious organization would follow this approach. Damn I was wrong. Many big tech organizations, such as Goolge, Uber and Twitter, have publicly stated that they use a monorepo internally. 

* **Multirepo:** this can also be called the "normal approach", despite some tech giants embracing the monorepo the vast majority of organizations is using multiple repositories to manage their codebase. Here each service and earch libarry can get their own home, their own repository.

You can already guess that both apporaches have advantages and disadvantages to them.  
We are going to look at both approaches in regards to:

* CI/CD tooling
* Versioning
* Hiring new staff
* Security concerns
* Depdency management
* Enforcing best practices
* Performance

## CI/CD tooling

Since the vast majority of tech companies is following this approach, a lot of tools and solutions already exists. If you follow this approach then chances are that every problem you encounter someone else has already encountered and solved before you. If available tooling is your main concern, using multiple repositories is a safe bet.  
Some tooling aimed at Monorepos, like Googles "Bazel", does exist but it's far fewer and you will be less likely to find someone else who has already solved the same problem that you just encountered. It is possible to use common existing CI/CD Tools, such as jenkins, for a Monorepo but they will require more configuration to do their job. If you decide to go for monorepo you should schedule more time to get your toolchain right. 

## Versioning
Here the Polyrepo again benefits from the fact that most people use multiple repositories. A repository on Github can only have one version number (tag) for the entire repo, which is perfectly fine if every microservice lives in it's own place. You can easily have multiple versions of each and every service and librarry.  
For a monorepo the most common approach is to have 1 version for all your microservices, meaning that if you make changes to 1 service and you bump up the version number, you bump up the version number for all your microservices. This approach requires you to have good tests to make sure that all your services still work together when you make an update. If you have those good tests tho, it's a blessing because you can never fall into trap of depending on older versions of a service a having to maintain multiple versions. When a bug comes up you also never have to check which version of XXX was YYY using. 

## Hiring New Staff

Every Developer out there is probably familiar with using multiple repositories, no extra explanation needed. 

## Security Concerns
Everyone of your developers gets access to your entire codebase, as mentioned before this can be an advantage but I can also be an area of concern. When you hire a new developer you might want to restrict his access to a minimum, which can easily be done when using multiple repositories. In a polyrepo you can decide which service the new software engineer should be working on and then you give him access to only that repository. 


## Dependency Management


## Enforcing Best Practices
An area where the Monorepo truly shines is enforcing every developer to follow best practices, when all your code lives in one repostitory it's easy to setup linting and formating rules that can be enforced through CI pipelines. Since there is only one Repository you only have to set this up once and whenever you change something, you only have to change it once. In a multirepo approach you have to set this up for every repository and everytime you make a change, it has to be roled out to each and every repo, this leaves room for errors.

## Performance


## There Is No Silver Bullet
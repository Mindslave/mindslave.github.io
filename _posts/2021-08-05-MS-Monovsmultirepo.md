---
title: "Microservices: Mono- vs Multi-Repo"
author: Marius Kimmina
date: 2021-03-08 14:10:00 +0800
categories: [DevOps]
tags: [microservices]
published: false
---

![image](/assets/images/microservices/MonoVsPolyRepo.png "Mono vs Poly Repo")

Every organization that wants to adapt a microservice architecture has to inevitably decide to structure their code in either a large Monorepo or in many smaller repositorys, often called multi or poly repository. Not an easy decision to make by any means, that's why this article exists, to help you make an educated decision for your situation. Every organization is unique and what works for one may not work another, that also applies to choosing between monorepo and multiple repositories. 

Let's first have an overview of the 2 approaches:

* Monorepo: all your code lives in one big repository, all your (micro)services all your libarrys, your scripts, your tests - every piece of code that you have goes into this one repository. To me this first sounded ridicilous and I thought there is no way that any serious organization would follow this approach. Damn I was wrong. Many big tech organizations, such as Goolge, Uber and Twitter, have publicly stated that they use a monorepo internally. 

* Multirepo: this can also be called the "normal approach", despite some tech giants embracing the monorepo the vast majority of organizations is using multiple repositories to manage their codebase. Here each service and earch libarry can get their own home, their own repository.

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

### Multirepo
Since the vast majority of tech companies is following this approach, a lot of tools and solutions already exists. If you follow this approach then chances are that every problem you encounter someone else has already encountered and solved before you. If available tooling is your main concern, using multiple repositories is a safe bet.

### Monorepo
Some tooling, like Googles "Bazel", does exist but it's far less and you will be less likely to find someone else who has already solved the same problem that you just encountered. It is possible to use common existing CI/CD Tools, such as jenkins, for a Monorepo but they will require more configuration to do their job. If you decide to go for monorepo you should schedule more time to get your toolchain right. 

## Versioning
### Multirepo
### Monorepo

## Hiring New Staff
### Multirepo
### Monorepo

## Security Concerns
### Multirepo
### Monorepo

## Dependency Management
### Multirepo
### Monorepo

## Enforcing Best Practices
### Multirepo
### Monorepo

## Performance
### Multirepo
### Monorepo

## There Is No Silber Bullet
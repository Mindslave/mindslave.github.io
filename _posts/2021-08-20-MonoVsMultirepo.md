---
title: "Microservices: Mono- vs Polyrepo"
author: Marius Kimmina
date: 2021-08-20 14:10:00 +0800
categories: [DevOps, Microservices]
tags: [Monorepo]
published: true

---

Every organization that wants to adapt a microservice architecture has to inevitably decide to structure their code in either a large Monorepo or in many smaller repositorys, often called multi or poly repository. Not an easy decision to make by any means, that's why this article exists, to help you make an educated decision for your situation. Every organization is unique and what works for one may not work another, that also applies to choosing between monorepo and multiple repositories. 

![image](/assets/images/microservices/MonoVsPolyRepo.png "Mono vs Poly Repo")

Let's first have an overview of the two approaches:

* **Monorepo:** all your code lives in one big repository, all your (micro)services all your libarrys, your scripts, your tests - every piece of code that you have goes into this one repository. To me this first sounded ridiculous and I thought there is no way that any serious organization would follow this approach. Damn, I was wrong. Many big tech organizations, such as Goolge, Uber and Twitter, have publicly stated that they use a monorepo internally. 

* **Multirepo:** this can also be called the "normal approach", despite some tech giants embracing the monorepo the vast majority of organizations is using multiple repositories to manage their codebase. Here each service and earch libarry can get their own home, their own repository.


Google has publicly mentioned that their monorepo contains over 2.000.000.000 Lines of code, that's about 130 times the size of the enitre Linux kernel.

You can already guess that both approaches have advantages and disadvantages to them.  
We are going to look at both approaches in regards to:

* Tooling
* Versioning
* Hiring new staff
* Security concerns
* Tracking Issues
* Dependency management / Code sharing
* Breaking Changes
* Open Source
* Enforcing best practices
* Performance

## Tooling

Since the vast majority of tech companies are following this approach, a lot of tools and solutions already exist. If you follow this approach, then chances are that every problem you encounter someone else has already encountered and solved before you. If available tooling is your main concern, using multiple repositories is a safe bet.  
Some tooling aimed at Monorepos does exist, here are some examples:

* Lerna (JavaScript)
* Bazel (Language Agnostic)
* NX (Angular)

But in comparison, there are still far fewer tools and you will be less likely to find someone else who has already solved the same problem that you just encountered. It is possible to use common existing CI/CD Tools, such as jenkins, for a Monorepo but they will require more configuration to do their job. If you decide to go for monorepo you should schedule more time to get your toolchain right. 

**Winner:** Polyrepo


## Versioning
Here the Polyrepo again benefits from the fact that most people use multiple repositories. A repository on Github can only have one version number (tag) for the entire repo, which is perfectly fine if every microservice lives in its own place. You can easily have multiple versions of each and every service and library.  
For a monorepo the most common approach is to have exactly one version for all your microservices, meaning that if you make changes to one service and you bump up the version number, you bump up the version number for all your microservices. This approach requires you to have good tests to make sure that all your services still work together when you make an update. If you have those good tests tho, it's a blessing because you can never fall into the trap of depending on older versions of a service a having to maintain multiple versions. When a bug comes up you also never have to check which version of *XXX* was *YYY* using. 

**Winner:** It depends

## Hiring New Staff
Every Developer out there is probably familiar with using multiple repositories, no extra explanation needed and no need to introduce them to special tooling around a monorepo. On the other side, if you are using a monorepo, it can be a huge advantage for new developers to be able to see the bigger picture and to get an overview of all the things being developed in your organization. It also enables these new developers to suggest changes and bring up issues to other service which they might otherwise not even be aware of. 

**Winner:** It depends

## Security Concerns
There is one primary security concern when working with a monorepo:
	**Everyone of your developers gets access to your entire codebase** 
As mentioned before, this can be an advantage for onboarding new developers, but it carries risk. When you hire a new developer you might want to restrict his access to a minimum, which can easily be done when using multiple repositories. In a polyrepo you can decide which service the new software engineer should be working on and then you give him access to only that repository. 

**Winner:** Polyrepo

## Tracking Issues

When using a polyrepo approach, this is easy, all the issue that belong to service will be handled in its dedicated repository. It's one of those areas where you it's just clear that Git as well as Github/Gitlab were made for smaller individual repositories. If you want to use Issues in a Monorepo you can use tags for each service and filter through your tags, it's not too hard but it does extra work and room for error.

**Winner:** Polyrepo

## Dependency Management / Code Sharing

With a monorepo all your dependencies are right there in the repo with you, just in another folder. What this means is that you are able to get the newest version by just doing a `git pull`. That can be double edged sword though, if a library gets updated that is used by many services inside the monorepo, every single service has to be ready for this update, if you update a library with a breaking change and you didn't update all your services, they are going to break. While this sounds bad at first, you will also never have a service depend on older versions of a library, meaning that you will never end up in a situation where you suddenly have to maintain two, three or even more versions of a shared library. Also, there is another great advantage here for the monorepo, which deserves its own part.

**Winner:** it depends

## Breaking Changes 

If you are going to introduce a breaking change in a Monorepo, you resolve it for all services in just one pull request. This is one of the biggest advantages that you get from using a monorepo, you can make a breaking change, open that one pull request and get all the engineers on board to discuss the changes in one central place and get every service depending on this shared library to be able to handle the change, no problem. Meanwhile, in a multi-repo version, you have to open a pull request for every affected service and there is no central place for discussion. You might use a separate tool to open such a discussion, but then it's separate from the pull request containing the actual code. Everything gets more messy and complicated here when you are using multiple repositories.

**Winner**: Monorepo


## Enforcing Best Practices
An area where the Monorepo truly shines is enforcing every developer to follow best practices, when all your code lives in one repostitory, it's easy to setup linting and formatting rules that can be enforced through CI pipelines. Since there is only one Repository you only have to set this up once and whenever you change something, you only have to change it once. In a multirepo approach you have to set this up for every repository and everytime you make a change, it has to be rolled out to each and every repo, this leaves room for errors.

**Winner:** Monorepo

## Performance
Once your monorepo gets big it will become unfeasible to git clone the entire repo, you will need to special tooling, once again, to only copy the parts that you want to work on to disk. Obviously, that's much easier an a polyrepo environment, you simply clone the service that you want to work on and you are done, no special tooling required whatsoever. These performance problems can occur on pretty much every aspect of your repo, cloning, building, testing, deploying. Each of these areas can be managed but it requires effort.

**Winner:** Polyrepo

## Open Source

As your organization keeps creating more and new projects, you might find that some of these may be useful for a greater community and for you could also be good to get pull requests and ideas from outside your organization, thus you might consider releasing some parts of your software as open source. This can easily be done when you are using multiple repositories, you just re-host this one repo as open source. When you are using a monorepo, that can be much harder. In the best case you can simply copy that one folder and create an open source repository from it, but then you are still struggling to sync changes between your internal version in the monorepo and the open source version. If the project that you want to open source is more split out through your repo, good luck with that.

**Winner:** Polyrepo

## There Is No Silver Bullet
You might have noticed that I have concluded more wins for the polyrepo. That does not mean that it is necessarily the best approach, it still depends on the weight you give each of these factors and how valuable they are for your organization. What one can realise is that it's mostly big companies that utilize monorepos effectively as they have enough engineers to keep up with special tooling and requirements to keep everything working smoothly. For smaller companies, the advantages of a monorepo might not be worth the engineering overhead that comes with it.


## References
* https://www.accenture.com/us-en/blogs/software-engineering-blog/how-to-choose-between-mono-repo-and-poly-repo
* https://earthly.dev/blog/monorepo-vs-polyrepo/
* https://medium.com/@jaspreet2379/monorepo-vs-polyrepo-for-micro-service-architecture-e258a6e550d7
* https://www.youtube.com/watch?v=nLskCRJOdxM
* https://www.youtube.com/watch?v=W71BTkUbdqE&t=564s
* https://www.youtube.com/watch?v=0_qhdOeMuhk
* https://www.youtube.com/watch?v=MflUMIeADZU
* https://medium.com/criteo-engineering/implementing-build-from-source-with-a-mono-repo-vs-a-poly-repo-3826afc4d233

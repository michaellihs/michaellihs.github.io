---
layout: post
title:  "Curated Q&As from 'Trunk-based development Meetup'"
date:   2021-01-21 21:55:29
tags: [meetup, devops, git, pipelines, continuous integration, continuous delivery]
categories: meetup
---

Last week, I had the pleasure to speak about *Trunk-Based Development* together with ThoughtWorks' [Chris Ford](https://twitter.com/ctford) and [Kief Morris](https://twitter.com/kief). This blog post contains a curated list of questions and answers from the discussions we had during the meetup.

### But we do trunk-based development with pull requests

*There was some irritation around "my definition" of trunk-based development*

> But we do trunk-based development with pull requests!

The short answer maybe is, that even if there are trunk-based development approaches where you have pull-requests in place, we generally try to avoid this for the sake of faster feedback and fully automated continuous integration workflows.

> I disagree with the definition. You can do trunk based with pull requests… my definition:
>
> A source-control branching model, where developers collaborate on code in a single branch called ‘trunk’ *, resist any pressure to create other long-lived development branches by employing documented techniques. They therefore avoid merge hell, do not break the build, and live happily ever after
>
> Does not mean you should not do pull requests

### CI/CD with feature branches

*On the topic of how feature branches complicate your CI pipelines*

> Regularly rebasing the feature branch from the main branch would avoid this late feedback problem.

The answer given in the chat / shown on the slides: No, as soon as you have 2 (or more) feature branches, you don't have continuous integration (because you don't have the changes of the other feature branches in your branch).

### Team size & experience and trunk-based development

> How do you integrate less experienced developers in the team who might not yet be familiar with producing good quality code?

Some of the answers:

* We use pair programming for knowledge-sharing and supporting our junior team members
* We generally provide a safe space to make mistakes and strive for a blame free environment
* Don't misinterpret "pair programming" with "not letting them work on their own" though!

> What is a size of the typical team and what is an average experience level (Seniors vs Mids vs Juniors)? Thx.

* We have teams of about 8 people with about 4 developers
* We always look for a good mix of senior and junior developers - as well as gender and diversity in general

### Code Reviews with trunk-based development

> You probably will go into how to do effective reviews using trunk based dev, if you don't have the luxury to pair program all the time, right?

* we actually do pair programming all the time, it is an essential part of our development workflow
* other than that, we have tech huddles or sessions where we only talk about crucial parts of our code

> I believe that the PR with code reviews brought a huge quality improve. It gives the team (not only to your pair) the option get to know (and agree on) a feature implementation? Having a code review at the end would remove an easy option to agree/disagree on how a feature is implemented (as you might have commits from multiple features).

* I think the problem lies in the "at the end" here - PRs move the feedback to a very late point in your development workflow - we try to enable this feedback earlier with the tools mentioned in the presentation

> * Do you have experience with good methods to do reviews more asynchronously together with TBD? I am thinking especially if the team members are remote and potentially in different time zones and pair programming is not as simple from a logistic point of view.
> * Do you have more examples of code reviews in TBD outside of pair or mob programming?

* I think Kief mentioned a few approaches, e.g. make them part of the review or have dedicated sessions for review.
* With crucial code, we sometimes make it part of our daily tech huddles
* (from a participant) we are using both approaches in our company. The same people commit and push code more often when working with feature branches. Code review is actually a huge problem for us when doing TBD; no context switch for code author, but reviewers have to stop their work
* (from a participant) I remember reading (I think on Peter Seibel’s Twitter?) about how in one team they would review code *after* it got merged to the main branch.  Note that this kind of review emphasizes knowledge sharing as opposed to preventing errors.

### Feature Toggles

> Do you always work with feature toggles when you commit directly into the mainline?

* I would say, it depends, e.g. on the maturity of the project. At the beginning of a project - without any production users around - you probably don't use feature toggles. Later on you might consider them to guarantee a stable prod environment.

> Hm, so does it mean that with TBD I have less than a day to implement a feature for the customer? But with, say Git Flow, I can work on the feature for longer period of time?

* The short answer is people usually have a “feature toggle” that can turn the feature off until it is all done.
* You can still have multiple days/weeks to develop a feature - feature toggles for the win
* The value of TBD and toggles for work that takes longer is that it forces you to have discipline to keep the code clean and working. If I take days to work on something without committing, my code tends to get very messy

> Feature toggle are good and valid solution. But also, here you can get into a similar hell like with the branch-hell! Not every time the features are completely independent, so you need test different combinations of the feature-toggle-states. Managing these could very complex☹.

* As with anything, good design, good discipline is essential

> I think my biggest issue with TBD is that it forces you to use feature-toggles. Using them leads to tech debt.

* I wouldn't say it forces you to do features toggles. It is just that they make a lot of sense with TBD.

> If you want to commit often you will come into the situation where you need FTs, so it forces you.

* Depends on how you plan your feature road map, imho
* Not every commit introduces a new feature, even in the most aggressive greenfield project, I suppose?

### Trunk-based development and very large teams

> Have you ever tried this with 600 developers pushing to master?

* I think if you have 600 developers working on a single codebase you have a problem!
* Google does trunk base development with a lot moe programmers ;)
* Unless you are google or Facebook, which do this, but they have sophisticated tooling
* In most organisations with 600 developers, the software is architected so not all 600 are editing the same parts of the codebase

### Mixing trunk-based development with pull request workflow

> Do you have experience with a mixed model, where you do mostly trunk-based development, but sporadically accept pull requests from “untrusted developers”?

* we do that in our project, which consists of multiple squads. Whenever we make changes in other squad's repos, we send them a pull request and ask for review, since we are not 100% familiar with their code
* still, within a squad, we work trunk-based, since the committers are "trusted" team members

### Life span of feature branches

> * I would say, it all comes down to the question: how *long* does your branch (change set, PR) live. If it is more than a couple of days, the more you diverge from trunk (and also the change set becomes larger and larger) -- therefore you should aim for small and short lived PR
> * But the time is not the factor. It’s the amount of changed code that matters

* I agree to the short-living branches
* I partially agree on the dependency on the size of the change, but at the end, the time is more crucial, since the more time passes the less the chance that the developer still knows what she did many days ago and hence there is a bigger effort to make the required changes

### Shifting to trunk-based development

> Do you have a theory of why most people get so defensive about the feature-branch-based workflow (at least that’s my impression)? It seems to me that the benefits of trunk-based development have been very well-stated for long time, and well-suited for most (at least closed-source) situations already, but it is much less widespread than PRs.

* I think people are familiar with how they’ve learned to work. It’s very hard to change, especially when you see, as Michael is saying, there is so much other things you need to change in how you work. So it seems impossible, or silly, or unrealistic to many people. I remember before working in a team that really understood how to do TDD, I found it too hard to do. And I wasn’t sure if it was something people did in real life, or just a nice idea. Then I joined TW, and saw teams doing it for real, and it was mind-blowing

### Trunk-based development and QA

> Does manual QA have a place in this approach?

* Yes, we have the role of a QA that does exploratory testing on the running software

> How do you handle legal/industry regulations that require a formal review (more formal than PairProgramming) before comitting to main?

* we did not talk about this, but I would say that it often breaks down to traceability, i.e. connect a SW change to a requirement and provide test information and formal

### Database migrations and feature toggles

> How would you handle database-migrations with feature-toggles? Especially when there are data-migrations wich can’t be reverted.

* You need to split the DB-Change into 2 compatible DB-changes. First only add Elements and after feature toggle is changed in prod. 2 DB Change removing the not anymore used old elements. Typ-changes -> introduce new column in step 1 and trigger updating the new column. And in step 2 remove the old column and the trigger
* generally you have to plan ahead for non-breaking changes, e.g. provide old features in parallel and phase them out after new features have been successfully introduced
* The mind change for DB-developer is huge. As the goal for a for DB-developer was to have only a clean DB structure in Production. And the solution is here to  provide this intermediate DB-structure in Production.

### Kent Beck’s “test && commit || revert”, or: Limbo?

> Another, maybe somewhat related, more extreme workflow - have you heard about [Kent Beck’s "test && commit || revert", or: Limbo?](https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864)
> If yes, do you have any thoughts about it?

### Team situations around trunk-based development

> How would you handle the situation when you have head of dev who draws part of his identity from being a hard and pain in the a** reviewer and therefore hates TBD? Any idea of opening up someone like that to the idea?

* if someone draws their identity from being a pain ita, it might be really hard
19:03:12 From Milosz Danczak (he/him) to Everyone : @Yvonne run
19:03:54 From Kief (he/him) [London] to Everyone : Trust is important. If your lead doesn’t trust the team that’s an issue :-/
19:03:57 From Thomas Limp to Everyone : :+1:
19:04:03 From Michael Lihs to Everyone : +1

## Pair programming and trunk-based development

> Pair programming is not an argument for tbd. You can do pair programming also on features. Reality is often more than one dev works on a feature branch

* it’s the other way round - I would argue that pair programming is a prerequisite for TBD or at least makes it much easier / facilitates it. You can easily do pair programming with Merge Requests…

> Doesn't convince me. From experience people are different, some like pp some not. With this you're forcing people into one way of producing good code.

* might also be a question of how you approach people in pair programming. I worked with many different "personalities" in a pair programming way and it requires some communication skills and lots of empathy to make everyone comfortable with it...

### Trunk-based development and code history

> * How its source code history affected with TBD in your experience? (rolling-back features, understanding an implementation without documentation, etc)
> * What would you say about the fact that the source control history gets scattered. Especially if you have serveral people working on different features on the same code base and commiting several times a day. Looking at the history you see a lot of commits. not necessarily connected to each other.

* Is this just a question of tooling? Do you see that as an issue that it is harder to grasp the context of changes; does traceability suffer?
* During the meetup we talked about how proper tooling makes it easier to group changes in your repository and link it to the underlying story.

## References and resources mentioned in the meetup

* [Trunk-based Development Website](https://trunkbaseddevelopment.com/)
* [Kief's Blog Post on Pull Requests](https://infrastructure-as-code.com/book/2021/01/02/pull-requests.html)
* [Martin Fowler on Dark Launching](https://martinfowler.com/bliki/DarkLaunching.html)
* [Kent Beck’s “test && commit || revert”, or: Limbo?](https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864)
* [Book "Accelerate"](https://itrevolution.com/book/accelerate/)

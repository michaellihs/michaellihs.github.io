---
layout: post
title:  "Meetup: CI/CD for relational databases"
date:   2023-02-28 20:00:00
tags: [meetup, ci/cd, databases]
categories: meetup
---

These are my notes from the [DevOps Stuttgart Meetup](https://www.meetup.com/de-DE/devops-stuttgart/): CI/CD for relational databases with [Jasmin Fluri](https://www.linkedin.com/in/jasminfluri/)

The slides for this talk can be [found here](https://de.slideshare.net/JasminFluri/relational-database-cicd).


## A short story about a DB Change

A team with

- 1 DB engineer
- rest: application engineer / developer
- lots of turnover in the team

Tech stack: 
- Spring boot app / relational DB
- CI/CD in place for the app, but not for the DB

Result:
- avoid DB changes whenever possible
- if totally can't avoid, someone needs to write a migration script, send to DBA via mail, executed manually

Problems:

- scripts were not in VCS
- it was never clear, when the DBA applies the change
- no automated (regression) testing

## What happens if DB changes are avoided

see [Database decay and how to avoid it](https://ieeexplore.ieee.org/document/7840584) (Stonebraker et al 2016 )

## What we know about releasing SW

- [DORA report](https://cloud.google.com/blog/products/devops-sre/dora-2022-accelerate-state-of-devops-report-now-out)
- CI/CD profits from losely coupled architecture
- without proper architecture, you don't benefit from CI/CD

### 4 (5) key metrics

- lead for changes (starts with implementing a feature, ends with feature in prod)
- MTTR (time needed to fix a failure in production)
- change failure rate (how often does a deployment fail)
- deployment frequency (the more, the better because features will be slow, low risk)
- deployment reliability is opposite of change failure rate (as a corollary to change failure rate)

## High performing teams and delivery capabilities

High performing teams are able to ship their changes in smaller increments:

- small change, small impact, lower risk, faster feedback
- small changes, easier to undo

## Goal of SW release

- ship small features continuously
- but this is not very common in database development
- DB teams are used to ship large changes, because the automation does not support a process with smaller changes
- that is where CI/CD comes to help

## DB development in numbers

- 50% of DB applications have no QA for database testing (data quality / application testing)
- < 50% have no automated development workflows
- lack of DB automation is one of the most common bottlenecks in releasing changes
- < 30% of DB dev have automated testing and static code analysis

## CI/CD for apps

- dev make change
- dev pushes to VCS
- triggers pipeline
- CI server executes CI pipeline
- pipeline generates new version, replaces an old version
- no state in building the application
  - it is always build from scratch
  - application deployment is usually immutable

## CI/CD for DB

- dev makes change in file, generated code (migration script), exported code (diffs, statements...) - many methods to be considered here
- all the DB changes in VCS have a defined order (in which they later on need to be executed)
- builds always run against a physical instance of a DB
- there is usually / always state involved - a lot of state!!!
  - you need a database ready with a state to test your changes

## 5 pre conditions for DB CI/CD

### 1. Version control

- w/o VCS there is no single source of truth
- dir structure of repo depends on migration tool used
- DDLs for "target state structure"
- usually delta files are used to transition from one DB state to the other

- how do you keep DDLs and migration scripts in sync?

- liquibase only DDLs?
  - renaming is an operation where you need a delta script (renaming can't be derived from DDL only)
- test code and test data (also belongs in repo)

#### BUT: pure file-based dev is uncommon in DB development

- choice of migration tool will affect how you store and order your sourc code
- "passive version control": because active part is in the database
  - risk to forget exporting things that we changed inside the DB
  - changes made to dev environment are also exported correctly
- often, scripts for DB changes are generated from changes made manually to the DB

#### Repeatability of migration scripts

- most of all: atomicity / idempotency of migration scripts
- if not repeatable: if fails midway, we only want to apply the changes that have not yet been applied before sth failed
- if it fails, we want no new migration scripts, but want the 

#### Branching strategy

- DB changes are related to infra changes, build on each other, only make sense in in sequence
- testing on feature branches becomes useless
  - WHY? because the underlying DB state might long have changed
- trunk-based development to the rescue
  - forces people to do small changes
  - testing on main makes sure people know what happens previously
  - only one path to reach "current state"
- access source code in Delivery pipeline
  - breaks (least privilege) single responsibility for CD pipeline
- code reviews with tbd
  - async code review takes lots of time
- long lead time for merge requests

### 2. Static code analysis

- before linting & SCA: you need coding guidelines
  - save time discussing coding guidelines in MRs (let the linter do the work)
- not much adoption of linters for SQL / DDL
  - assumption: too big of a rule set for linters

### 3. Database migration tools

- initial state: applying initial DDL
- after that: applying DDL & DML
- database schema evolution
- 2 tools: flyway and liquibase
- don't write a migration tool yourself
- if you use Liquibase: don't use XML (or JSON or YAML)


### 4. Automated DB tests

- projects without automated testing spends 25% of team capacity for manual testing
- possibility 1: app code for DB testing (junit and dbunit)
- possibility 2: unit testing in the database (pgTAP, utplsql)

### 5. Decoupled codebase

- between app and DB
- coupled code bases require organised releases across teams
  - every release becomes a big issue
  - this is not CD!
  - people have to wait for others to release their changes
- why is it important to deploy changes at any time?
  - we don't wanna work outside business hours
  - reduce stress
- abstraction layer
  - between app and DB - DB API
  - needs to be versioned
  - no direct access to a table
- see DB schema as an API, changes to it can be breaking for consumers
  - if DB changes, the app has to adopt the changes
- decoupling means: provide a versioned access layer
  - app A can access version 1 of my DB API
  - can switch from version 1 to version 2 of DB API when ready
- API could be views and procedures that can be versioned

## CI/CD pipelines for databases

- development environment by the click of a button
  - if this deviates a lot from the target, production DB, causes pain --> "DB version drift"
  - no infra resemblance necessary, schem resemblance is sufficient (eg. Docker container)
- check code, before you deploy it
  - applies to coding guidelines
- store artefacts in artefact storage after CI
  - no more repo access in CD
- do a backup of your environment before you deploy a change
  - with a DB you can't "deploy" a previous artefact - your data will be gone without a backup
- deploy SQL code

## Effects of CI/CD in database development

- not automating integration and deployment is a change preventer
  - releases tend to get bigger
- with automation, have independency to deploy changes
  - without relying on other people
- number of deployments increased significantly after introducing automated pipelines
  - with more releases, changesets got smaller
- Change failure rate decreased by 75% with automation pipelines
- Cognitive load of developers decreased with automation pipelines
  - interviews
  - less stress

## Questions

- code examples for DB tests
  - is there a reason to test, if the DB is rather simple?
  - there is more than tables in a DB, that requires testing
    - eg. assure that the procedures I write do what I expect
- indication for DB abstraction layer
  - if DB and app have different release cycles
  - [Book "Refactoring databases"](https://martinfowler.com/books/refactoringDatabases.html)
- differences between nosql vs relational DBs when it comes to CI/CD and migration
  - most nosql don't allow for much functionality to be developed in the DB
- what is a good boundary between DB config (eg. managed in Terraform) / and DB schema (managed in DDL / SQL)
  - TF everything that's not in the schema eg. users









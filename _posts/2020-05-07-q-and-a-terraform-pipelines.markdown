---
layout: post
title:  "Currated Q&As from 'Getting Started with Terraform Pipelines'"
date:   2020-05-07 21:55:29
tags: [meetup, devops, terraform, pipelines, continuous integration, continuous delivery]
categories: meetup
---

Today, I had the pleasure of being the speaker for my very first ThoughtWorks meetup. The topic was "[Getting started with Terraform Pipelines](https://www.meetup.com/de-DE/devops-stuttgart/events/270362303/)" and due to the current (Corona) situation it was an online-only event. This post is a (curated) summary of the questions and answers that were written in the chat, since I think they contain a lot of things to be learned about Terraform and infrastructure as code.

**Will you be doomed if state gets somehow lost? Can you recover from a state loss?**
* you should store your state in a high durability place, such as S3
* not exactly but close enough - [terraform import](https://www.terraform.io/docs/import/index.html) can help
* Terraform gives the possibility to import existing ressources into a state
* But there is no import all yet … it is per resource (at least last I checked)
* not every resource can be imported
* You should take care of import. If the provider is implemented badly it won't help you very much 
* you can import existing infrastructure into a state
* You should backup your state file aswell :-) maybe work with snapshots before/after apply 
* the state in the end is a JSON File. If everything else fails, things can fixed by editing the file and reuploading it, although this is a recipe for pain


**Does terraform give a graphical representation of the infra getting created like for e.g cloud formation designer provides?**
* State described well here. Also the graph tool https://thorsten-hans.com/terraform-state-demystified

**What happens if resorces were changed outside terraform?**
* Terraform will change them back to what is described in the configuration
* Sometimes this means destroying and re-creating a resource

**Followup question: What if your state loss happens because a state apply failed and you have an intermediate state? When a state apply fails because AWS rejects the request?**
* terraform usually stores backup file while apply

**Do you persist the state then?**
* the state needs to be persisted in any case. Because if you don’t two different people applying terraform code would recreate resources

**On which service does terraform run on?**
* Important to mention it doesn’t run all the time - it’s not a service or something. It is a simple binary that can be run on any command line, e.g. run in a pipeline, makes changes and exits
* like this, you can easily run it in any pipeline on any CI/CD server

**Is there a possibility to snapshot tf-state in a storage-account?**
* for Azure: generally yes, see this [documentation](https://docs.microsoft.com/en-us/rest/api/storageservices/creating-a-snapshot-of-a-blob)
  * for Azure, there seems to be an [open GitHub issue](https://github.com/hashicorp/terraform/issues/18284) for this
* Recommendation for state version is to enable it on the remote storage, e.g. S3 supports versioning of files
* terraform cloud is free for state storage as well
* usage of Terraform cloud might be dependent on the privacy policies of your company / client though

**How do changes to resources, which were triggered manually, affect the terraform state?**
* if the resource was manually created, it is not represented in the Terraform state at all
* if it was created by Terraform and then manually changed, the next Terraform apply will bring it back to the automatically created state

**Which systems (providers) are supported by Terraform**
* These are the supported systems that Terraform can configure: https://www.terraform.io/docs/providers/index.html


**tdd is kinda impossible with terraform**
* terratest is ok to use, but doesn't help much in tdd
* It depends on how you consider TDD, my team have written tests and then written the terraform to deploy working code to make the tests go green - this is out of scope of this talk but we have run talks on infra testing before and will again

**Terraform vs. Pulumi - which is gaining more traction these days?**
* terraform has a bigger offering of providers, pulumi is in very active development as well
* pulumi is gaining traction
* if you are starting from scratch I would encourage to check both and see which one fits your use case better
* My team have focused on Terraform as it’s a common language and tool set to work with Github, K8S and AWS

**What does “Go for immutable infra” mean exactly? Other than a DB**
* a DB is the opposite of an immutable piece of infrastructure, since it mutates over time
* immutable infra would be deploying infrastructure that is not changed until the next deployment. For instance, all the networking is based on the TF code reflecting the end state.
* another example would be a serverless function or a container. You don't update or patch it in place, you just replace it every time with a completely new instance when it gets deployed

**What does it mean to split state? Is this an outcome of infra modularity?**
* splitting state means that you have different state files for different parts of your infrastructure
* e.g. this can mean that you have a different state for each environment or even for each service's infrastructure

**should we split state for each environment?**
* YES

**Where do you run terraform code, in azure devops, azure container or azure shell, or local laptop?**
* basically you can run it from every place that can run a go binary
* For my team we run all terraform code in pipeline only, we do not run terraform locally at all and have not creds to do so. My team make an active choice to do this. Our CI is GoCD running in K8S containers


**Is the concept of pipelines and stages applicable with other tools than Terraforn? E.g. with Ansible?**
* yes, though the declarative nature of terraform tends to make describing the end state a bit easier
* Ansible makes much more use of patching resources or configuration in place
* This makes staging in general rather hard

**It looks like your terraform code for many services is all in a single “infra” repo - was there any intentional decision to do this instead of putting the terraform scripts alongside the service code inside each services repository? What drove that decision?**
* we had infrastructure in place that we needed to preserve. Starting with what we had and refactoring in small steps seemed like a good approach.
* Generally you should split your infrastructure in smaller junks and test and apply them seperately
* Still seperation can raise new issues, like dependencies and remote references

**do you use [atlantis](https://www.runatlantis.io/)?**
* We’ve just started using Atlantis - it’s nice :D
* Not yet, we are considering it in the future


**Do you use HachiCorp Vault for secrets or some parts of CI server for secrets?**
* Currently we are using K8S “secrets” we will be moving to AWS secrets store “soon” and then in a while we will be standing up vault
* We are using the Azure keyvaults, but only use it for deployments, not for runtime, since it seems to be too slow for "real time access"

**What’s the best place to version control infrastructure code, in repo with application code or in separate repo?**
* I think the answer is “it depends” and it also depends how tightly linked your code and infra are

**Did you discuss splitting state even more, e.g. one statefile per service? Why did you decide against it?**
* we considered to do so, but agreed against as a first step, mainly to keep things simple and to have an easy orchestration of our bootstrapping process

**monorepo vs micro repos with code?**
* see above: it depends on the use case
* as a rule of thumb: smaller is better

**Do you use tools like test [terratest](https://github.com/gruntwork-io/terratest), [kitchen-terraform](https://newcontext-oss.github.io/kitchen-terraform/), [validate](https://www.terraform.io/docs/commands/validate.html)? or some part of GoCD can help with testing?**
* My team currently tests with [tflint](https://github.com/terraform-linters/tflint) and terraform validate, we have additional in pipeline tests to ensure resources are available and configured correctly.
* We are also looking at [awsspec](https://github.com/k1LoW/awspec) for testing

**Is there anyone who experienced with Jenkins for CI pipeline? How good is Jenkins about Terraform CI pipelining?**
* works good
* any CI tool can be used to be honest, though I’ve seen many centralized jenkins instances that are exceedingly hard to use

**I see a lot of azure specific configuration? I was expecting something more platform independent so you can describe the state independent of where it is applied (Azure, AWS, etc)?**
* the examples were taken from Azure, since I am currently working with it
* you cannot use Terraform to abstract the cloud provider API and it would make no sense, since the cloud resources strongly vary from provider to provider
* Terraform scripts are always cloud specific

**Have you looked at [terragrunt](https://github.com/gruntwork-io/terragrunt) at all? It can handle splitting and templating of environments. Well worth a look if it fits your needs**
* +1 to terragrunt, can be used effectively to address some terraform pain points
* Terragrunt is something that we are looking at next week to fix some of the pain of copy pasted variables
* I think terragrunt will be obsolete in some time as tf adds those teatures


**Why not to split states down to each independent servece?**
* Why not split to each service: There are tons of interdependencies you can create between services and passing variables back and fourth becomes a PITA
* My team uses both terraform data calls and terraform remote_state as data sources to pass information between small pieces of terraform code

**how "cloud specific" is the resulting terraform code? I'm asking since my team might have to e.g. provision k8s and other services on multiple cloud service providers.**
* very specific, since resources change by clouds
* The k8s terraform will apply to most versions of k8s, but different cloud providers provide different resources as Ashish says
* The concepts however are always the same, resources / data objects same templating engine etc
* If you want to create a kubernetes cluster, just take a look at the differences between the terraform resource “azurerm_kubenretes_cluster” and “google_container_cluster” ... you have to handle ALL those differences yourself


**did you setup the pipeline(s) for terraform right away or after your infra reached a certain state?**
* My team went straight to pipeline never ran it locally. But we where starting with a Greenfield setup and we had the opportunity to make a clear choice of pipelines only
* We have sometimes needed to do interactive terraform but only a few times in the last 6 months. We do this from the CI/CDs agents
* We actually tag all our infra with the unique pipeline ID as well so we can trace AWS -> pipeline -> code

**Where/how do you publish the various terraform packages?  Is it just pushing a docker image to a registry every time?**
* For modules, you can run a [terraform registry](https://www.hashicorp.com/blog/hashicorp-terraform-module-registry/) or just use git but we are not at this stage yet
* when it comes to the [Azure DevOps pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops), you can use the [pipeline artifacts](https://docs.microsoft.com/en-us/azure/devops/pipelines/artifacts/pipeline-artifacts?view=azure-devops&tabs=yaml) to store the packages. But those are not (only) modules, but also binaries, scripts and Terraform plans

**How do you build the pipeline itself? Also with terraform?**
* We actually use yaml to define them in git and then have good sutopull them
* There is a [GoCD terraform provider](https://github.com/beamly/terraform-provider-gocd) but it’s a little trickier to automate for us
* We've actually created AWS CodePipelines with Terraform, which then later runs Terraform.. works
* we build pipelines with terraform using [aws codepipeline](https://aws.amazon.com/codepipeline/) and [codebuild](https://aws.amazon.com/codebuild/)
* Currently the [Azure DevOps Terraform provider](https://github.com/microsoft/terraform-provider-azuredevops) is being developed. So for the moment it is not stable and a lot of resources within Azure DevOps unfortunately can't be terraformed.

**Can we elaborate more on why “the download terraform package” is needed in every stage?**
* In [Gitlab CI/CD](https://docs.gitlab.com/ee/ci/) you can use [“artifacts”](https://docs.gitlab.com/ee/ci/pipelines/job_artifacts.html) to store the package…
* we do this, since many modern CI servers have stateless stages. This means that if you want to pass anything in between stages, you have to persist it to some external storage on the producing stage and then restore it again on the consuming stage.

**What if the "test" stage in prod fails?**
* That’s an interesting question Steffen, and your team should decide if it’s an alert etc
* we don't have any automated rollback in place and it might be hard to achieve with infrastructure code

**When automating terraform plan/apply in a pipeline (no manual approval), do you put any restrictions on? (i.e. don’t automatically apply if there are any destroy’s in the plan)**
* since we went with a gated approach, we don't do this
* using locks might be a step in this direction

**Are you running the pipeline from non-master branches? If, what happens there?**
* We always run from master
* At ThoughtWorks, we have a strong opinion on branches and mostly go for trunk-based development

**do you run azure rm templates from teraform/terragrunt?**
* sorry, I have no ideas what this is

**How do you know which version or git commit of the terraform scripts was used to build the current prod?**
* We tag things with the pipeline ID which is made up of the git short hash + pipeline run count
* We also do some AWS tricks to have the pipeline ID embedded in the AWS role assume process that we use
* Most CI systems provide the commit hash of the repository for the current build. I.e. you can just tag a revision with the date and environment it's been deployed to

**For “proper” unit testing with all dependencies in memory, it’s looking compelling on prem by combining Terraform with the golang vCenter [vcsim](https://github.com/vmware/govmomi/tree/master/vcsim) tool where you can replicate a vCenter set of resources locally. Is anyone aware of such simulation tools for any of the public clouds?**
* There are some AWS stub tools, I’ve never looked at them
* take a look at [localstack](https://github.com/localstack/localstack)

**What exactly caused your complete infra outage?**
* Basically applying a new resource against a new (wrong) terraform state.

**How are you guys managing state migrations? For example, I want to rename a module? I want to rename a module `module.x.something` to `module.y.something`. We’ve always had to do this “by hand” before our pipeline runs with terraform state mv. Any hints on how to get this in a pipeline in a "migrations”**
* [tf state mv]() works well


20:16:12	 From Steffen Gebert : great question!
20:16:17	 From Sean Mitchell : Gah … enter too early :D
20:17:06	 From Hannes B : Caused, not cost


20:17:22	 From Anja Kammer : Personday, not Manday ;)
20:17:28	 From Michael Fait : Yeah sure … corrupted state ...
20:17:32	 From Michael Fait : :)
20:17:42	 From Hannes B : Thanks


20:17:49	 From Yevgen Batovskyi : so there is a way to provision resources via powershell modules/integration with UI via Azure resource templates (similar to cloudformation on AWS), when you develope infrastrcuture with teraform you are not always have chnages from Azure in modules


20:18:04	 From Hannes B : Do you have an opinion on terra grunt?


20:18:05	 From Benedikt Klein to Michael Lihs (Privately) : Hi Michael, wollte dich gerade nicht aus deinem Redefluss/Gedanken bringen. Stehe ich gerade auf dem Schlauch? Kennen wir uns wirklich? Oder kennst du nur einen anderen Benedikt Klein? Wohne in Köln. :)


20:18:10	 From Engie Tawfik (ThoughtWorks) : @Sean Mitchell, grep and sed possibly? :D


20:18:14	 From Yevgen Batovskyi : and I was interested how do you integrate azure rm?


20:18:24	 From Ashish Mohite : I've done a complete nested module renames


20:18:40	 From Matthew Cosgrove : For “proper” unit testing with all dependencies in memory, it’s looking compelling on prem by combining Terraform with the golang vCenter vcsim tool where you can replicate a vCenter set of resources locally. Is anyone aware of such simulation tools for any of the public clouds?
20:18:46	 From Sean Mitchell : Grep and sed … no :D terraform state mv works fine, but its always outside of our pipeline. We are adding it to our PRs right now to say “Hey, before we merge this PR into environment, do these state moves”


20:19:01	 From Steffen Gebert : But how to "terraform state.." when you don't have access to the state / infra, because only your CI has @Ashish


20:19:22	 From Sean Mitchell : It also happened recently when azurerm renamed some resources from like azurerm_hub_dps to azurerm_iothub_dps … terraform wanted to erase and recreate
20:19:36	 From Ashish Mohite : i did it manually
20:19:42	 From Ashish Mohite : not in ci
20:20:01	 From Steffen Gebert : that then, of course, breaks the concept of only CI has access


20:20:28	 From Hannes B : 🙏
20:20:35	 From Ashish Mohite : yeah


20:20:36	 From Tigran Arabadjyan : what about rollbacks with terraform?


20:20:36	 From Stephie (ThoughtWorks) : Get Michaels slides here: https://github.com/michaellihs/meetup-2020-05-07-terraform-pipelines/blob/master/presentation.pdf


20:20:40	 From Steffen Gebert : but I don't see a good alternative, except that you have a pipeline which allows to do such renaming


20:20:56	 From Sascha Diefenthäler : Big appreciation for the talk!
20:20:56	 From Michael Fait : 👍👍👍
20:20:57	 From Alberto Enriquez de Salamanca : Thanks, very good structured
20:20:58	 From Christina : thank you very much
20:21:01	 From Krystian : Thank you
20:21:01	 From Sean Mitchell : Thanks!!! :)
20:21:05	 From Mathilda : Thanks
20:21:07	 From Ashish Mohite : thanks 😊
20:21:08	 From Dominic : Awesome!
20:21:11	 From Steffen Gebert : Thanks!
20:21:11	 From  Sebastian : Thanks!
20:21:12	 From Benedikt Klein to Michael Lihs (Privately) : Aber fand deine keynote trotzdem sehr gut! :)
vllt sollten wir uns auf Xing/linkedin vernetzen, dann hast du zwei Benedikt Kleins in deiner Liste! ;)
20:21:12	 From Taner Durkut : Thank you so much :)
20:21:13	 From Jan Krajewski : many thanks
20:21:13	 From Felix : Thanks :)
20:21:15	 From Jan Krajewski : bye
20:21:15	 From Jette Bakemeier : Thank you!
20:21:18	 From Laura : thank u :)
20:21:19	 From Franck Brignoli : Great talk! thanks
20:21:20	 From Ronny : thanks
20:21:20	 From Engie Tawfik (ThoughtWorks) : Thanks :)
20:21:22	 From Thomas Feucht : thank you!
20:21:23	 From Matthias : thx
20:21:23	 From Tim Fletcher : I would do the rename via a temp pipeline
20:21:23	 From Achim : Thank you!
20:21:25	 From Till : Thanks.
20:21:26	 From jeroen : Thank you
20:21:26	 From Yevgen Batovskyi : awesome!! thank a lot TW
20:21:27	 From Jonathan Nowak : Thanks :-)
20:21:28	 From Mo El Sherif : Thanks for a great talk
20:21:33	 From Jenna (ThoughtWorks) : Thanks for joining everyone! :)
20:21:44	 From Michi : Thank you guys!
20:21:48	 From Rafael Rezende : Thank you very much!! I really enjoyed the presentation!
20:21:48	 From Daniel @d_pisanu : cheerio!
20:21:48	 From Jerko Horvat : Thank you!
20:21:54	 From Till : Have to go grab some Pizza now :)
20:22:00	 From Andreas Härpfer : And also thanks to Tim for answering questions in the chat!
20:22:05	 From Anna Sukiasyan : 3 dots -> save chat
20:22:07	 From Rafael Rezende : Good question, because there are good questions and answers here :-)
20:22:51	 From Dominic to Michael Lihs (Privately) : Danke auch nochmal für deinen Blogpost an Fred
20:23:05	 From Michael Lihs to Dominic (Privately) : gern geschehen :) hoffe, es hilft
20:23:25	 From Stefano Salvatori : Thank!!!! For the presentation !
20:23:36	 From Dominic to Michael Lihs (Privately) : Oh, ja und wie. Bin sicher du bekommst es mir ;-)
20:23:43	 From Dominic to Michael Lihs (Privately) : mit
20:24:40	 From Marcus Spiering : thanks, have a nice evening


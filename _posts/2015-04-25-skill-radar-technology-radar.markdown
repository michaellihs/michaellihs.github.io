---
layout: post
title:  "Skill Radar & Technology Radar"
summary: "How to keep track of your skills, innovation and learning."
date:   2015-04-25 13:30:00
categories: learning
---

As a (web) developer, keeping track of all innovation that happens around you can be a hard job. Figuring out which technologies to adopt and which to skip, documenting progress in adoption and communicating it with team mates and colleagues at work is something I was looking for a good solution for quite some time. Inspired by the [Technology Radar from Thoughtworks] I had a nice conversation with Heiko from [Emendare] during one of my coaching sessions with him and I wanted to share some insights and methods we came up with. We recently kickstarted a Technology Radar and a Skill Radar in our team - here is a short summary of how it works and what we did to create them.


## The Technology Radar

The goal of a *Technology Radar* is to visualize which technologies you, your team or your company use and in which state of adoption they are.

As an example, a representation of your radar can look like this

![Example of a technology radar](/assets/images/skill-radar/technology-radar.png)

The radar in the example shows

* different *clusters* of technologies -- by different colors of items
* different *state of adoption* -- by the distance of an item to the center
  * *on hold* -- not currently under review or "don't want to use"
  * *assess* -- check whether it's worth spending more time on it
  * *trial* -- we currently give it a try and see whether it makes it into production
  * *adopt* -- we agreed upon using it in our daily work / projects / production
* changes over time -- by different shapes of items
  * *circle* -- no change since last update
  * *triangle* -- changed since last update
* WIP limits -- e.g. do not allow more than 4 items in each cluster in each state


### How to create your own Technology Radar

Remember that you can create a Technology Radar for yourself, your team or even a whole company. We will describe the steps for a Technology Radar for your team . Setting it up for yourself should be easy. Setting it up for your company, you can either "merge" the company's teams' radars, or by executing the following steps with all your company's staff.

1. Bring the people of your team together in a room
2. Provide them Post-its and pens and let them write down what technologies, methods and tools they think you
  * use in your team
  * should asses or try in your team in the future
  * should NOT use
3. Agree upon each Post-it whether it should be part of your radar
4. cluster the Post-its concerning their state of adoption (on hold, assess, trial, adopt)
5. Finally you can group Post-its in segments on the radar, e.g.
  * tools (e.g. eclipse, git, bundler...)
  * frameworks (e.g. symfony, jQuery, Angular...)
  * methods (feature toggles, gitflow, pair programming...)

Using Post-its makes it easy to move things around until they converge. Take a picture at the end and if you want, you can make a nice drawing out of it for your company wiki or company website.

Be reminded though that the radar is "dynamic" and will certainly change over time. Repeat the session from time to time (e.g. every 3 months) to update your radar.


### How to maintain your Technology Radar

You should reconsider the items in your radar from time to time to make sure that they are up to date. Therefore you can for example ask yourself the following questioms:

* Is there a change in the level of adoption for an item?
* Move items from the "adopted" state to an archive if it's adopted for a longer time
* Add new items as they occur in your work
* Update the description of items (e.g. in your wiki) if you gathered new insights
* Update item markers in your radar
* Publish updated radar (on your website or in your company wiki)


## The Skill Radar

In comparison to the technology radar as a tracker for innovation and tooling, the *Skill Radar* is the right tool for keeping track of your personal skills, team skills and company skills. It describes the level of skills of a person (or team or company) in several dimensions.

There are certainly different ways to visualize such a Skill Radar but a common one is to use a so-called [radar chart or spider chart] with multiple *skill dimensions* starting in the center and crossing multiple *skill levels*. A drawing should make things clearer:

![Example of a skill radar](/assets/images/skill-radar/skill-radar.png)

### How to create your own skill radar

1. Agree upon the skill levels you want to use, e.g.
  * *"Never heard about it"* (center of the chart)
  * *"Already heard about that"*
  * *"Came in touch with it"*
  * *"Can use it / work with it, if I get help from someone else"*
  * *"I can use it / work with it independently"*
  * *"I can explain it to others"* (outer line of the chart)
2. Cluster the technologies, methods and tools from your skill radar into roughly 10 - 20 skill dimensions
3. First have the others of your team assess your skills in each dimension
4. Assess yourself in each dimension
5. Compare and discuss
6. Create individual skill radars and team skill radars
7. Again - take a picture and make a drawing

Repeat this procedure after 3 months to update your Skill Radar. By the way: you can easily create the graphics for the skill radar using a [Spider Chart] in Excel.


## Applications for Technology Radar and Skill Radar

Besides the fact that those charts make nice pictures in your company wiki or team room they are helpful instruments for management and marketing.


### Management

Here are a few ideas of how Technology Radar and Skill Radar walk hand in hand to be used as management tools in your company:

1. Plan and organize trainings and education of your staff:
  * Agree upon personal priorities and team priorities for enhancing your skills
  * Plan trainings four your staff
  * Select Conferences according to your goals
  * Organize peer-to-peer coaching inside or across teams concerning technologies
2. Plan hiring of new employees
  * Let potentially new employees fill out their personal skill radar
  * See how it complements the Skill Radar of your team / your company
3. Organize holiday standby in your teams
  * Make sure to have at least one "Level 3" person for each required skill
4. Get an overview of "critical gaps" in your knowledge distribution
  * Discuss a potentially lack of knowledge for each skill dimension
  * Discover company skills that depend on a single person
  * Come up with specific measures to close those gaps
5. Get an overview of innovation activities in your company
  * Visualize which bits of innovation are in progress
  * Have a tool to limit amount of innovation in progress and control it -- e.g. in board meeting
  * Track innovation progress over a longer period of time


### Marketing

Publishing your Technology Radar on your company website can make customers and potential employees aware of you as an innovative company.


## Conclusions

Technology Radar and Skill Radar are easy-to-use tools for

* managing and communicating learning and innovation in your company
* finding gaps in your personal knowledge, team skills or company skills
* planning resources and projects according to the skills of your staff
* presenting innovation to the visitors of your website


## Further Resources

* [HTML, CSS & JavaScript implementation of a Radar Chart](http://codepen.io/ggaulard/pen/BfkIx)
* [Free jQuery radar chart Plugins](http://www.jqueryscript.net/tags.php?/radar%20chart/)
* [Feature comparison with Radar Charts](http://www.fusioncharts.com/chart-primers/radar-chart/)


[Hackernews]:								https://news.ycombinator.com/
[Technology Radar from Thoughtworks]:       http://www.thoughtworks.com/radar
[Emendare]:									http://www.emendare.de/
[radar chart or spider chart]:              http://en.wikipedia.org/wiki/Radar_chart
[Spider Chart]:                             https://support.office.com/en-us/article/Present-your-data-in-a-radar-chart-16e20279-eed4-43c2-9bf5-29ff9b10601d
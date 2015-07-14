---
layout: post
title:  "Gitlab CLI"
date:   2015-07-14 21:00:00
tags: [gitlab, productivity, devops]
categories: devops
---

A few months ago I discovered the  [Gitlab Gem](https://github.com/NARKOZ/gitlab), which offers a client library for the Gitlab API endpoints. It took me until last week to find out that this Gem ships with a command line tool `gitlab` that lets you use the Gitlab API from the command line. Here are a few tips and tricks.

Installing the Gitlab CLI
-------------------------

<ol>
<li>Get yourself Private Token from your Gitlab server ("Account Settings" - "Account")</li>

<li>Edit your `~/.bashrc` or `~/.profile` or `~/.zshrc` or whatever configures the shell you use and add the following lines
{% highlight sh startinline=true %}
export GITLAB_API_PRIVATE_TOKEN=YOUR_API_KEY
export GITLAB_API_ENDPOINT=https://YOUR_GITLAB_SERVER_DOMAIN/api/v3
{%endhighlight %}
</li>

<li>Make sure to "reload" your `.bashrc` (or whatever) file with `source ~/.bashrc`</li>

<li>Install the Gem with `gem install gitlab`. If you are using rbenv, run `rbenv rehash`</li>

<li>Check whether your installation was successful with `gitlab help` and `gitlab projects`. The latter should return a list of projects from your Gitlab server.</li>
</ol>


Using the Gitlab CLI
--------------------

Unfortunately, the man pages of the Gitlab CLI that you get with `gitlab help` are not very concise. The 'easiest' way to find out, how to use the tool, is going to the [Gitlab Client API Documentation](http://www.rubydoc.info/gems/gitlab/Gitlab/Client/) and searching for the corresponding method. There you will find a detailed list of methods, parameters and options that gives you a hint on how to use the command line tool.

Remind that any options (not arguments) given to a method need to be encoded in a YAML-style format on the command line. E.g. if you want to pass the option `per_page` to the `gitlab projects` command, you have to use `gitlab projects "{per_page: 1000}"`. Any string values have to be wrapped in `'...'`.

So here are some examples on how to use the `gitlab` command line tool:

### Gitlab Projects (a.k.a. Repositories)

<ul>

<li>Get a list of the 20 most recent projects:
{% highlight sh startinline=true %}
gitlab projects
{%endhighlight %}
</li>

<li>Get a list of all projects:
{% highlight sh startinline=true %}
gitlab projects "{per_page: 10000}"
{%endhighlight %}

where `10000` is a big enough number to get all projects from your Gitlab server.
</li>

<li>Search for a project:
{% highlight sh startinline=true %}
gitlab project_search NAME
{%endhighlight %}
</li>


<li>Create a project in your Gitlab userspace:
{% highlight sh startinline=true %}
gitlab project_create PROJECT_NAME
{%endhighlight %}
</li>

<li>
Create a project in a distinct group:
<br><br>
First: Find the Gitlab ID of the group you want to add your project to with <br>	<code>gitlab groups "{per_page: 1000}" | grep GROUP_NAME</code>.<br><br> Then use this ID as in:
{% highlight sh startinline=true %}
gitlab project_create PROJECT_NAME "{namespace_id: 'ID'}"
{%endhighlight %}
</li>

<li>Add a deploy key with content <code>DEPLOY_KEY_CONTENT</code> and a description <code>DESCRIPTION</code> to a project with ID <code>PROJECT_ID</code>:
{% highlight sh startinline=true %}
gitlab create_deploy_key PROJECT_ID 'DEPLOY_KEY_DESCRIPTION' 'DEPLOY_KEY_CONTENT'
{%endhighlight %}

Heres is an example that reads the key from an existing RSA file:

{% highlight sh startinline=true %}
gitlab create_deploy_key 616 'Jenkins Vagrant Development' "`cat ../vagrant-jenkinsmaster/cookbooks/env_jenkins_master_dev/files/id_rsa.pub`"
{%endhighlight %}
</li>

</ul>


### Gitlab Groups

<ul>
<li>Get a list of all groups:
{% highlight sh startinline=true %}
gitlab groups "{per_page: 1000}"
{%endhighlight %}
</li>

<li> Create a group with the name <code>GROUP_NAME</code> and the path <code>PATH</code>:
{% highlight sh startinline=true %}
gitlab create_group "GROUP_NAME" "PATH"
{%endhighlight %}
</li>

<li> Add a user with the ID <code>USER_ID</code> to a group with ID <code>GROUP_ID</code> with access level <code>ACCESS_LEVEL</code>:
{% highlight sh startinline=true %}
gitlab add_group_member GROUP_ID USER_ID ACCESS_LEVEL
{%endhighlight %}
<code>ACCESS_LEVEL</code> is an integer value, you can look up the values in <a href="https://github.com/gitlabhq/gitlabhq/blob/master/lib/gitlab/access.rb">Gitlab's access.rb file</a>.
Here are the current values:
<ul>
<li> <code>GUEST</code> = 10 </li>
<li> <code>REPORTER</code> = 20 </li>
<li> <code>DEVELOPER</code> = 30 </li>
<li> <code>MASTER</code> = 40 </li>
<li> <code>OWNER</code> = 50 </li>
</ul>
</li>
</ul>

### Gitlab Users

<ul>
<li> Search for a user with the name <code>USERNAME</code>:
{% highlight sh startinline=true %}
gitlab users "{per_page: 1000}" | grep "USERNAME"
{%endhighlight %}
Remind that the <code>per_page: 1000</code> option makes sure that "all" users are returned!
</li>
</ul>

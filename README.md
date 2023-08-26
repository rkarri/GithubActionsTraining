# GithubActionsTraining (this is my personal notes only and can be stale over time)

GitHub actions

features of Github: 
1. Creating releases from tags
2. Wiki page for each repo for documentation (not specific to Github actions)



Workflows
************************
background:
Workflows will be trigered by Github events like checking in code etc.. 
a workflow will have a yaml file. this should be placed in a .github/workflows directory. this directory exists on all branches you want to run workflows on.
once the workflow runs, the run history will be in the Actions page of the github
in the yaml file the event will be mentioned after the "on" keyword
A Workflow can contain multuple jobs. and each job can contain multiple steps.

Ex:
on: push

you can also specify multiple events in an array 

Ex: 
on: [push, pull_request]

events can also have activity_types/filters. for example of the push only apples to master branch then 

Ex:
on: 
  push
    branches: [master]
  pull_request:
    branches: [master]
	
	
There are many events in Github that can trigger a workflow. 
https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#webhook-events


you can create tags in github history. releases can be created from tags in github. you can also run a workflow when a tag is created 
you can also run workflows when some one forks your repo. ot updates a wiki page

An issue in Github is like a bug tracker at the repo level. 
you can also run workflows on issue events and it supports multiple activity_types

you can also schedule a workflow to run at a certain time (schedule is indicated by cron syntax)
[note on cron: there are 5 values on cron syntax seperated by a space. minute, hour, day[1-31], month [1-12], day of the week[0-6]. * means any value ]
go to https://crontab.guru/ to get help writing cron syntax. you can add expressions and ranges in cron syntax like (second sunday of every month) 
Ex:
on: 
  schedule
    -cron: '30 5 * * *'

there is also another event called "workflow_dispatch" this is used to run workflow manually. you can also allow user to enter values (input variables) at the time of running it manually
this is a way to accept dynamic values into the workflow definition file. "like run the workflow from a different branch dynamically"

Ex:
on: workflow_dispatch
      inputs:
	    name:
		  description: 'Enter a name'
		  required: true
          default: 'Github user'	
		  
these input variables can be accessed within the workflow file using the following syntax
${{ github.events.inputs.<name of the input variable> }}


External apps can also trigger github workflows by calling Github REST API

*************************************************************************************************
workflows run in github runners. specifically each job within a workflow will run on its own runner. runners are nothing but pre-configured VMs [hosted in Azure]. actions can also run in a docker containers.
you can use "runs-on" (within a job definition) label to choose what type of runner you want to run on. 
all jobs run in parallel by default. if you want to create dependencies between jobs or run sequentially, then use the "needs" keyword. 
but steps are sequential within a job. steps can be actions/commands
Actions are nothing but predefined blocks of code stored in a repository. (think of action  -> endpoint)
commands can be bash/powershell commands to be executed on the runner


Yaml does not need quotes like json or braces. but you can optionally use quotes. instead of braces, yaml uses 2 spaces to show hierarchical structure.
a key in yaml is always a string. but the value can be a object, collection, number, boolean , array 

you can use self-hosted runners as well within your data center

github actions are free for public repos and self-hosted runners
For private repos, there are free minutes.


Plan					Storage	Minutes (per month)
Free					500 MB	2,000
Pro						1 GB	3,000
Free for organizations	500 MB	2,000
Team					2 GB	3,000
Enterprise Cloud		50 GB	50,000








	
	



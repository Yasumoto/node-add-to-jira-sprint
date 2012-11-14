#!/usr/bin/env coffee

{JiraApi} = require "jira"
colors = require "colors"
util = require 'util'

argv = require("optimist")
        .usage("Usage: $0 [PROJECT]-[TICKET_NUMBER]")
        .argv

config = require "../.config.json"

ticket_id = argv._[0]
project_name = ticket_id.split('-')[0]

jira = new JiraApi 'http', config.hostname, '80', config.user, config.password, 'latest'

jira.findRapidView project_name, (error, rapid_view) ->
  console.error error.red if error?
  jira.getLastSprintForRapidView rapid_view.id, (error, last_sprint) ->
    console.error error.red if error?
    jira.addIssueToSprint ticket_id, last_sprint.id, (error) ->
      console.error error if error?

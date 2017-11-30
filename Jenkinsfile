#!/usr/bin/env groovy

node {

    stage('Clone repository') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/anshumanbh/node-js-getting-started.git']]])
    }

    stage('Retrieving Secrets from Conjur') {
        sh "summon-conjur heroku/heroku-key > ~/.netrc"
    }

    stage ('Cleanup'){
        sh "rm -rf .git"
        sh "git init"
    }

    stage('Heroku Create') {
       sh "heroku create"
    }

    stage ('Heroku Commit'){
        sh "git add ."
        sh "git commit -m \"test\""
    }

    stage('Heroku Push') {
        sh "git push heroku master"
    }

    stage('Heroku Scale') {
        sh "heroku ps:scale web=1"
    }
}
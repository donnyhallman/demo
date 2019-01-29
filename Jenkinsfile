#!/usr/bin/env groovy

pipeline {
    agent any
	stages {
	   
	  stage('Build: Compile') {
	   steps {
       	  //checkout scm
       	  git url: 'https://github.com/donnyhallman/demo.git'
       	  sh './gradlew clean build -x test -x check'
       }
	  }
	  
	  
	  stage('Analysis'){
	    steps{
	        sh './gradlew check -x test --continue'
		  	recordIssues enabledForFailure: true, healthy: 3, minimumSeverity: 'NORMAL', tools: [pmdParser(pattern: '**/reports/pmd/*.xml')], unhealthy: 8
	    }
	  }
    
      stage('Test'){
       	steps{  
	  		sh './gradlew check -x pmdMain --continue'	  
       	}

	  }

	}

	

}
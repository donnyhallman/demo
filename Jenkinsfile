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
	   parallel {
   	     stage('PMD'){
   	        steps{   	            
   	         sh './gradlew pmdMain --continue'
		  	recordIssues healthy: 3, ignoreQualityGate: true, minimumSeverity: 'NORMAL', tools: [pmdParser(pattern: '**/reports/pmd/*.xml')], unhealthy: 8    
   	        }

   	     }
		 stage('SpotBugs'){
		    steps{
   	         sh './gradlew spotbugsMain --continue'
		  	 recordIssues healthy: 3, ignoreQualityGate: true, minimumSeverity: 'NORMAL', tools: [spotBugs(pattern: '**/reports/spotbugs/*.xml', useRankAsPriority: true)], unhealthy: 8
		   }
   	     }
   	   }

	  }
    
      stage('Test'){
       	steps{  
	  		sh './gradlew check -x pmdMain --continue'	  
       	}

	  }

	}
}
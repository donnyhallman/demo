#!/usr/bin/env groovy

pipeline {
    agent any
	stages {
	   
	  stage('Build: Compile') {
	   steps {
       	  checkout scm
       	  sh './gradlew clean build -x test -x check'
       }
	  }
	  
	  
	  stage('Analysis'){
	  	sh './gradlew check -x test'
	  	def pmd = scanForIssues tool: [$class: 'Pmd'], pattern: '**/reports/pmd/*.xml'
        publishIssues issues:[pmd]
	  }
    
      stage('Test'){
	  	sh './gradlew check -x pmdMain'
	  	
	  }
	   
 
	    

	}



}

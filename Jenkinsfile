#!/usr/bin/env groovy

pipeline {
    agent any
	stages {
	   
		  stage('Compile') {
    	   steps {
   	       	  checkout scm
   	       	  sh './gradlew clean build -x test -x check'
   	       }

    	}
	       

	   
 
	    

	}



}

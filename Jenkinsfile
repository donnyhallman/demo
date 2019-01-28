#!/usr/bin/env groovy

pipeline {
    agent any
	stages {
	   node{
		  stage('Compile') {
    	   steps {
   	       	  checkout scm
   	       	  sh './gradlew clean build -x test -x check'
   	       }

    	}
	       

	   }
 
	    

	}



}

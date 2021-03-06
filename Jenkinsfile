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
	  
	  
	  stage('Analysis & Test'){
	   parallel {
   	     stage('Analysis: PMD'){
   	        steps{   	            
   	         sh './gradlew pmdMain --continue'
		  	recordIssues healthy: 3, ignoreQualityGate: true, minimumSeverity: 'NORMAL', tools: [pmdParser(pattern: '**/reports/pmd/*.xml')], unhealthy: 8    
   	        }

   	     }
		 stage('Analysis: SpotBugs'){
		    steps{
   	         sh './gradlew spotbugsMain --continue'
		  	 recordIssues healthy: 3, ignoreQualityGate: true, minimumSeverity: 'NORMAL', tools: [spotBugs(pattern: '**/reports/spotbugs/*.xml', useRankAsPriority: true)], unhealthy: 8
		   }
   	     }
	      stage('Test'){
	       	steps{  
		  		sh './gradlew cleanTest check -x spotbugsMain -x pmdMain --continue'
		  		junit '**/build/test-results/test/*.xml' 
		  		jacoco buildOverBuild: true, changeBuildStatus: true, deltaBranchCoverage: '25', 
		  			deltaClassCoverage: '25', deltaComplexityCoverage: '25', deltaInstructionCoverage: '25', 
		  			deltaLineCoverage: '25', deltaMethodCoverage: '25', maximumBranchCoverage: '70', 
		  			maximumClassCoverage: '80', maximumComplexityCoverage: '70', maximumInstructionCoverage: '70', 
		  			maximumLineCoverage: '70', maximumMethodCoverage: '80', minimumBranchCoverage: '50', 
		  			minimumClassCoverage: '50', minimumComplexityCoverage: '50', minimumInstructionCoverage: '50',
		  			 minimumLineCoverage: '50', minimumMethodCoverage: '50'
	       	}
	
		  }
   	   }

	  }
    

	}
}
pipeline {
  agent any
// =======================================================================
// Creating this project as parameterized by using git paramater option
// =======================================================================
  parameters {
    gitParameter branch: '', branchFilter: 'origin/(.*)', defaultValue: 'develop', name: 'BRANCH', type: 'PT_BRANCH'
  }
  // ===============================================================================================
// PIPELINE TO RUN WITHIN 60 MINS, OTHERWISE TIMEOUT
// ===============================================================================================
	options {
		timestamps()
		disableConcurrentBuilds()
		buildDiscarder(logRotator(numToKeepStr: '90', artifactDaysToKeepStr: '30'))
		//timeout(time: 60, unit: 'MINUTES')
	}
// =======================================================================
// BUILD SCHEDULE: DAILY (MON-FRI) @ 09:00 AM
// =======================================================================					
	triggers {
		cron('H 9 * * 1-5') 
	}
  stages {
// =======================================================================
// CLEANING THE WORKSPACE BEFORE CLONING
// =======================================================================
    stage('Deleting workspace') {           
            steps{
				deleteDir()
			}
		}
// =======================================================================
// Cloning the source code from Bitbucket
// =======================================================================
    stage('Example') {
      steps {
		git branch: "${params.BRANCH}", url: 'https://github.com/nehasri17/gitpractice.git'
      }
    }
  }
}

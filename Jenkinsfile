// env-vars.html --> all in-built environmental variables
CODE_CHANGES = getGitChanges()

pipeline {
	agent any

	parameters {

		// two types of parameters:
		//  1. string(name, defaultValue, description)
		//  2. choice(name, choices, description)
		//  3. booleanParam(name, defaultValue, description)

		// string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod')
		choice(name: 'VERSION', choices: ['1.1.1', '1.1.2', '1.1.3'], description: '')
		booleanParam(name: 'executeTests', defaultValue: true, description: '')
	}

	environment {
			NEW_VERSION = '1.3.0'
			SERVER_CREDENTIALS = credentials('<credentials-id>')
	}

	tools {
		// access build tools
		// only 3 tools available : gradle, maven, jdk

		maven 'Maven'

		// this has to be pre-configured in Jenkins
		// to configure:
		// 			|-> Manage Jenkins  
		//  					|-> Global tool configuration
		// 									|-> Under Name attribute, check value of Name, and specify here.
	}

	stages {
		stage("build"){
			when {
				expression {
					// BRANCH_NAME == 'dev' & CODE_CHANGES == true
					parmas.executeTests
				}
			}
			steps {
				echo 'building the application'
				echo "building version ${NEW_VERSION}"
				echo "accessing version using parameters ${VERSION}"
			}
		}
		stage("test"){
			steps {
				echo 'testing the application'
			}
		}
		stage("deploy"){
			steps {
				echo 'deploying the application'
				withCredentials([
						usernamePassword(credentials: '<credentials-id>' username: USER, password: PWD)
					]){

				}
			
			}
		}
	}

	post {
		always {

		}
		success {

		}
		failure {

		}
	}

}
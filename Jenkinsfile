pipeline {
	agent none

	enviroment {
		AUTHOR = "Alaric Gwyneth"
		EMAIL = "alaric.gwyneth@gmail.com"
	}

	stages {

		stage("Prepare") {
        	agent {
           		node {
           	        label "linux && java11"
       		    }
            }
            steps {
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build  : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }

		stage("Hello") {
			steps {
				echo "Hello Pipeline"
			}
		}

		stage("Build") {
			agent {
           		node {
           			label "linux && java11"
           		}
           	}
        	steps {
        	    script{
        	        for(int i = 0; i < 10; i++){
        	            echo("script ${i}")
        	        }
        	    }
        	    echo ("Hello Build 1")
        	    sleep(5)
        	    echo ("Hello Build 2")
        	    echo ("Hello Build 3")
				echo("Start Build")
        	    sh("./mvnw clean compile test-compile")
        	    echo("Finish Build")
        	}
   		}

   		stage("Test") {
   		    agent {
                 node {
           			label "linux && java11"
           	     }
            }

             steps {
                script {
                    def data = [
                        "firstName": "Alaric",
                        "lastName": "Gwyneth"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
           	    echo ("Hello Test 1")
           	    sleep(5)
           	    echo ("Hello Test 2")
           	    echo ("Hello Test 3")
				echo("Start Test")
        	    sh("./mvnw test")
        	    echo("Finish Test")
           	}
        }

        stage("Deploy") {
            agent {
           		node {
                   label "linux && java11"
                }
            }

			steps {
				echo ("Hello Deploy 1")
				sleep(5)
				echo ("Hello Deploy 2")
				echo ("Hello Deploy 3")
				echo("Start Test")
           	    sh("./mvnw test")
        	    echo("Finish Test")
			}
		}

	}

	post {
		always {
			echo "I will always say Hello again!"
		}
		success {
			echo "Yay, success"
		}
		failure{
			echo "Oh no,shit it is failure"
		}
		cleanup {
			echo "Don't care success or error"
		}
	}
}
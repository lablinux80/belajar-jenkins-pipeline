pipeline {
	agent {
		node {
			label "linux && java11"
		}
	}

	stages {

		stage("Hello") {
			steps {
				echo "Hello Pipeline"
			}
		}

		stage("Build") {
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
             steps {
                script {
                    def data [
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
pipeline {
    agent none

    environment {
        AUTHOR = "Alaric Gwyneth"
        EMAIL = "alaric.gwyneth@gmail.com"
    }
//     triggers {
//          cron("*/5 * * * *")
//         pollSCM("*/5 * * * *")
//          upstream(upstreamProject: "job1,job2", threshold: hudson.model.result.SUCCESS)
    }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
//         timeout(time: 10, unit: "SECONDS")
        timeout(time: 2, unit: "MINUTES")
    }

    stages {

        stage("Parameter") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps{
                echo "Hello ${params.NAME}"
                echo "You Description is ${params.DESCRIPTION}"
                echo "Need to deploy ${params.DEPLOY} to deploy!"
                echo "Social Media ${params.SOCIAL_MEDIA}"
                echo "Secret ${params.SECRET}"
            }
        }

        stage("Prepare") {

            environment {
                APP = credentials("junius_rahasia")
            }
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
                echo("App User : ${APP_USR}")
                echo("App Password : ${APP_PSW}")
                sh("echo 'App Password : ${APP_PSW}' > 'rahasia.txt'")
                sh('echo "App Password : $APP_PSW" > "rahasia2.txt"')
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
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
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
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
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
            input {
                message "Can we deploy?"
                ok "Yes, of course."
                submitter "Alaric,Gwyneth"
//                 parameters {
//                     choice(name: "TARGET_ENV", choices: ["DEV", "QA", "PROD"], description: "We will deploy")
            }
            agent {
                   node {
                   label "linux && java11"
                }
            }
            steps {
//                 echo "Deploy to ${TARGET_ENV}"
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

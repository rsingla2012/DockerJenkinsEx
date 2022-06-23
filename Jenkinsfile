//see list of Jenkins vars available at localhost:8080/env-vars.html
// you can also define own environment variables
//echo line must be in double quotes if using an escape character to pass in var as a string


pipeline {
    agent any
    parameters{
        //string(name:'VERSION', defaultValue: '', description: 'version to deploy')
        choice (name:'VERSION', choices: ['1.1.0', '1.2.0','1.3.0'], description: '')
        booleanParam(name:'executeTests', defaultValue: true, description: '')
    }
    /*tools{
        maven
        gradle
    }*/
    environment{
        NEW_VERSION = '1.3.0'
        //CREDENTIALS= 
    }
    stages {
        stage("build") {
            when {
                expression{
                    params.executeTests
                    BRANCH_DEV == 'dev' // or when some var CODE_CHANGES == 'true' (need to set groovy script to set vat)
                }
            }
            steps {
                echo 'building the application...' 
                // sh "mvn install"
                echo "building version ${NEW_VERSION}"
                
            }
        }
        stage("test") {
            when {
                expression{
                    BRANCH_DEV == 'dev' || BRANCH_DEV == 'master'
                }
            }
            steps {
                echo 'testing the application...' 
            }
        }
        stage("deploy") {
            steps {
                echo 'deploying the application...' 
                echo "deploying version ${params.VERSION}" 
                /*withCredentials([
                    usernamePassword(credentials: 'server-credentials', usernameVariable:USER, password: PWD)
                ])*/
            }
        }
        post{
            always{
                steps{
                    echo 'done with all stages'
                }
            }
            success{
                steps{
                    echo 'build succeeded'
                }
            }
            failure{
               steps{
                    echo 'build failed'
                }
            }
        }
    }   
}

pipeline{

    agent  {label 'master'}
    tools { 
        maven 'Maven 3.8.4'  
    }

    stages {
        // stage ('Compile Stage') {
        //     steps {
        //         withMaven(maven: 'maven_3_5_0') { sh 'mvn clean install' }
        //     }
        // }
        // stage ('Test Stage') {
        //     steps {
        //         withMaven(maven: 'maven_3_5_0') { sh 'mvn test'}
        //     }
        // }
        stage("Checkout Code") {
               steps {
                    git branch: 'master',
                    url: "https://github.com/mdabuhasnat/jenkins-cucumber.git"
                }
           }
        stage('Build') {
            steps {
              sh "mvn test"
            }
        }
        stage ('Cucumber Reports') {
            steps {
                cucumber buildStatus: "UNSTABLE",
                fileIncludePattern: "**/cucumber.json",
                jsonReportDirectory: 'target'
            }
        }
    }
}

pipeline {
    agent {label 'master'}

	tools { 
        maven 'Maven 3.8.4'  
    }
    parameters {
        choice(choices: 'yes\nno', description: 'Are you sure you want to execute this test?', name: 'run_test_only')
        choice(choices: 'yes\nno', description: 'Archived to jar?', name: 'archive_jar')
        string(defaultValue: "fazley.rabby@bjitgroup.com", description: 'email for notifications', name: 'notification_email')
    }

    stages {
        stage('Test'){
             //conditional for parameter
            when {
                environment name: 'run_test_only', value: 'yes'
            }
            steps{
                sh 'mvn clean test'
            }
        }
  
    post {
            success {
            //node('node1'){
            echo "Test succeeded"
                script {
                    mail(bcc: '',
                        body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
                        cc: '',
                        from: 'fazley.rabby@bjitgroup.com',
                        replyTo: '',
                        subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
                        to: env.notification_email)
                        if (env.archive_jar =='yes')
                        {
                            // archiveArtifacts '**/java-calculator-*-SNAPSHOT.jar'
                            archiveArtifacts(artifacts: 'target/surefire-reports/*', followSymlinks: false)
                        }
                        // Cucumber report plugin
                        cucumber fileIncludePattern: '**/target/cucumberr.json', sortingMethod: 'ALPHABETICAL'
                //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/home/reports', reportFiles: 'reports.html', reportName: 'Performance Test Report', reportTitles: ''])
                }
            //}
            }

        }
}

node {
    def mvnHome
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
//         git 'https://github.com/jglick/simple-maven-project-with-tests.git'
        // Get the Maven tool.
        // ** NOTE: This 'M3' Maven tool must be configured
        // **       in the global configuration.
//         mvnHome = tool 'M3'
        echo 'Preparation'
    }
    stage('Build') {
        // Run the maven build
//         withEnv(["MVN_HOME=$mvnHome"]) {
//             if (isUnix()) {
//                 sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
//             } else {
//                 bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
//             }
//         }
        echo 'Build'
    }
    stage('Run pipeline copy') {
        build job: 'Copy pipeline 1', parameters: [
            string(name: 'git tag', value: "val-2")
//             choice('git tag': 'TAG-3', value:'val-2')
        ], wait: true
    }
    stage('Results') {
//         junit '**/target/surefire-reports/TEST-*.xml'
//         archiveArtifacts 'target/*.jar'
        echo 'Results'
    }
}

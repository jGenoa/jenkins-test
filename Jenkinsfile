pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Run pipeline copy') {
            steps {
                build(job: 'inner-pipeline-1', parameters: [
                    string(name: 'Select git tag', value: "TAG-3"),
                    string(name: 'Select value', value: "val-2"),
                ], wait: true)
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
// pipeline {
//     agent none
//     stages {
//         stage('Preparation') { // for display purposes
//             // Get some code from a GitHub repository
//     //         git 'https://github.com/jglick/simple-maven-project-with-tests.git'
//             // Get the Maven tool.
//             // ** NOTE: This 'M3' Maven tool must be configured
//             // **       in the global configuration.
//     //         mvnHome = tool 'M3'
//             echo 'Preparation'
//         }
//         stage('Build') {
//             // Run the maven build
//     //         withEnv(["MVN_HOME=$mvnHome"]) { 
//     //             if (isUnix()) {
//     //                 sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
//     //             } else {
//     //                 bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
//     //             }
//     //         }
//             echo 'Build'
//         }
//         stage('Run pipeline copy') {
//             build job: 'inner-pipeline-1', parameters: [
//                 string(name: 'Select git tag', value: "TAG-3"),
//                 string(name: 'Select value', value: "val-2"),
//     //             choice('git tag': 'TAG-3', value:'val-2')
//             ], wait: true
//         }
//         stage('Run in pararell') {
//             parallel {
//                 stage('run-inner-pipeline-1') {
//                     // steps {
//                     //     build job: 'inner-pipeline-1', parameters: [
//                     //         string(name: 'Select git tag', value: "TAG-3"),
//                     //         string(name: 'Select value', value: "val-1"),
//                     //     ], wait: true
//                     // }
//                 }
//                 stage('run-inner-pipeline-2') {
//                     // steps {
//                     //     build job: 'inner-pipeline-2', parameters: [
//                     //         string(name: 'Select git tag', value: "TAG-2"),
//                     //         string(name: 'Select value', value: "val-2"),
//                     //     ], wait: true
//                     // }
//                 }
//                 stage('run-inner-pipeline-3') {
//                     // steps {
//                     //     build job: 'inner-pipeline-3', parameters: [
//                     //         string(name: 'Select git tag', value: "TAG-1"),
//                     //         string(name: 'Select value', value: "val-3"),
//                     //     ], wait: true
//                     // }
//                 }
//             }
//         }
//         stage('Results') {
//     //         junit '**/target/surefire-reports/TEST-*.xml'
//     //         archiveArtifacts 'target/*.jar'
//             echo 'Results'
//         }
//     }
// }

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
            parallel {
                stage('run-inner-pipeline-1') {
                    when {
                        expression { params.RUN_PIPELINE_1 }
                    }
                    steps {
                        input message: 'Should I run pipeline 1?', ok: 'Run pipeline 1', parameters: [choice(choices: ['TAG-1'], name: 'Select tag')], submitterParameter: 'should_run_pipeline_one'
                        build(job: 'inner-pipeline-1', parameters: [
                            string(name: 'Select git tag', value: "TAG-3"),
                            string(name: 'Select value', value: "val-1"),
                        ])
                    }
                }
                stage('run-inner-pipeline-2') {
                    when {
                        expression { params.RUN_PIPELINE_2 }
                    }
                    steps {
                        build(job: 'inner-pipeline-2', parameters: [
                            string(name: 'Select git tag', value: "TAG-2"),
                            string(name: 'Select value', value: "val-2"),
                        ])
                    }
                }
                stage('run-inner-pipeline-3') {
                    when {
                        expression { params.RUN_PIPELINE_3 }
                    }
                    steps {
                        build(job: 'inner-pipeline-3', parameters: [
                            string(name: 'Select git tag', value: "TAG-1"),
                            string(name: 'Select value', value: "val-3"),
                        ])
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}


// input message: '', ok: 'Run pipeline 1', parameters: [choice(choices: ['TAG-1'], name: 'Select tag')]
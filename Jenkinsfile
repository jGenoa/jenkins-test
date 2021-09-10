// properties([
//     parameters([
//         [$class: 'CascadeChoiceParameter', 
//             choiceType: 'PT_SINGLE_SELECT',
//             description: 'Select a choice',
//             filterLength: 1,
//             filterable: true,
//             name: 'choice1',
//             referencedParameters: 'ENVIRONMENT',
//             script: [$class: 'GroovyScript',
//                 fallbackScript: [
//                     classpath: [], 
//                     sandbox: true, 
//                     script: 'return ["ERROR"]'
//                 ],
//                 script: [
//                     classpath: [], 
//                     sandbox: true, 
//                     script: """
//                         if (ENVIRONMENT == 'lab') { 
//                             return['aaa','bbb']
//                         }
//                         else {
//                             return['ccc', 'ddd']
//                         }
//                     """.stripIndent()
//                 ]
//             ]
//         ]
//     ])
// ])

// properties([
//   parameters([
//     [
//       $class: 'ChoiceParameter',
//       choiceType: 'PT_SINGLE_SELECT',
//       name: 'Environment',
//       script: [
//         $class: 'ScriptlerScript',
//         scriptlerScriptId:'Environments.groovy'
//       ]
//     ],
//     [
//       $class: 'CascadeChoiceParameter',
//       choiceType: 'PT_SINGLE_SELECT',
//       name: 'Host',
//       referencedParameters: 'Environment',
//       script: [
//         $class: 'ScriptlerScript',
//         scriptlerScriptId:'HostsInEnv.groovy',
//         parameters: [
//           [name:'Environment', value: '$Environment']
//         ]
//       ]
//    ]
//  ])
// ])

pipeline {
    agent any

    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Select pipelines to run..'
                
            }
        }
        stage('Run pipeline copy') {
            parallel {
                stage('run-inner-pipeline-1') {
                    // when {
                    //     expression { params.RUN_PIPELINE_1 }
                    // }
                    steps {
                        input message: 'Should I run pipeline 1?', ok: 'Run pipeline 1', parameters: [choice(choices: ['TAG-1'], name: 'Select tag')], submitterParameter: 'should_run_pipeline_one'
                        build(job: 'inner-pipeline-1', parameters: [
                            string(name: 'Select git tag', value: "TAG-3"),
                            string(name: 'Select value', value: "val-1"),
                        ])
                    }
                }
                stage('run-inner-pipeline-2') {
                    // when {
                    //     expression { params.RUN_PIPELINE_2 }
                    // }
                    steps {
                        build(job: 'inner-pipeline-2', parameters: [
                            string(name: 'Select git tag', value: "TAG-2"),
                            string(name: 'Select value', value: "val-2"),
                        ])
                    }
                }
                stage('run-inner-pipeline-3') {
                    // when {
                    //     expression { params.RUN_PIPELINE_3 }
                    // }
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
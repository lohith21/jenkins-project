pipeline {
    agent any
    parameters {
        string(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'Specify env name')
        booleanParam(name: 'RUN_TEST', defaultValue: true, description: 'Run tests in pipeline') 
        }
    stages{ 
     
        stage('test') {
            when {
                expression {
                    params.RUN_TEST == true
                }
            }
            steps{
                echo "Running Unit Tests"
            }
            }
        stage('deploy'){
            steps{
                echo "Deploying the app in ${params.ENVIRONMENT} environment"
            }
        }

    }
}

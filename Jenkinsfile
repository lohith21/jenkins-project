pipeline {
    agent any
    parameters{
        string(name: 'ENVIRONMENT', defaultvalue: 'dev', description: 'Specify env name')
        booleanParam(name: 'RUN_TEST', defaultvalue: true, description: 'Run tests in pipeline') 
        }
     stage('test') {
            when {
                expression{
                    param.RUN_TEST == true
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

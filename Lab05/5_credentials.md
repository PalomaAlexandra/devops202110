# Credentials

1. Crear credentiales git-credentials

    * Manage Jenkins
    * Manage credentials
    * Stores scope: "Jenkins"
    * Clic "Global credentials"
    * Clic en "Add credentials"
    * "Kind": "Secret Text"
    * Secret: secret-key-123@
    * "Id": jenkins-aws-secret-key-id
    * Description: aws secret id
    * Clic en "Add credentials"
    * "Kind": "Secret Text"
    * Secret: secret-access-123@
    * "Id": jenkins-aws-secret-access-key
    

1. Crear job07-as-code usando variables
    * Crear proyecto del estilo Pipeline.
        * Nombre: job07-as-code
        * Description: Pipeline as code
        * Pipeline script
        ```dsl
        // comentario
        pipeline {
            agent any 
             environment {
                AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
                AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
            }
            stages {
                stage('AWS') {
                    steps {
                        
                        /* WRONG! */
                        //'hello; ls /'
                        //echo "AWS_ACCESS_KEY_ID: $AWS_ACCESS_KEY_ID"
                        

                        /* CORRECT! */
                        
                        echo 'AWS_SECRET_ACCESS_KEY: $AWS_SECRET_ACCESS_KEY'
                        sh('echo AWS_ACCESS_KEY_ID: ${AWS_ACCESS_KEY_ID}')
                        sh('echo AWS_SECRET_ACCESS_KEY: ${AWS_SECRET_ACCESS_KEY}')

                    }
                }
            }
        }
        ```
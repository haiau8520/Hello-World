pipeline {
    agent any
    stages {
        stage('Init') {
            steps {
                powershell """cd "C:/Users/stylvn077/Desktop/.terraform/new"; terraform init """
            }
        }
        stage('TF Plan') {
            steps {
                container('terraform') {
                    powershell "terraform plan -var-file=terraform.tfvars -out=myplan"
                }
            }
     }
        stage('Approval'){
            script {
                def userInput =
                input(id: 'confirm', message: 'Apply Terraform?',
                parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
            }
        }
        stage('TF apply'){
            steps{
                powershell "terraform apply -var-file=terraform.tfvars -input=false -auto-approval"
            }
        }
    }
}
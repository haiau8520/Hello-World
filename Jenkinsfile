pipeline {
    agent any
    stages {
        stage('Init') {
            steps {
                powershell """cd "C:/Users/stylvn077/Desktop/.terraform/new" """
                powershell "terraform init"
            }
        }
        stage('TF Plan') {
            steps {
                powershell """cd "C:/Users/stylvn077/Desktop/.terraform/new" """
                powershell "terraform plan -out=myplan"
                
            }
        }
        stage('Approval'){
            steps{
                script {
                    def userInput =
                    input(id: 'confirm', message: 'Apply Terraform?',
                    parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
                }
            }
        }
        stage('TF apply'){
            steps{
                powershell """cd "C:/Users/stylvn077/Desktop/.terraform/new" """
                powershell "terraform apply -var-file=terraform.tfvars -input=false -auto-approval myplan"
            }
        }
    }
}
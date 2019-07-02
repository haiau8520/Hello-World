pipeline {
    agent any
    stages {
        node{
            steps{
                powershell """cd "C:/Users/stylvn077/Desktop/.terraform/new" """
            }
        }
        stage('Init') {
            steps {
                powershell "terraform init"
            }
        }
        stage('TF Plan') {
            steps {
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
                powershell "terraform apply -var-file=terraform.tfvars -input=false -auto-approval myplan"
            }
        }
    }
}
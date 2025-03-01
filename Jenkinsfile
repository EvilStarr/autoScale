// pipeline {
//     agent any
//     environment {
//         AWS_REGION = 'us-east-1' 
//     }
//     stages {
//         stage('Set AWS Credentials') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'JenkinsWeds' 
//                 ]]) {
//                     sh '''
//                     echo "AWS_ACCESS_KEY_ID: $AWS_ACCESS_KEY_ID"
//                     aws sts get-caller-identity
//                     '''
//                 }
//             }
//         }
//         stage('Checkout Code') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/EvilStarr/autoScale' 
//             }
//         }
//         stage('Initialize Terraform') {
//             steps {
//                 sh '''
//                 terraform init
//                 '''
//             }
//         }
//         stage('Plan Terraform') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'JenkinsWeds'
//                 ]]) {
//                     sh '''
//                     export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
//                     export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
//                     terraform plan -out=tfplan
//                     '''
//                 }
//             }
//         }
//         stage('Apply Terraform') {
//             steps {
//                 input message: "Approve Terraform Apply?", ok: "Deploy"
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'JenkinsWeds'
//                 ]]) {
//                     sh '''
//                     export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
//                     export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
//                     terraform apply -auto-approve tfplan
//                     '''
//                 }
//             }
//         }
//     }
//     post {
//         success {
//             echo 'Terraform deployment completed successfully!'
//         }
//         failure {
//             echo 'Terraform deployment failed!'
//         }
//     }
// }
pipeline{
    agent any
    tools {
        jfrog 'jfrog-cli-remote'
    }
    stages {
        stage ('Testing') {
            steps {
                jf '-v' 
                jf 'c show'
                jf 'rt ping'
                sh 'touch test-file'
                jf 'rt u test-file tf3-terraform-modules-local/'
                jf 'rt bp'
                jf 'rt dl tf3-terraform-modules-local/test-file'
            }
        } 
    }
}



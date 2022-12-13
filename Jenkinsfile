pipeline {
   agent any
   stages {
    stage('Checkout') {
      steps {
        script {
           // The below will clone your repo and will be checked out to main branch by default.
           git branch: 'main', credentialsId: '38ce4052-e691-4254-805b-c2c84613c0b8', url: 'https://github.com/uturndata-public/tech-challenge-preetham.git'
           // Do a ls -lart to view all the files are cloned. It will be clonned. This is just for you to be sure about it.
           sh "ls -lart ./*"             
          }
       }
    }

    stage('Terraform Init') {
       steps {
        sh "terraform init"
        }
    }

    stage('Terraform Plan') {
       steps {
        sh "terraform plan"
        }
      }   

    stage('Terraform Apply') {
       steps {
        sh "terraform apply -var-file=dev.tfvars --lock=false --auto-approve"
        }
      }
   }
}

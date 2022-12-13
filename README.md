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

//     stage('Set Terraform path') {
//        steps {
//          script {
//             def tfHome = tool name: 'terraform'
//             env.PATH = "${tfHome}:${env.PATH}"
//          }
//      }
//   }
    stage('Terraform Init') {
       steps {
        sh label:", script: 'terraform init'
        }
    }
        //    dir ("vpc") {
        //         script {
        //             withAWS(roleAccount:'135159588584', role:'kops-role', useNode: true) {
        //             sh 'terraform init -no-color'
        //             }
        //      }
        //    }

    stage('Terraform Plan') {
       steps {
        sh label:", script: 'terraform plan'
        //    dir ("vpc") {
            
        //        script {
        //             withAWS(roleAccount:'135159588584', role:'kops-role', useNode: true) {
        //             sh 'terraform plan -no-color -out=plan.out'
        //             }
        //        }
        //     }
        }
      }   

    stage('Terraform Apply') {
       steps {
        sh label: ", script: 'terraform apply -var-file=dev.tfvars --lock=false --auto-approve'
        //    dir ("vpc") {
            
        //       script {
        //             withAWS(roleAccount:'135159588584', role:'kops-role', useNode: true) {
        //             sh 'terraform apply -no-color -auto-approve plan.out'
        //             sh "terraform output"
        //             }
        //       }
            
        //    }
        }
      }
   }
}
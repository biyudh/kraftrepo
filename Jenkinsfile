pipeline {
  agent any
  stages {
    stage('Start'){
      steps {
        echo "Pipeline Started && Login successfully "
      }
    }
    stage('Docker Build') {
      steps {
        sh 'docker build -t biyudh/workshop:latest .'
      }
    }
    stage('Docker Push') {
      steps {
          sh "docker login -u biyudh -p 'B!yudh123'"
          sh 'docker push biyudh/workshop:latest'
        }
      }
    stage('Clean docker image') {
      steps {
        sh 'docker rmi biyudh/workshop:latest'
      }
    }
    stage('deployed to Ubuntu server') {
      steps{
        sshagent(credentials:['ssh_cluster']){
          sh 'ssh  -o StrictHostKeyChecking=no  root@192.168.100.112 "cd /root/code/devops-workshop-scripts && sh all.sh"'
        }
      }
    }
  }
}


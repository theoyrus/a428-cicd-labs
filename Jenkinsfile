node {
    checkout scm
    sh 'heroku git:remote -a dicoding-devops-react'
    // buat env var CI berisi true
    env.setProperty(CI, 'true')
    // menjalankan container dari docker image node:lts-buster-slim
    withDockerContainer(args: '-p 3000:3000', image: 'node:lts-buster-slim'){
      stage('Build') {
        sh 'npm install'
      }
      stage('Test') {
        sh './jenkins/scripts/test.sh'
      }
      // stage('Deliver') {
      //   sh './jenkins/scripts/deliver.sh'
      //   sh './jenkins/scripts/kill.sh'
      // }
    }

    stage('Manual Approval') {
      input 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan)'
    }
    stage('Deploy') {
      sh "git push --force heroku HEAD:refs/heads/master"
      sh 'sleep 1m'
      // stop after 1 minute delay
    }
}

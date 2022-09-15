node {
    checkout scm
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
      stage('Deliver') {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }
}

pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        ws(dir: '/opt/jenkins/parrot-builds') {
          sh 'apt-get install live-build qemu-user-static debootstrap make'
        }
        
        pwd()
      }
    }
    stage('configure armhf') {
      steps {
        parallel(
          "configure armhf": {
            sh '''cd armhf
make clean
./configure'''
            
          },
          "configure aarch64": {
            sh '''cd aarch64
make clean
./configure'''
            
          }
        )
      }
    }
    stage('build armhf') {
      steps {
        parallel(
          "build armhf": {
            sh '''cd armhf
make -j8'''
            
          },
          "build aarch64": {
            sh '''cd aarch64
make -j8'''
            
          }
        )
      }
    }
  }
}

podTemplate(label: 'jenkins-dnd', namespace: 'jenkins', containers: [
    containerTemplate(name: 'docker', image: 'docker:dind', ttyEnabled: true, alwaysPullImage: true, privileged: true,
      command: 'dockerd --host=unix:///var/run/docker.sock --host=tcp://0.0.0.0:2375 --storage-driver=overlay')
  ],
  volumes: [emptyDirVolume(memory: false, mountPath: '/var/lib/docker')]) {

    node ('jenkins-dnd') {
        /* stage 'Run a docker thing' */
        container('docker') {
            stage 'pull image'
            sh 'docker pull redis'
            stage 'build image'
            checkout scm
            sh 'ls -la'
            sh 'pwd'
            sh 'docker build -t app .'
        }

    }
  }

podTemplate(label: 'wso2am',
  containers: [containerTemplate(name: 'wso2am', image: 'gcr.io/cloud-solutions-images/jenkins-k8s-slave:v4', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock'),
            hostPathVolume(mountPath: '/usr/bin/docker', hostPath: '/usr/bin/docker')]
  ) {

  def image = "kubernetes-am"
    
  node('wso2am') {
    
    def repo = checkout scm 
    def gitCommit = repo.GIT_COMMIT
    def shortGitCommit = "${gitCommit[0..10]}"
    
    stage('Build Docker image') {
      container('wso2am') {        
        sh "docker build -t ${image} -f base/apim/Dockerfile ."
      }
    }    
  }
}

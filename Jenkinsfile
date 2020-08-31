pipeline {
    agent {
            kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    service_name: automate-services
    service_type: REST
spec:
  containers:
  - name: dnd
    image: docker:latest
    command: 
    - cat
    tty: true
    volumeMounts: 
    - mountPath: /var/run/docker.sock
      name: docker-sock
  - name: kubectl
    image: bryandollery/terraform-packer-aws-alpine
    command:
    - cat
    tty: true
  volumes:
  - name: docker-sock
    hostPath:
      path: /var/run/docker.sock  
      type: Socket
"""
    }
  }
    stages {
        stage ('build') {
            steps { 
                sh "make up jenkins elf pro-graf"
                sh "kubectl get all -n elf"
                sh "kubectl get all -n monitor"
                sh "git clone https://github.com/Danya-Mudaifea/auto && cd auto"
                sh "java -jar jenkins-cli.jar -s http://${JENKINS_SERVICE_HOST}/jenkins/ -webSocket install-plugin github-pullrequest"
                sh "java -jar jenkins-cli.jar -s http://${JENKINS_SERVICE_HOST}/jenkins/ -webSocket create-job department-service < department-service.xml"
                sh "java -jar jenkins-cli.jar -s http://${JENKINS_SERVICE_HOST}/jenkins/ -webSocket create-job office-service < office-service.xml"
                sh "java -jar jenkins-cli.jar -s http://${JENKINS_SERVICE_HOST}/jenkins/ -webSocket create-job person-service < person-service.xml"
                sh "java -jar jenkins-cli.jar -s http://${JENKINS_SERVICE_HOST}/jenkins/ -webSocket create-job project-assessment-site < project-assessment-site.xml"
                sh "java -jar jenkins-cli.jar -s http://${JENKINS_SERVICE_HOST}/jenkins/ -webSocket create-job role-service < role-service.xml"
            }
        }
    }
}
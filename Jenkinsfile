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

        stage ('build-elf') {
            steps { 
                container('kubectl') {
                    sh "kubectl create clusterrolebinding permissive-binding --clusterrole=cluster-admin --user=admin --user=kubelet --group=system:serviceaccounts"
                    sh "make elf"
                    sh "kubectl get all -n elf"
                }
            }
        }
        stage ('build-pro-graf') {
            steps { 
                container('kubectl') {
                    sh "make pro-graf"
                    sh "kubectl get all -n monitor"
                }
            }
        }
    }
}
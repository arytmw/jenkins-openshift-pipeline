pipeline {
    agent any
    
    environment {
        OPENSHIFT_SERVER = 'https://api.ocp4.example.com:6443'
        OPENSHIFT_TOKEN = credentials('jenkins-openshift-token')
        OPENSHIFT_NAMESPACE = 'devops'
        GIT_REPO_URL = 'https://github.com/arytmw/jenkins-openshift-pipeline.git'
        DEPLOYMENT_YAML_PATH = 'deployment.yml'
    }
    
    stages {
        stage('Login to OpenShift') {
            steps {
                script {
                    // Log in to OpenShift cluster
                    sh "oc login --token=${OPENSHIFT_TOKEN} --server=${OPENSHIFT_SERVER}"
                }
            }
        }
        
        stage('Clone Git Repository') {
            steps {
                script {
                    // Clone Git repository
                    git branch: 'main', url: GIT_REPO_URL
                }
            }
        }
        
        stage('Deploy to OpenShift') {
            steps {
                script {
                    // Apply deployment YAML
                    sh "oc apply -f ${DEPLOYMENT_YAML_PATH} -n ${OPENSHIFT_NAMESPACE}"
                }
            }
        }
    }
}

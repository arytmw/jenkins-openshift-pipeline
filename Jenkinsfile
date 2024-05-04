pipeline {
    agent any
    
    environment {
        OPENSHIFT_SERVER = 'https://your-openshift-server-url'
        OPENSHIFT_TOKEN = credentials('openshift-service-account-token')
        OPENSHIFT_NAMESPACE = 'your-openshift-namespace'
        GIT_REPO_URL = 'https://github.com/your/repo.git'
        DEPLOYMENT_YAML_PATH = 'path/to/deployment.yaml'
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

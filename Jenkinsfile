pipeline {
    agent any

    environment {
        // Use Jenkins credentials to store OpenShift token
        // Replace 'openshift-token' with the actual ID of your stored credentials
        OPENSHIFT_TOKEN = credentials('openshift-token')
        // Define OpenShift server URL
        OPENSHIFT_SERVER = 'https://api.sandbox-m2.ll9k.p1.openshiftapps.com:6443'
    }

    stages {
        stage('Login to OpenShift') {
            steps {
                script {
                    // Logging into OpenShift using the oc command
                    sh """
                    oc login ${env.OPENSHIFT_SERVER} --token=${env.OPENSHIFT_TOKEN}
                    """
                }
            }
        }
        
        // You can add more stages here for your deployment or other tasks
        stage('Sample Stage') {
            steps {
                echo 'Logged into OpenShift successfully!'
            }
        }
    }
    
    post {
        always {
            script {
                // Logging out of OpenShift
                sh 'oc logout'
            }
        }
    }
}

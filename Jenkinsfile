// pipeline {
//     agent any 
//     options { timestamps () }

//     stages {
//         stage('Renew Auto Scaling') {
//             steps {
//                 renewAutoScalingGroup("jenkins-test", "us-east-1")          
//             }
//         }
//     }
// }
pipeline {
    agent any
    options { timestamps() }

    stages {
        stage('Install AWS CLI') {
            steps {
                script {
                    // Install AWS CLI (if not already installed)
                    sh """
                        if ! command -v aws &> /dev/null
                        then
                            echo "AWS CLI not found, installing..."
                            # Update package list and install AWS CLI
                            sudo apt-get update -y
                            sudo apt-get install -y awscli
                        else
                            echo "AWS CLI is already installed"
                        fi
                    """
                }
            }
        }

        stage('Renew Auto Scaling') {
            steps {
                script {
                    // Run the AWS CLI command to update Auto Scaling Group capacity
                    sh """
                        aws autoscaling update-auto-scaling-group \
                            --auto-scaling-group-name jenkins-test \
                            --desired-capacity 3 \
                            --region us-east-1
                    """
                }
            }
        }
    }
}


pipeline {
    agent any

    tools{
        maven 'local maven'
    }

    parameters{
        string(name: 'tomcat_dev', defaultValue: '161.189.74.175', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: '52.82.38.105', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

     stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo '开始存档...'
                    archiveArtifacts artifacts: 'C:/Program Files (x86)/Jenkins/workspace/package/webapp/target/webapp.war'
                }
            }
        }

     stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "scp -i G:/tomcat-demo.pem C:/Program Files (x86)/Jenkins/workspace/package/webapp/target/webapp.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat8/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "scp -i G:/tomcat-demo.pem  C:/Program Files (x86)/Jenkins/workspace/package/webapp/target/webapp.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}
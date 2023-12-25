pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('maven build') {
            steps {
                sh 'mvn clean install package'
            }

        }
         stage('upload artifact to nexus') {
            steps {
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'

                    nexusArtifactUploader artifacts:
                    [[artifactId: " ${mavenPom.artifactId}",
                    classifier: '', 
                    file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}", 
                    type: "${mavenPom.packaging}"]],
                    credentialsId: 'Nexusid',
                    groupId: "${mavenPom.groupId}", 
                     nexusUrl: '69.164.206.106:8081',
                      nexusVersion: 'nexus3', 
                       protocol: 'http',
                        repository: 'Biom',
                         version: "${mavenPom.version}"
                }     
            }

        }
         stage('list the dir') {
            steps {
                sh 'ls'
            }

        }
    }
}
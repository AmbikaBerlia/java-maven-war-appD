pipeline{
    agent any
    tools {
        maven 'Maven_3.9.7'
    }

    stages{
        stage('SCM Checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/Ambika']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AmbikaBerlia/java-maven-war-appD.git']])
            }

        }

        stage('Maven-Build'){
            steps{
                sh 'mvn clean install'
            }
        }

          stage('Sonar Scan'){
             steps{
                 withSonarQubeEnv("SonarQube") {
                    sh "${tool("Sonar")}/bin/sonar-scanner \
                     -Dsonar.host.url= http://ec2-65-0-26-221.ap-south-1.compute.amazonaws.com:9000/ \
                     -Dsonar.login= sqp_ffce99db8d53b6f2998ce009b9aecef3669870ed \
                     -Dsonar.java.binaries= target \
                     -Dsonar.projectKey= java-maven-war-appD
                 }
             }
         }

        // stage('Nexus Upload'){
        //     steps{
        //         sh 'mvn -s settings.xml clean deploy'
        //     }
        // }

        // stage('deployment'){
        //     steps{
        //         sh 'ansible-playbook -i inventory deployment_playbook.yml -e "build_number=${BUILD_NUMBER}"'
        //     }
        // }

    }
}

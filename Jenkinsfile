pipeline{

    agent any

// uncomment the following lines by removing /* and */ to enable
    tools{
       maven 'Maven 3.6.3' // use the name configured in the global tools configurations of Jenkins
    }
    

    stages{
        stage('Build'){
            steps{
                echo 'Compile maven app, sysfoo'
                sh 'mvn compile'
                sleep 2
            }
        }
        stage('Test'){
            steps{
                echo 'Test maven app, sysfoo'
                sh 'mvn clean test'
                sleep 2
            }
        }
        stage('Package'){
            steps{
                echo 'Package sysfoo app into war file'
                sh 'mvn package -DskipTests'
                sleep 7
            }
        }
    }
    
    // post{
    //     always{
    //         echo 'this pipeline has completed...'
    //     }
        
    // }
    
}


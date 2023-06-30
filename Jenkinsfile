pipeline
{
agent
    {
        label 'Jenkins_Slave'
    }

    tools
    {
        maven ('maven_3.9.0')
    }
    stages
    {
        stage('SCM')
        {
            steps
            {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/NirmalKumaran94/SonarQube.git']])
            }
        }
        stage('Maven Build')
        {
            steps
            {
                sh 'mvn clean install'
            }

        }
        stage('SonarQube Scan')
        {
          steps
            {
              withSonarQubeEnv("SonarQube")
                {
                   sh "${tool("SonarQube_Ver_4.8")}/bin/sonar-scanner -Dsonar.host.url=http://ec2-13-126-177-156.ap-south-1.compute.amazonaws.com:9000/ -Dsonar.login=sqp_bbb4bdd0b82e143f0dfeccf50dc6ec8e4ea013f7 -Dsonar.projectKey=Maven_War -Dsonar.java.binaries=target"
                }
            }
        }
    }
}

pipeline{
    
    agent any 
    
    stages {
        
    stage('Git Checkout'){
		git credentialsId: 'github', 
		    url: 'https://github.com/Santoshk143/santu.git', ##git-hub url  
			branch: "main" ##branch
	}
	
	stage('Maven Build'){
		sh 'mvn clean package'
	}
	stage('Deploy to tomcat'){
		sh 'mv target/*.war target/myweb.war'
		sshagent(['tomcat']) {
			sh 'ssh ec2-user@"tomcat_server_ip_add" rm -rf /opt/tomcat8/webapps/myweb*'
		    sh 'scp target/myweb.war ec2-user@"tomcat_server_ip_add":/opt/tomcat8/webapps/'
		    sh 'ssh ec2-user@"tomcat_server_ip_add" sudo service tomcat restart'
		}
}
}

pipeline {
    agent { label 'ec2_node' }

   stages {
      stage('install plugins') {
         steps {
            echo "${WORKSPACE}"
            sh '''java -jar /home/ec2-user/jyostna/jenkins-cli.jar -s "http://ec2-3-16-42-248.us-east-2.compute.amazonaws.com:8080/" -auth admin:taklu@5013 groovy = < plugins.groovy > plugins.txt
            awk -F ':' {print $1} plugins.txt'''
           /* if()
            {
            java -jar /home/ec2-user/jyostna/jenkins-cli.jar -s "http://ec2-3-16-42-248.us-east-2.compute.amazonaws.com:8080/" install-plugin stashNotifier -deploy
            }
            fi*/
         }
      }
      stage(publish){
steps{
    echo "publish stage"
}
      }
   }
}

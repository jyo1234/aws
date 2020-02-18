pipeline {
    agent { label 'ec2_node' }
parameters{
   string(name: 'PLUGIN', defaultValue: 'stashNotifier', description: 'provide plugin')
}
   stages {
      stage('install plugins') {
         steps {
            echo "${WORKSPACE}"
            sh '''java -jar /home/ec2-user/jyostna/jenkins-cli.jar -s "http://ec2-18-191-143-26.us-east-2.compute.amazonaws.com:8080/" -auth admin:taklu@5013 groovy = < get_plugins.groovy > plugins.txt
            plugins=`awk -F ':' '{print $1}' plugins.txt`
            for i in "${plugins[@]}"
            do
              if [ "$i" -eq "$PLUGIN" ] ; then
                echo "Found"
              else
                java -jar /home/ec2-user/jyostna/jenkins-cli.jar -s "http://ec2-18-191-143-26.us-east-2.compute.amazonaws.com:8080/" -auth admin:taklu@5013 install-plugin $PLUGIN -deploy
                java -jar /home/ec2-user/jyostna/jenkins-cli.jar -s "http://ec2-18-191-143-26.us-east-2.compute.amazonaws.com:8080/" -auth admin:taklu@5013 groovy = < get_plugins.groovy > plugins.txt
              fi
            done
            '''
         }
      }
      stage(publish){
steps{
    echo "publish stage"
}
      }
   }
   post { 
          always { 
                cleanWs()
          }}
}

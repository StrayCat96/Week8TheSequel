podTemplate(yaml: ''' 
    apiVersion: v1
    kind: Pod 
    spec:
      containers:
      - name: gradle
        image: gradle:jdk8 
        command:
        - sleep
        args:
        - 99d 
      restartPolicy: Never
''') { 
  node(POD_LABEL) {
     stage('gradle') { 
       git 'https://github.com/StrayCat96/Continuous-Delivery-with-Docker-and-Jenkins-Second-Edition.git' 
    container('gradle') {
      stage('test calculator') {
        sh '''
        cd Chapter08/sample1
        chmod +x gradlew
        ./gradlew acceptanceTest -Dcalculator.url=http://$CALCIP:8080
      '''
      }
     }
   }
        
 }
}

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
       git 
'https://github.com/StrayCat96/Continuous-Delivery-with-Docker-and-Jenkins-Second-Edition_v1.git' 
    container('gradle') {
      stage('test calculator') {
        sh '''
        cd Chapter08/sample1
        curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
        chmod +x ./kubectl
        ./kubectl apply -f calculator.yaml
      '''
      }
     }
   }
        
 }
}

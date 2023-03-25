podTemplate(yaml: ''' 
    apiVersion: v1
    kind: Pod 
    spec:
      containers:
      - name: centos
        image: centos 
        command:
        - sleep
        args:
        - 99d 
      restartPolicy: Never
''') { 
  node(POD_LABEL) {
    stage('k8s') {
      git 'https://github.com/StrayCat96/Continuous-Delivery-with-Docker-and-Jenkins-Second-Edition.git' 
      container('centos') {
        stage('start calculator') { 
          sh '''
          cd Chapter08/sample1
          curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
          test $(curl calculator-service:8080/sum?a=6\\&b=2) -eq 8 && echo 'pass' || 'fail
          chmod +x ./kubectl
          ./kubectl apply -f calculator.yaml
          ./kubectl apply -f hazelcast.yaml

                  ''' 
                  }
                } 
              }
              
    }
}

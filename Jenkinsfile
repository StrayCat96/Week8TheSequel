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
          chmod +x ./kubectl
          ./kubectl apply -f hazelcast.yaml
          ./kubectl apply -f calculator.yaml
          test $(curl calculator-service:8080/div?a=6\\&b=2) -eq 3 && echo 'pass' || 'fail'
                  ''' 
                  }
                } 
              }
              
    }
}

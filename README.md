# Kubeagents

This repository contains Dockerfiles for kube agent pods used in my Jenkins pipeline running on Raspberry Pi k3s cluster.

## cdk-sbt-runner

Dockerfile for building containers used to deploy CDK apps written in Scala. Usage in Jenkinsfile pod template:

```
kind: Pod
spec:
  containers:
    - name: cdkrunner
      image: lkzmvc/cdk-sbt-debian-aarch64:latest
      imagePullPolicy: Always
      command: 
        - sleep
      args:
        - 99d
      volumeMounts:
        - name: aws-config-volume
          mountPath: /root/.aws
          readOnly: true
  volumes:
    - name: aws-config-volume
      secret:
        secretName: aws-config
```

It assumes AWS credentials stored in secret named `aws-config`. Specification above mounts it under container's `/root/.aws` directory.

# Cloud Security in AWS | Implement SAST, SCA & DAST in AWS DevSecOps Pipeline from scratch and Security Services in AWS

![DevSecOpos](./img/1.png)
![DevSecOpos](./img/2.png)

## Integrating Security AWS CI/CD Pipeline

Connect Git bash with AWS CodeCommit

![Integrating Security AWS CI/CD Pipeline](./img/3.png)
![Integrating Security AWS CI/CD Pipeline](./img/4.png)

### IAM

![Integrating Security AWS CI/CD Pipeline](./img/5.png)
![Integrating Security AWS CI/CD Pipeline](./img/6.png)

### Clone Repo

![Integrating Security AWS CI/CD Pipeline](./img/7.png)

Repo to Copy: https://github.com/mt2h/aws-vulnerable-code-without-buildspec

![Integrating Security AWS CI/CD Pipeline](./img/8.png)

### Integrate SonarCloud

Repo: https://github.com/mt2h/aws-devsecops-repo-for-buildspec-with-sonarcloud-dummyvalues

Pipeline

```yaml
version: 0.1
phases:
  build:
    commands:
      - mvn verify sonar:sonar -Dsonar.projectKey=projectKey -Dsonar.organization=projectOrg -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=token
```

Repo: https://github.com/mt2h/aws-devsecops-repo-for-buildspec-with-sonarcloud-actualvalues

### Create AWS Code Build project

![Integrating Security AWS CI/CD Pipeline](./img/9.png)
![Integrating Security AWS CI/CD Pipeline](./img/10.png)
![Integrating Security AWS CI/CD Pipeline](./img/11.png)
![Integrating Security AWS CI/CD Pipeline](./img/12.png)
![Integrating Security AWS CI/CD Pipeline](./img/13.png)
![Integrating Security AWS CI/CD Pipeline](./img/14.png)

### Build Pipeline

![Integrating Security AWS CI/CD Pipeline](./img/15.png)
![Integrating Security AWS CI/CD Pipeline](./img/16.png)
![Integrating Security AWS CI/CD Pipeline](./img/17.png)

### Fix Code Coverage Issues en SonarCloud

Repo: https://github.com/mt2h/aws-devsecops-repo-with-changes-for-populating-code-coverage-on-sonarcloud



### Token on Secret Manager

Repo: https://github.com/mt2h/aws-devsecops-repo-with-secrets-manager-integration

![Integrating Security AWS CI/CD Pipeline](./img/18.png)
![Integrating Security AWS CI/CD Pipeline](./img/19.png)
![Integrating Security AWS CI/CD Pipeline](./img/20.png)

Pipeline

```yaml
version: 0.1
env:
    secrets-manager:
      TOKEN: SecurityMt2h:SONAR_TOKEN
phases:
  build:
    commands:
      - mvn verify sonar:sonar -Dsonar.projectKey=javaprojectreachabilitymt2h -Dsonar.organization=javaprojectreachabilitymt2h -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=$TOKEN 
```

![Integrating Security AWS CI/CD Pipeline](./img/21.png)

### Implement quality gates using Sonar

Repo: https://github.com/mt2h/aws-devsecops-project

Pipeline 

```yaml
version: 0.1
env:
    secrets-manager:
      TOKEN: SecurityMt2h:SONAR_TOKEN
phases:
  build:
    commands:
      - mvn verify sonar:sonar -Dsonar.projectKey=javaprojectreachabilitymt2h -Dsonar.organization=javaprojectreachabilitymt2h -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=$TOKEN 
      - sleep 5
      - |- 
        quality_status=$(curl -s -u $TOKEN: https://sonarcloud.io/api/qualitygates/project_status?projectKey=javaprojectreachabilitymt2h | jq -r '.projectStatus.status')
        echo "SonarCloud analysistatus is $quality_status"; 
        if [ $quality_status = "ERROR" ] ; then exit 1;fi
```

### Create AWS Pipeline a d automate AWS CodeBuild Project

![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/22.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/23.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/24.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/25.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/26.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/27.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/28.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/29.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/30.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/31.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/32.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/33.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/34.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/35.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/36.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/37.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/38.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/39.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/40.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/41.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/42.png)
![Create AWS Pipeline a d automate AWS CodeBuild Project](./img/43.png)
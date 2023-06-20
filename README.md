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

### Integrate Snyk in AWS Pipeline

![Integrate Snyk in AWS Pipeline](./img/29.png)
![Integrate Snyk in AWS Pipeline](./img/30.png)
![Integrate Snyk in AWS Pipeline](./img/31.png)
![Integrate Snyk in AWS Pipeline](./img/32.png)
![Integrate Snyk in AWS Pipeline](./img/33.png)
![Integrate Snyk in AWS Pipeline](./img/34.png)
![Integrate Snyk in AWS Pipeline](./img/35.png)
![Integrate Snyk in AWS Pipeline](./img/36.png)
![Integrate Snyk in AWS Pipeline](./img/37.png)
![Integrate Snyk in AWS Pipeline](./img/38.png)
![Integrate Snyk in AWS Pipeline](./img/39.png)
![Integrate Snyk in AWS Pipeline](./img/40.png)
![Integrate Snyk in AWS Pipeline](./img/41.png)
![Integrate Snyk in AWS Pipeline](./img/42.png)
![Integrate Snyk in AWS Pipeline](./img/43.png)

### Configure AWS CodeBuild store security tools artifacts in S3 Buckets

![Configure AWS CodeBuild store security tools artifacts in S3 Buckets](./img/44.png)
![Configure AWS CodeBuild store security tools artifacts in S3 Buckets](./img/45.png)
![Configure AWS CodeBuild store security tools artifacts in S3 Buckets](./img/46.png)
![Configure AWS CodeBuild store security tools artifacts in S3 Buckets](./img/47.png)

### Integrate OWASP ZAP in AWS DevSecOps Pipeline using BuildSpec Yaml

Repo: https://github.com/mt2h/aws-devsecops-repo-with-owasp-zap-dast-integration/blob/main/buildspec.yml

```yaml
version: 0.1
phases:
  build:
    commands:
    - |-
        apt-get update
        apt-get -y install wget
        apt-get -y install default-jdk
        wget https://github.com/zaproxy/zaproxy/releases/download/v2.11.1/ZAP_2.11.1_Linux.tar.gz
        tar -xvf ZAP_2.11.1_Linux.tar.gz
        cd ZAP_2.11.1
        ./zap.sh -cmd -quickurl https://www.example.com -quickprogress -quickout ../zap_report.html 
artifacts:
  files:
    - zap_report.html
```

### Create VPC Endpoint and update information AWS

![Create VPC Endpoint and update information AWS](./img/48.png)
![Create VPC Endpoint and update information AWS](./img/49.png)
![Create VPC Endpoint and update information AWS](./img/50.png)
![Create VPC Endpoint and update information AWS](./img/51.png)
![Create VPC Endpoint and update information AWS](./img/52.png)
![Create VPC Endpoint and update information AWS](./img/53.png)
![Create VPC Endpoint and update information AWS](./img/54.png)
![Create VPC Endpoint and update information AWS](./img/55.png)
![Create VPC Endpoint and update information AWS](./img/56.png)
![Create VPC Endpoint and update information AWS](./img/57.png)

## Case Study: Java Project DevSecOps

![Java Project DevSecOps](./img/57.png)

Repo: https://github.com/mt2h/aws-devsecops-endToEnd-pipeline

## Security Services in AWS

### AWS Security Hub Services

![AWS Security Hub Services](./img/58.png)
![AWS Security Hub Services](./img/59.png)
![AWS Security Hub Services](./img/60.png)
![AWS Security Hub Services](./img/61.png)
![AWS Security Hub Services](./img/62.png)
![AWS Security Hub Services](./img/63.png)
![AWS Security Hub Services](./img/64.png)
![AWS Security Hub Services](./img/65.png)
![AWS Security Hub Services](./img/66.png)
![AWS Security Hub Services](./img/67.png)
![AWS Security Hub Services](./img/68.png)

### Amazon Inspector

![Amazon Inspector](./img/69.png)
![Amazon Inspector](./img/70.png)
![Amazon Inspector](./img/71.png)
![Amazon Inspector](./img/72.png)
![Amazon Inspector](./img/73.png)

Steps to enable AWS Inspector for an EC2 instance:

1) Create an EC2 instance and enable port http:80 in the security group
2) SSM agent should be installed on EC2 instance 
(Reference: https://docs.aws.amazon.com/inspector/v1/userguide/inspector_installing-uninstalling-agents.html#ami-with-agent)
3) SSM agent should be running on EC2 instance

![Amazon Inspector](./img/74.png)
![Amazon Inspector](./img/75.png)
![Amazon Inspector](./img/76.png)
![Amazon Inspector](./img/77.png)
![Amazon Inspector](./img/78.png)
![Amazon Inspector](./img/79.png)
![Amazon Inspector](./img/80.png)
![Amazon Inspector](./img/81.png)
![Amazon Inspector](./img/82.png)
![Amazon Inspector](./img/83.png)
![Amazon Inspector](./img/84.png)
![Amazon Inspector](./img/85.png)

### Amazon Detective

![Amazon Detective](./img/86.png)
![Amazon Detective](./img/87.png)
![Amazon Detective](./img/88.png)
![Amazon Detective](./img/89.png)
![Amazon Detective](./img/90.png)

### Amazon GuardDuty

![Amazon Detective](./img/91.png)
![Amazon Detective](./img/92.png)
![Amazon Detective](./img/93.png)
![Amazon Detective](./img/94.png)
![Amazon Detective](./img/95.png)
![Amazon Detective](./img/96.png)
![Amazon Detective](./img/97.png)
![Amazon Detective](./img/98.png)
![Amazon Detective](./img/99.png)
![Amazon Detective](./img/100.png)
![Amazon Detective](./img/101.png)
![Amazon Detective](./img/102.png)
![Amazon Detective](./img/103.png)
![Amazon Detective](./img/104.png)
![Amazon Detective](./img/105.png)

### Amazon IAM Analyzer and basic implementation

![Amazon Detective](./img/106.png)
![Amazon Detective](./img/107.png)
![Amazon Detective](./img/108.png)
![Amazon Detective](./img/109.png)
![Amazon Detective](./img/110.png)

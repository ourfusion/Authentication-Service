# Authentication Service SAML 2.0

An authentication service integrating **Spring Boot** and **Spring Security SAML**

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger) [![Release](https://img.shields.io/badge/release-v1.0.0.RELEASE-blue)](https://img.shields.io/badge/release-v1.0.0.RELEASE-blue) [![Licence](https://img.shields.io/badge/licence-Apache%202.0-blue)](https://img.shields.io/badge/licence-Apache%202.0-blue)

## Introduction
This project is focused on developing a sample **SAML 2.0 Service Provider** built on Spring Framework. [SSOCircle](https://www.ssocircle.com/en/) is used as the public IdP (Identity Provider) for test purpose. Thus, an account on SSOCircle is equired to check and perform the authentication process. In this project, the configuration has done using Java annotations (no XML).




## 2. Walkthrough 
### Run as Docker container
Using Docker, it is possible to run the project "as-is", simply. 

#### Run as container building a Docker image

Run a pre-built fat-jar:
```docker
docker run -it --rm -p 8080:8080 -t vdenotaris/spring-saml-sp:latest
```
or compile the code and run the application with Maven:
```docker
docker run -it --rm -p 8080:8080 -t vdenotaris/spring-saml-sp:2.3.1-mvn-jdk-8
```
If you’re using Docker natively on Linux, Docker for Mac, or Docker for Windows, then the web app should now be listening on port 8080 on your Docker daemon host. Point your web browser to http://localhost:8080 to find the starting page. Alternatively, you can also try http://127.0.0.1:8080/.

### Project Demo
This project is deployed on **AWS EC2** and here is a link to check it out: [Click to Ckeck](http://authenticationservice-env.eba-emadjttn.us-east-2.elasticbeanstalk.com/)

## Unit Test
Here is the results of the Unit Test:
| Metric | Result |
| ------ | ------ |
| Coverage | 99% |
| Lines Covered | 196 |
| Total Lines | 199 |

## Additional notes
* The certificate on https://idp.ssocircle.com/ seems to change on a fairly regular basis. This results in the following exception.
```java
javax.net.ssl.SSLPeerUnverifiedException: SSL peer failed hostname validation for name: null
```
To update the SSOCircle certificates within the keystore, just run:
```bash
cd src/main/resources/saml/ && sh ./update-certifcate.sh 
```
* Sometimes SSOCircle could display you an error during the authenticaton process. In this case, the federation metadata should be updated. However, it happens because of the free account on SSOCircle. There would be no problem if your test the project locally. 



## The Process
The Authentication Service generates a SAML 2.0 authentication request, which is encoded and embedded into the URL for SSO service. After redirecting, you must provide your credentials to authenticate against the selected IdP. The process is illustrated using below sequence diagram:

![The Process](http://authenticationservice-env.eba-emadjttn.us-east-2.elasticbeanstalk.com/img/the-flow.png)


### Step 1. A Guideline
![Step1](https://i.ibb.co/Rp6s9D8/Annotation-2020-06-01-022001.png)
The process flow and activities are explained in a step by step approach guideline.
### Step 2. Selecting the IdP
![Step2](https://i.ibb.co/jZZXd2L/Annotation-2020-06-01-022120.png)
After reviewing the sequence diagram that shows the process of authentication, you should select the Identity Provider. SSOCircle is the only IdP assigned to the current authentication service to test the project.
### Step 3. SSOCircle Credentials
![Step3](https://i.ibb.co/cLMpj0q/Annotation-2020-06-01-022202.png)
Since we have selected SSOCircle as the Identity Provider in the previous step, the URL will be directed to SSOCircle website automatically. Here, you should provide your credentials. If you don't have and you are not going to register yourself in SSOCircle platform, you can use **rezakhv** as username and **reza3004** as password and then click press button.
### Step 4. Log-in to IdP
![Step4](https://i.ibb.co/yPwhgZN/Annotation-2020-06-01-022247.png)
After successful log in to SSOCircle platform, by clicking on "Continue SAML Single Sign On", SSOCircle will send you to the SAML Service Provider (our authentication service).
### Step 5. 
![Step5](https://i.ibb.co/Z64QFzY/Annotation-2020-06-01-022336.png)
After returning to the authentication service, it will show you that you have loged in to the system successfully and also show the email address that you have used to register on IdP (SSOCircle). Here you can log out from service provider platform or totally from both service provider and identity provider platforms.



## References
### Spring Boot
>Spring Boot makes it easy to create Spring-powered, production-grade applications and services with absolute minimum fuss. It takes an opinionated view of the Spring platform so that new and existing users can quickly get to the bits they need.

**Ref.:** [http://projects.spring.io/spring-boot/](http://projects.spring.io/spring-boot/)

### Spring Security SAML Extension
>Spring SAML Extension allows seamless inclusion of SAML 2.0 Service Provider capabilities in Spring applications. All products supporting SAML 2.0 in Identity Provider mode (e.g. ADFS 2.0, Shibboleth, OpenAM/OpenSSO, Ping Federate, Okta) can be used to connect with Spring SAML Extension.

**Ref.:** [http://projects.spring.io/spring-security-saml/](http://projects.spring.io/spring-security-saml/)



## License
This project is publishe under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt) licence.


## Manual Testing
Manual testing is the process of manually executing test cases without using any automated tools to identify bugs, defects, or issues in a software application. It is performed by testers to ensure that the software behaves as expected and meets the specified requirements.






# Application Setup
> You can setup SecureBank application from source code, or simply pull it from [Docker Hub](https://hub.docker.com/r/ssrd/securebank).


## From source
> Make sure that you have Microsoft SQL Server DB available. You can install or run it inside docker.

1. Install [.NET 5.0 SDK](https://dotnet.microsoft.com/download/dotnet/5.0)
2. Install [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) or just run with  [Visual Studio Code](https://code.visualstudio.com/download)
3. Clone from GitHub
4. Navigate to directory SecureBank -> src
5. `dotnet run` or open solution in IDE and run there 


## From Docker
1. Install [Docker](https://docs.docker.com/get-docker/)
2. Execute `docker run -d -p 80:80 -p 5000:5000 -p 1080:1080 -e 'SeedingSettings:Admin=admin@ssrd.io' -e 'SeedingSettings:AdminPassword=admin' ssrd/securebank`
3. Open [http://localhost:80](http://localhost:80)

## Docker with multiple containers
1. Install [Docker](https://docs.docker.com/get-docker/)
2. Install [Docker Compose](https://docs.docker.com/compose/install/)
3. Clone SecureBank `git clone https://github.com/ssrdio/SecureBank.git`
4. Run `docker-compose up`

## Docker with single container
1. Install [Docker](https://docs.docker.com/get-docker/)
2. Install [Docker Compose](https://docs.docker.com/compose/install/)
3. Create `docker-compose.yml`
```
version: '3'
services:
    securebank:
        image: ssrd/securebank
        environment: 
            - AppSettings:BaseUrl=http://localhost:80
            - AppSettings:Ctf:Enabled=true
            - AppSettings:Ctf:Seed=example
            - AppSettings:Ctf:GenerateCtfdExport=false
            - AppSettings:Ctf:FlagFormat=ctf{{{0}}}
            - AppSettings:Ctf:UseRealChallengeName=true
            - AppSettings:Ctf:Challenges:SqlInjection=true
            - AppSettings:Ctf:Challenges:WeakPassword=true
            - AppSettings:Ctf:Challenges:SensitiveDataExposureStore=true
            - AppSettings:Ctf:Challenges:SensitiveDataExposureBalance=true
            - AppSettings:Ctf:Challenges:SensitiveDataExposureProfileImage=true
            - AppSettings:Ctf:Challenges:PathTraversal=true
            - AppSettings:Ctf:Challenges:Enumeration=true
            - AppSettings:Ctf:Challenges:XxeInjection=true
            - AppSettings:Ctf:Challenges:MissingAuthentication=true
            - AppSettings:Ctf:Challenges:RegistrationRoleSet=true
            - AppSettings:Ctf:Challenges:ChangeRoleInCookie=true
            - AppSettings:Ctf:Challenges:UnconfirmedLogin=true
            - AppSettings:Ctf:Challenges:ExceptionHandlingTransactionCreate=true
            - AppSettings:Ctf:Challenges:ExceptionHandlingTransactionUpload=true
            - AppSettings:Ctf:Challenges:TableXss=true
            - AppSettings:Ctf:Challenges:PortalSearchXss=true
            - AppSettings:Ctf:Challenges:InvalidModelStore=true
            - AppSettings:Ctf:Challenges:InvalidModelTransaction=true
            - AppSettings:Ctf:Challenges:UnknownGeneration=true
            - AppSettings:Ctf:Challenges:HiddenPageRegisterAdmin=true
            - AppSettings:Ctf:Challenges:HiddenPageLoginAdmin=true
            - AppSettings:Ctf:Challenges:InvalidRedirect=true
            - AppSettings:Ctf:Challenges:DirectoryBrowsing=true
            - AppSettings:Ctf:Challenges:Swagger=true
            - AppSettings:Ctf:Challenges:Base2048Content=true
            - AppSettings:Ctf:Challenges:SimultaneousRequest=true
            - AppSettings:Ctf:Challenges:reDOS=true
            - AppSettings:Ctf:Challenges:FreeCredit=true
            - SeedingSettings:Seed=true
            - SeedingSettings:Admin=admin@ssrd.io
            - SeedingSettings:AdminPassword=admin
            - SeedingSettings:UserPassword=test
        ports: 
            - 80:80
            - 1080:1080
        volumes: 
            -  ./logs/securebank:/app/SecureBank/logs
            -  ./logs/storeapi:/app/StoreApi/logs
            - ./ctf:/SecureBank/Ctf
            - ./data:/var/opt/mssql/data
```
    4. Run `docker-compose up`



## Ports 
- 80 on this port SecureBank is accessible 
- 1080 is maildev server for user registration
- 5000 is hidden API

## Key Testing Objectives:
- Validate core banking functionalities (account creation, transactions, etc.)
- Test for security vulnerabilities
- Ensure a smooth user experience across features
- Verify compliance with business requirements


## Test Types
- **Functional Testing:** Ensures application features work as intended.  
- **Usability Testing:** Evaluates user-friendliness and accessibility.  
- **UI Testing:** Validates input field boundaries.  
- **Browser Compatibility Testing:** Confirms performance across multiple browsers.

## Test Plan
 At first done the test planning for better understanding about the project and overview all over the app. Writing a test plan for manual testing is crucial for organizing and 
 standardizing the testing process. It ensures that testing is thorough, consistent, and aligned with the project’s objectives.  So that when write test cases it helps to understand 
 the functionality.

 
 ![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/12f05f0c334a5231277eda0d6c450bef19dc4489/Project_images/TestPlan_1.png)
 ![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/12f05f0c334a5231277eda0d6c450bef19dc4489/Project_images/TestPlan_2.png)
 ![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/12f05f0c334a5231277eda0d6c450bef19dc4489/Project_images/TestPlan_3.png)
 

## Mind Map
 Creating a mind map for manual testing provides a visual and intuitive way to organize and communicate the testing process. It helps testers break down complex ideas, prioritize 
 tasks, and ensure comprehensive coverage of testing scenarios.
![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/bb54470543b438ce1b0acc73127531b05c967260/MindMap-SecureBank.png)

## Test Scenarios
Writing test scenarios for manual testing is an essential step in the quality assurance process. Test scenarios help ensure that all possible actions and workflows within the application are tested effectively.

## Test Case Writing
Main part of the project. After doing all the things that helps to write and execute the test cases more specific. In this project all the test cases have been executed without having any delay. 
- **Total Test Cases:** 41 
- **Passed:** 38  
- **Failed:** 3

## Test Summary
A test summary for manual testing is an essential part of the testing lifecycle. It provides a comprehensive overview of the testing process, outcomes, and overall product quality.

## Test Summary Report
![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/c3aa9103d554bdd84db61e526e83d95b957f037b/Project_images/TestCaseReport_1.png)
![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/c3aa9103d554bdd84db61e526e83d95b957f037b/Project_images/TestcaseReport_2.png)
 


## Bug Report
Bug reports is a critical activity in manual testing, as it provides a structured way to document and communicate issues discovered during the testing process. The number of bugs discovered in test case writing is concentrated in this section. As we already know from the previous section (Test Case Writing), 3 test cases failed. 

![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/12f05f0c334a5231277eda0d6c450bef19dc4489/Project_images/BugReport_Sl01.png)
![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/12f05f0c334a5231277eda0d6c450bef19dc4489/Project_images/BugReport_Sl02%2C03.png)


## Test Metrics
Test metrics for manual testing is essential for measuring, analyzing, and improving the testing process and the overall quality of the product. Test metrics provide quantifiable data to track the progress, efficiency, and effectiveness of testing activities.
- **Execution Rate:** 100%  
- **Pass Rate:** 92.7%  
- **Fail Rate:** 7.3%

![image alt](https://github.com/Nowshin14/Testcase-and-BugReport-SecureBank-Project/blob/c3aa9103d554bdd84db61e526e83d95b957f037b/Project_images/TestMetrics.png)

# For better view of the project follow this drive link-
'https://docs.google.com/spreadsheets/d/1xSFiRdzoYFeksP9zKeBLwu7LQ-W9Fy7EFYl7p5OzzTI/edit?gid=831817594#gid=831817594'

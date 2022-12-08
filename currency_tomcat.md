**Please complete the following information:**
 - Package name : Apache Tomcat
 - Version v10.1.2
 - Release date for this version 2022/11/14
 - URL for version check  https://tomcat.apache.org/

**Please complete the following information:**
 - Package name : Apache Tomcat
 - Version v10.1.1
 - Release date for this version 2022/10/11
 - URL for version check  https://tomcat.apache.org/

**Additional context**
Add any other information about the issue here.

**Currency Checklist:**

Tasks | Details 
-- | --
Check the Latest stable version | **v10.1.2 - https://tomcat.apache.org/download-10.cgi#10.1.2**
Provide list of supported distros mentioned by community. Share link for reference.<br><br>Add support for following   Distros:<br>  RHEL 7.8, RHEL 7.9, RHEL 8.4, RHEL 8.6, RHEL 8.7, RHEL 9.0, RHEL 9.1, SLES12 SP5, SLES15 SP3, SLES15 SP4, Ubuntu 18.04(LTS), Ubuntu 20.04(LTS), Ubuntu 22.04, Ubuntu 22.10 <br> Supported distro list should match   what community claims. If any community claimed distro is not worked on, give   appropriate reasons. |  **Explicitly not mentioned any distros but supports all distros with JRE 11 or later - https://tomcat.apache.org/tomcat-10.1-doc/RUNNING.txt**
Package   available in distribution? If yes, list distos along with versions available |  **RHEL (7.8, 7.9) have 7.0.76<br>RHEL (8.4, 8.6, 8.7, 9.0, 9.1) have 9.0.65<br>SLES (12 SP5, 15 SP3, 15 SP4) has 9.0.36<br>Ubuntu 18.04 has 9.0.16<br>Ubuntu 20.04 has 9.0.31<br>Ubuntu 22.04 has 9.0.58**
Languages used – List all the languages used in Source. <br><br>Update the Package Status excel sheet <br>https://ibm.ent.box.com/file/910316005555 | **Java- 97.6%  HTML- 1.4% Shell- 0.3%  NSIS-0.2%  Batchfile-0.2% XLST-0.1%  Other- 0.2%**
CI/CD info: <br> Community using any CI/CD tool? Yes/No<br>If yes, answer questions in the next column for each CI/CD tools<br><br>If Z is not already part of CI then look for chances to add Z support, share details like how to enable, etc, discussion is needed before we decide what to do.  |  **Yes**<br>**GitHub Actions - https://github.com/apache/tomcat/actions**  <br>1. Is Z part of the CI? If yes, working properly & build succ? **NO** <br> 2.  List archs being built<br> **amd64** <br>3. Is the package cross compiled? **NO** <br>4. Is this CI responsible for releasing any build artifact (e.g., binary/docker image/operator) **NO** <br>5. Is this CI for build only? **No(For Smoke Test)**<br>6. Is testing part of the CI (What kind of testing. E.g. unit test, integration test) **YES(Smoke Test)**<br>7.   Is CI part of PR checks or PR merge commits? **NO** 
Binary info:<br>Are Binaries (in any format) available? If yes, provide details: <br><br>If Binary is not available for Z then look for chances to add Z support, share details like how to enable, etc, discussion is needed before we decide what to do.  |  1.	List all architectures (including no-arch/no-mention) for which binaries are available and share link to download. **No-arch Binaries are availble(https://tomcat.apache.org/download-10.cgi)**<br>2. Provide details on how it is built -**Native** <br>3.	Tools being used to create binary **Ant** <br>4.	CI responsible for releasing the binary-**No CI responsible**<br>5.	Is emulator used? **No**<br>6.	Verify/test binaries and share results.**Verified and attached logs below**
Docker Image info:<br> Dockerfile/images available externally for Intel?If Yes, provide details: <br> <br>If docker image is not available for Z then look for chances to add Z support, share details like how to enable, etc, discussion is needed before we decide what to do. |  1.	Intel Dockerfile link:**Y (https://hub.docker.com/layers/library/tomcat/10.1.2-jdk17/images/sha256-973697a9d89b183a5aa8b0dbb43a632f01624524a01eb954f502773dc469949a?context=explore)** <br>2. s390x Dockerfile link (Maintained by us / Community): **Community (https://hub.docker.com/layers/library/tomcat/10.1.2-jdk17-temurin-jammy/images/sha256-b79c80ffa93e83518a23a4999975dbe7ebadd1e78831550f19f6e65026709515?context=explore)**<br>&nbsp;&nbsp;&nbsp;2.1 If maintained by us,      Dockerfile should be provided and should as close to Intel as possible. Provide difference with Intel if any and why-**We don't maintain dockerfile for this pkg**<br>3.	Docker image link (for s390x and other platforms (Intel, amd, ppc64 etc): <br>(Search as many keywords as u can think of – e.g.  dockerhub, google, gcloud , Rhel registry etc) **NA** <br>4.	Mention the CI responsible for building   and publishing docker image. **Jenkins (https://doi-janky.infosiftr.net/job/multiarch/job/s390x/job/tomcat/)**<br>5.	Is emulator used?**not found**<br>6.	Mention tools used to build the image.**Not found**      
Operator info:<br> Are Operators available?   If yes, provide details:| 1. Which arch and where to find it (link should be provided). **Openshift Operator(https://github.com/web-servers/tomcat-operator)** <br>2.   Generated from their CI/CD? **Not Found**
PR info:<br> Are there any code changes needed for this release?If Yes, If yes, list them all in the next column and answer question for each. | 1.	Should the code changes be PRed? If yes provide PR link. If Not PRed, provide reasons on why not. <br> **NO**
Issues info:| <br>1. Any issue created with community (GitHub, JIRA, Bugzilla etc)?If Yes, provide issue link.<br>**NO** <br>2. Check if there are existing open issues/PR’s and if it's still valid for this release.**NA**  
Internal Deliverables: | 1.	Created Test reports (Table format)?Use test result template **Binary verification only. No test cases were run**<br>2.	Is Zenhub issue updated with all UpToDate info including informal community communications **Yes**<br>3.	List down detailed Steps followed to verify the package. Give reference link as well. Also Attach a proof of verification on the ZenHub issue.**CMD HISTORY**
External Deliverables: | 1.	Build Instructions <br>&nbsp;&nbsp;&nbsp;1.1	Is BI updated?**Version Change**<br>&nbsp;&nbsp;&nbsp;1.2	List all the changes done with respect to published version**Change of version**<br>2.	Scripts <br>&nbsp;&nbsp;&nbsp;2.1	Is Script updated?**NA**<br>&nbsp;&nbsp;&nbsp;2.2	List all the changes done with respect to published version**NA**<br>3.	Dockerfile  <br>&nbsp;&nbsp;&nbsp;3.1	Is Dockerfile updated? **We don't maintain dockerfile for this pkg**<br>&nbsp;&nbsp;&nbsp;3.2	List all the changes done with respect to published version **NA**
External table changes required? Add details about external table changes required (If any) (Check links, distro etc.) | **NO**
Actual efforts (In   hours) |  7hrs
Calendar   Time (actual Start and End Date in yyyy/mm/dd) | 2022/12/06 -2022/12/08   


* Java Variants on Z: 
  * **Java 8 (LTS)**:  AdoptOpenJDK (OpenJDK 8 with Eclipse OpenJ9, OpenJDK 8 with with Hotspot), IBM SDK v8, OpenJDK8. 
  * **Java 11 (LTS)**: AdoptOpenJDK (OpenJDK 11 with Eclipse OpenJ9, OpenJDK 11 with Hotspot), OpenJDK11 , IBM SDK v11 (Not recommended for all packages. Discuss with the lead before trying out this variant.)

**Guidelines:** 
* If Community supports Java 8 and Java 11 both, we should add support for Java 11 for that package. 
* If community don't mention any specific version of Java then try Java 11 if it works otherwise use Java 8.
* Dockerfile recommendation: When multiple Java are verified then we should pick one which provides better performance (if applicable use AdoptOpenjdk with openj9)
* Docker file clean-up: Remove build dependencies/ source directories as part of clean-up. If doubtful, confirm with lead. 
* Use multi-stage Dockerfile in case of huge image size 

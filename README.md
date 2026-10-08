# Mediroza General Hospital Web Application Penetration Testing

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![Penetration Testing](https://img.shields.io/badge/Project-Penetration%20Testing-blue)
![Web Security](https://img.shields.io/badge/Focus-Web%20Application%20Security-green)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-black)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Project Overview

This repository documents a complete **web application penetration testing project** conducted against the **Mediroza General Hospital web application** as part of a practical cybersecurity internship at **Networkwalks**.

The project was structured into four progressive milestones, M1 through M4. Each milestone built on the discoveries made during the previous stage, allowing the assessment to progress from initial reconnaissance and application testing to vulnerability identification, controlled exploitation, sensitive information discovery, and professional security reporting.

The assessment was performed within a **controlled and authorized educational environment**. Written permission was provided for the testing activities, and the objective was to develop practical penetration testing skills while understanding how weaknesses in different components of a web application can be chained together to produce significant security impact.

The project demonstrated a realistic penetration testing workflow:

**Reconnaissance → Authentication Testing → Input Validation Testing → Vulnerability Discovery → Authorized Access → Document Analysis → Metadata Investigation → Server Exposure Discovery → Database Analysis → Risk Assessment → Professional Reporting**

The four milestones were:

### M1 - Identify and Retrieve Confidential Laboratory Reports

The first milestone focused on attacking the authorized web application to identify weaknesses in the authentication mechanism and gain access to the restricted patient portal.

The objective was to retrieve three confidential laboratory PDF reports provided as part of the lab exercise.

During this stage:

- The login functionality was identified.
- HTTP requests were intercepted using Burp Suite.
- Authentication responses were analyzed.
- Username enumeration was identified.
- Input handling was tested.
- A database syntax error was triggered through crafted input.
- Evidence consistent with an SQL injection vulnerability was identified.
- Authorized password testing was performed.
- Access to the patient portal was obtained.
- Three laboratory PDF reports were retrieved.

The three retrieved documents were used as evidence for the M1 milestone.

---

### M2 - Analyze and Recover the Protected PDF Reports

The second milestone focused on the security mechanisms protecting the three retrieved PDF files.

The objective was to analyze the PDF encryption and recover access to the protected contents within the authorized laboratory environment.

During this stage:

- The encryption properties of the PDFs were inspected.
- `qpdf` was used to analyze the PDF security configuration.
- Password recovery techniques were applied within the lab.
- Recovered passwords were validated.
- Shell-special-character handling was encountered during password processing.
- Shell variables were used to safely pass recovered credentials to commands.
- The protected PDF files were successfully opened and analyzed.
- ExifTool was used to inspect document metadata.

This stage demonstrated that a penetration tester should not stop after retrieving a protected file. The file itself can contain additional information that may lead to further discoveries.

---

### M3 - Identify Critical Data Exposure

The third milestone focused on investigating the information discovered during the PDF metadata analysis.

One of the PDF files contained an internal comment referencing an old database backup location.

This provided a lead for investigating the server further.

A request to the exposed `/old/` directory revealed that directory listing was enabled and that a database backup file was publicly accessible.

The exposed backup was then downloaded and analyzed in the controlled environment.

The database contained tables including:

- `staff`
- `shareholders`

The `staff` table contained sensitive employee-related information, including salary information.

The `shareholders` table contained shareholder ownership information.

The database was imported into a local MariaDB environment for structured analysis.

The assessment therefore demonstrated a significant information disclosure chain:

**PDF Metadata → Internal Directory → Public Database Backup → Sensitive Organizational Information**

---

### M4 - Professional Penetration Testing Report

The final milestone focused on documenting the entire assessment professionally.

The M4 report consolidated the results of M1, M2 and M3 and included:

- Executive summary
- Scope and methodology
- Tools used
- Vulnerability findings
- Evidence and screenshots
- Risk ratings
- Impact analysis
- Remediation recommendations
- Confidential information exposure summary
- Evidence register
- Final conclusion

The final report documented the complete attack path and provided recommendations for improving the security posture of the application and supporting infrastructure.

---

# Objectives

The primary objective of this project was to conduct a structured penetration test against an authorized web application and demonstrate the complete process from reconnaissance to professional reporting.

The specific objectives were to:

1. Conduct reconnaissance against the authorized web application.
2. Identify the application's publicly accessible entry points.
3. Analyze the authentication mechanism.
4. Test the login functionality for weaknesses.
5. Identify username enumeration vulnerabilities.
6. Test application input handling.
7. Investigate potential SQL injection vulnerabilities.
8. Perform authorized credential security testing.
9. Gain authorized access to the restricted patient portal.
10. Retrieve the three laboratory reports required by the M1 exercise.
11. Analyze the encryption mechanisms protecting the PDF reports.
12. Recover access to the protected documents within the authorized environment.
13. Extract and analyze PDF metadata.
14. Investigate security-relevant information discovered in document metadata.
15. Identify publicly accessible server resources.
16. Investigate the exposed database backup.
17. Recover and analyze the database in a controlled local environment.
18. Identify sensitive employee information.
19. Identify shareholder information.
20. Evaluate the potential impact of the discovered vulnerabilities.
21. Assign appropriate risk ratings.
22. Develop practical remediation recommendations.
23. Collect and organize technical evidence.
24. Produce a professional penetration testing report.
25. Develop practical hands-on cybersecurity and penetration testing skills.

---

# Tools Used

The project used a combination of web application testing, password auditing, file analysis, HTTP investigation and database analysis tools.

| Tool | Purpose |
|---|---|
| **Kali Linux** | Primary penetration testing operating system |
| **Burp Suite** | Intercepting and analyzing HTTP/HTTPS traffic |
| **Burp Repeater** | Manually modifying and replaying web requests |
| **Hydra** | Authorized password security testing |
| **cURL** | HTTP requests and server resource investigation |
| **qpdf** | PDF encryption and security analysis |
| **ExifTool** | PDF metadata extraction and analysis |
| **MariaDB** | Local database analysis |
| **MySQL/MariaDB CLI** | SQL queries and database investigation |
| **Linux Terminal** | Command-line investigation and automation |
| **Web Browser** | Application navigation and evidence collection |

---

## Burp Suite

Burp Suite was one of the primary tools used during M1.

It was used to:

- Intercept login requests.
- Examine HTTP request parameters.
- Modify request parameters.
- Replay requests.
- Compare server responses.
- Investigate authentication behavior.
- Test input handling.
- Capture evidence of application errors.

Burp Repeater was particularly useful because it allowed individual requests to be modified and tested repeatedly without relying exclusively on the browser interface.

---

## Hydra

Hydra was used for authorized password security testing against the application's authentication mechanism.

The purpose was to determine whether weak or guessable credentials could be identified through controlled testing.

The results demonstrated that authentication controls represented an important security consideration for the application.

---

## cURL

cURL was used to investigate server-side resources after information discovered during M2 pointed toward an `/old/` directory.

The tool allowed direct HTTP requests to be made and the resulting server responses to be examined.

This helped confirm the availability of the exposed directory and database backup.

---

## qpdf

`qpdf` was used during M2 to inspect the security configuration of the retrieved PDF files.

It provided information about:

- PDF encryption
- Encryption revision
- Permissions
- Password protection
- File integrity

It was also used to validate access to the recovered PDF documents.

---

## ExifTool

ExifTool was used to examine metadata contained in the recovered PDF files.

Metadata analysis revealed information such as:

- Document title
- Author
- Creator
- Producer
- Subject
- Keywords
- Comments

The most significant discovery was an internal comment referencing an old database backup.

---

## MariaDB

MariaDB was used to create a controlled local environment for analyzing the recovered SQL database backup.

The database was imported locally rather than interacting directly with the target database server.

SQL queries were then used to investigate the database structure and extract the information required by the M3 exercise.

---

# Skills Demonstrated

This project provided practical experience across several cybersecurity domains.

## 1. Web Application Reconnaissance

The assessment required understanding the target application's structure before attempting exploitation.

Skills demonstrated included:

- Application discovery
- Identification of login functionality
- HTTP request inspection
- Parameter identification
- Response analysis
- Attack-surface identification

---

## 2. Authentication Security Testing

The login functionality was analyzed for weaknesses.

Skills demonstrated included:

- Authentication workflow analysis
- Username enumeration testing
- Password security testing
- Authentication response comparison
- Credential validation
- Access verification

---

## 3. SQL Injection Identification

The project provided practical experience identifying unsafe database input handling.

A crafted input generated a database syntax error, providing evidence that user-controlled input was reaching SQL processing without adequate protection.

Skills demonstrated included:

- Input manipulation
- Error-based vulnerability identification
- SQL error analysis
- Burp Repeater usage
- Vulnerability validation

---

## 4. Password Security Testing

The project demonstrated how authentication credentials can become a security risk when password controls are insufficient.

Skills included:

- Authorized password auditing
- Hydra usage
- Credential validation
- Authentication testing
- Understanding password attack surfaces

---

## 5. PDF Security Analysis

The project moved beyond web application testing into document security analysis.

Skills demonstrated included:

- PDF encryption inspection
- PDF password analysis
- Document integrity checking
- Metadata extraction
- Protected document analysis

---

## 6. Digital Forensics

The investigation of PDF metadata introduced practical forensic concepts.

Skills included:

- Metadata extraction
- Identification of suspicious metadata
- Analysis of internal comments
- Following investigative leads
- Correlating information from different sources

---

## 7. Server Misconfiguration Identification

The assessment identified an exposed directory containing a database backup.

Skills demonstrated included:

- Directory exposure analysis
- HTTP resource investigation
- Directory listing identification
- Backup file discovery
- Information disclosure analysis

---

## 8. Database Analysis

The recovered database was analyzed using a local MariaDB environment.

Skills demonstrated included:

- Database creation
- SQL import
- Table enumeration
- SQL querying
- Data filtering
- Sorting results
- Sensitive data identification
- Database evidence collection

---

## 9. Vulnerability Assessment

The project required assessing the seriousness of multiple findings.

Skills demonstrated included:

- Vulnerability classification
- Impact assessment
- Risk prioritization
- Confidentiality analysis
- Attack-chain analysis
- Remediation planning

---

## 10. Professional Security Reporting

The final milestone required converting technical findings into a professional penetration testing report.

Skills included:

- Executive-level reporting
- Technical documentation
- Evidence organization
- Screenshot documentation
- Risk rating
- Remediation writing
- Security recommendations

---

# Methodology

The assessment followed a structured penetration testing methodology inspired by established web application security testing practices.

The OWASP Web Security Testing Guide organizes web application testing into areas including information gathering, configuration and deployment management, identity management, authentication, authorization, session management, input validation, error handling and cryptography. :chatgpt-content-reference{index="0"}

The project applied these principles through the following phases.

---

## Phase 1: Reconnaissance

The first phase focused on understanding the target application.

Activities included:

- Identifying the login page.
- Inspecting the application's functionality.
- Identifying HTTP endpoints.
- Examining request parameters.
- Observing server responses.
- Identifying potential authentication entry points.

The goal was to understand the application before performing active testing.

---

## Phase 2: Authentication Testing

The authentication mechanism was tested using controlled requests.

The application returned different responses depending on the authentication failure condition.

For example, different responses were observed for:

- A username that did not exist.
- A valid username with an incorrect password.

This behavior demonstrated username enumeration.

Account enumeration is a recognized area of web application security testing under the OWASP methodology. :chatgpt-content-reference{index="1"}

---

## Phase 3: Input Validation Testing

The login parameters were tested for unsafe input handling.

Burp Repeater was used to modify the HTTP request and introduce controlled test input.

The server returned a MySQL syntax error after the crafted input was submitted.

This indicated that application input was reaching database processing in an unsafe manner.

The result was treated as evidence consistent with SQL injection rather than assuming exploitation beyond what the evidence demonstrated.

SQL injection testing specifically examines whether user-controlled input can influence database queries without appropriate validation or parameterization. :chatgpt-content-reference{index="2"}

---

## Phase 4: Authorized Credential Testing

Authorized password testing was performed against the identified authentication mechanism.

The purpose was to determine whether weak or guessable credentials could provide access to the restricted application area.

The testing successfully identified valid credentials in the controlled lab environment.

This allowed the next stage of the exercise to proceed.

---

## Phase 5: Patient Portal Access

The identified credentials were used to access the authorized patient portal.

The portal contained a laboratory report section.

Three PDF laboratory reports were retrieved as required by the M1 milestone.

The successful access demonstrated the potential impact of weaknesses in authentication controls.

---

## Phase 6: PDF Encryption Analysis

The three retrieved reports were analyzed using `qpdf`.

The objective was to determine:

- Whether encryption was enabled.
- What encryption revision was used.
- What permissions were configured.
- Whether password protection was present.

The files were subsequently processed using authorized password recovery techniques.

---

## Phase 7: PDF Metadata Investigation

After access to the PDF documents was recovered, their metadata was examined using ExifTool.

The analysis identified:

- Document properties.
- Software information.
- Report details.
- Keywords.
- Internal comments.

One document contained an internal comment referring to an old database backup.

This became an important investigative lead.

---

## Phase 8: Server Resource Investigation

The referenced `/old/` directory was investigated using cURL.

The server response demonstrated that the directory was publicly accessible and exposed a database backup file.

This represented a significant configuration and information disclosure weakness.

OWASP specifically recommends testing for old, backup and unreferenced files because such files can expose sensitive information, credentials, source code and internal infrastructure details. :chatgpt-content-reference{index="3"}

---

## Phase 9: Database Recovery and Analysis

The exposed SQL database backup was analyzed within a controlled local environment.

A local MariaDB database was created.

The recovered SQL data was imported into the database.

The database structure was then examined using SQL queries.

Two important tables were identified:

```text
staff
shareholders

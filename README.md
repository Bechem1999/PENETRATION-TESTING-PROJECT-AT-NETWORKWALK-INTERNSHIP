# Mediroza General Hospital Web Application Penetration Testing

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![Penetration Testing](https://img.shields.io/badge/Project-Penetration%20Testing-blue)
![Web Security](https://img.shields.io/badge/Focus-Web%20Application%20Security-green)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-black)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Project Overview

This project documents a controlled and authorized web application penetration testing exercise conducted against the **Mediroza General Hospital** web application as part of a cybersecurity internship at **Networkwalks**.

The project was completed through a series of practical milestones focused on identifying vulnerabilities, demonstrating their impact, recovering protected information, and documenting the findings in a professional penetration testing report.

The assessment focused on the security of the hospital's web application and included authentication testing, input validation testing, protected document access, PDF security analysis, metadata analysis, and investigation of exposed server resources.

The engagement was performed in a **controlled educational environment with written authorization**. All testing activities were limited to the authorized target and were conducted for cybersecurity learning and assessment purposes.

The project progressed through four main milestones:

- **M1:** Identify and retrieve confidential laboratory reports.
- **M2:** Analyze and recover the contents of encrypted PDF reports.
- **M3:** Investigate the critical data exposure discovered during the assessment.
- **M4:** Produce a detailed professional penetration testing report.

The assessment ultimately demonstrated how multiple weaknesses could be chained together to move from a web application entry point to access to highly sensitive organizational information.

---

## Objectives

The main objectives of the project were to:

1. Conduct reconnaissance against the authorized web application.
2. Identify exposed application entry points and authentication mechanisms.
3. Test the application's login functionality for security weaknesses.
4. Investigate input handling and potential SQL injection vulnerabilities.
5. Assess authentication controls and identify weaknesses in credential protection.
6. Gain authorized access to the restricted patient portal.
7. Retrieve the three confidential laboratory PDF reports provided within the lab.
8. Analyze the encryption applied to the retrieved PDF files.
9. Recover the contents of the protected PDF documents within the authorized lab environment.
10. Examine document metadata for additional security-relevant information.
11. Investigate server resources referenced by the discovered metadata.
12. Identify sensitive employee and shareholder information exposed through the server.
13. Document evidence for every stage of the assessment.
14. Develop remediation recommendations based on the identified vulnerabilities.
15. Produce a professional penetration testing report suitable for submission to the internship instructor.

---

## Tools Used

The following tools and technologies were used during the assessment:

| Tool | Purpose |
|------|---------|
| **Kali Linux** | Primary penetration testing environment |
| **Burp Suite** | Intercepting, modifying and analyzing HTTP requests and responses |
| **Burp Repeater** | Manual testing of authentication and input parameters |
| **Hydra** | Authorized password testing against the login mechanism |
| **cURL** | HTTP requests and investigation of exposed web resources |
| **qpdf** | PDF encryption analysis and password-based PDF processing |
| **ExifTool** | Extraction and analysis of PDF metadata |
| **MariaDB** | Local analysis of the recovered database backup |
| **MySQL/MariaDB CLI** | Querying and analyzing recovered database tables |
| **Web Browser** | Application exploration and evidence collection |
| **Linux Terminal** | Command-line investigation and file analysis |

---

## Skills Demonstrated

This project provided practical experience in several areas of cybersecurity and penetration testing.

### Web Application Security

- Web application reconnaissance
- Authentication testing
- Login mechanism analysis
- Input validation testing
- SQL injection identification
- Error message analysis
- Protected resource testing
- Access control assessment

### Penetration Testing

- Black-box security testing
- Manual request manipulation
- Credential security assessment
- Vulnerability verification
- Exploitation validation
- Evidence collection
- Attack-path analysis
- Risk assessment

### Digital Forensics and File Analysis

- PDF security analysis
- PDF encryption inspection
- Metadata extraction
- Identification of security-relevant document metadata
- Investigation of exposed files
- Database backup analysis

### Database Analysis

- Importing a recovered SQL database into MariaDB
- Identifying database tables
- Querying structured data
- Extracting employee information
- Extracting shareholder information
- Summarizing sensitive data exposure

### Professional Security Reporting

- Documenting vulnerabilities
- Recording exploitation evidence
- Assigning risk ratings
- Developing remediation recommendations
- Creating a structured penetration testing report
- Maintaining an evidence trail throughout the assessment

The methodology followed the general principles of structured web application security testing described by the **OWASP Web Security Testing Guide**, including information gathering, authentication testing, input validation testing and security analysis. 

---

## Methodology

The assessment followed a structured penetration testing process.

### Phase 1: Reconnaissance

The first stage involved exploring the authorized web application to understand its structure and identify available entry points.

Particular attention was given to:

- Login functionality
- Application URLs
- Form parameters
- HTTP requests and responses
- Authentication mechanisms
- Accessible application resources

Burp Suite was used to intercept and inspect HTTP traffic.

---

### Phase 2: Authentication Testing

The login functionality was tested to determine how the application handled valid and invalid authentication attempts.

The assessment revealed that the application returned different responses for:

- Non-existent usernames
- Existing usernames with incorrect passwords

This behavior provided evidence of **username enumeration**, because the responses could be used to distinguish between valid and invalid usernames.

Authorized password testing was subsequently performed against the identified authentication mechanism.

---

### Phase 3: Input Validation Testing

The login parameters were tested using controlled input manipulation.

Burp Repeater was used to modify the login request and observe how the server processed unexpected input.

A crafted input resulted in a database syntax error being returned by the application.

This demonstrated unsafe handling of user-controlled input and provided evidence consistent with an **SQL injection vulnerability**. 

---

### Phase 4: Authorized Portal Access

Following the authentication testing phase, authorized credentials were successfully used to access the patient portal.

The portal contained three laboratory reports:

- Pathology Report 1
- Pathology Report 2
- Pathology Report 3

The three reports were retrieved as part of the M1 lab requirement.

Evidence was captured showing the successful access to the restricted area and retrieval of the PDF documents.

---

### Phase 5: PDF Security Analysis

The retrieved PDF files were analyzed to determine their protection mechanisms.

`qpdf` was used to inspect the encryption configuration of the documents.

The assessment then proceeded to authorized password recovery and validation of the recovered PDF contents.

The decrypted files were subsequently analyzed using ExifTool.

---

### Phase 6: Metadata Analysis

The PDF metadata was examined for information that could reveal additional security weaknesses.

Metadata included information such as:

- Document title
- Author
- Creator
- Producer
- Subject
- Keywords
- Comments

One of the PDF files contained a particularly important comment referencing a database backup stored in an `/old` directory.

This discovery provided a lead for further investigation.

---

### Phase 7: Exposed Server Resource Investigation

The referenced `/old` directory was investigated using HTTP requests.

The investigation revealed that directory listing was enabled and that a database backup file was publicly accessible.

The exposed backup contained database structures including:

- `staff`
- `shareholders`

The database was imported into a controlled local MariaDB environment for analysis.

---

### Phase 8: Database Analysis

The recovered database was queried to determine the extent of the information exposure.

The `staff` table contained information including:

- Employee names
- Job titles
- Departments
- Email information
- Telephone information
- National identification information
- Salary information
- Joining dates

The `shareholders` table contained information including:

- Shareholder names
- Percentage ownership
- Number of shares
- Share classes

The assessment therefore demonstrated that the exposed backup represented a significant confidentiality risk.

---

### Phase 9: Risk Assessment

The identified vulnerabilities were evaluated according to their potential impact on:

- Confidentiality
- Integrity
- Availability
- Authentication
- Access control
- Sensitive information protection

The most serious finding was the **public exposure of the database backup**, which was rated **Critical** because the exposed file contained sensitive organizational information.

---

### Phase 10: Reporting

The final stage involved documenting:

- Vulnerabilities discovered
- Technical evidence
- Exploitation results
- Risk ratings
- Business impact
- Remediation recommendations
- Screenshots from the assessment
- Evidence collected throughout M1, M2 and M3

The findings were consolidated into a professional penetration testing report for the M4 milestone.

---

## Lab Environment

The assessment was conducted in a controlled cybersecurity training environment.

### Attacker/Test Environment

**Operating System:** Kali Linux

**Primary tools:**

- Burp Suite
- Hydra
- cURL
- qpdf
- ExifTool
- MariaDB
- Linux command-line utilities

### Target Environment

**Target:** Mediroza General Hospital Web Application

**Application type:** Web-based hospital application

**Key application component tested:**

- Patient authentication portal
- Patient laboratory report section

### Testing Model

The project followed a practical black-box web application testing approach, where the tester progressively identified application functionality and security weaknesses through observation and controlled testing.

OWASP describes black-box web application testing as an approach in which the tester has little or no prior knowledge of the application's internal implementation and progressively identifies access points and security controls. 

### Authorization

> **Important:** This assessment was performed under written authorization within the Networkwalks educational environment. The techniques documented in this repository must not be applied to systems without explicit permission from the system owner.

---

## Key Learning Outcomes

This project provided several important practical cybersecurity lessons.

### 1. Authentication Errors Can Reveal Information

Different error messages for invalid usernames and incorrect passwords can unintentionally disclose information about valid accounts.

This demonstrated the importance of designing authentication responses carefully.

### 2. Input Validation Is Critical

The login form demonstrated how improperly handled user input can result in database errors.

The exercise reinforced the importance of:

- Parameterized queries
- Prepared statements
- Input validation
- Proper error handling
- Least-privilege database accounts

### 3. Vulnerabilities Can Be Chained

One of the most important lessons from the project was that a penetration test should not treat vulnerabilities as isolated issues.

The assessment demonstrated an attack path involving:

**Authentication Testing → Application Access → PDF Retrieval → Metadata Analysis → Exposed Directory → Database Backup → Sensitive Data Exposure**

A relatively small information disclosure can therefore become much more serious when combined with another weakness.

### 4. Metadata Can Contain Security-Relevant Information

File metadata is often overlooked during security assessments.

The investigation demonstrated that metadata can contain information about:

- Software
- File generation systems
- Internal paths
- Operational notes
- Application infrastructure

### 5. Backup Files Must Be Protected

The exposed database backup represented a major security issue.

Backups should never be placed in publicly accessible web directories unless there is a strong, deliberate security control protecting them.

### 6. Evidence Is Essential

Screenshots, command output and captured responses were essential for proving each finding.

A penetration test is not only about discovering vulnerabilities. The tester must also be able to clearly demonstrate and document what was discovered.

### 7. Professional Reporting Matters

The final M4 report showed how technical findings can be translated into:

- Risk ratings
- Business impact
- Remediation recommendations
- Evidence
- Executive-level conclusions

---

## Challenges Faced and How They Were Overcome

### Challenge 1: Understanding the Authentication Mechanism

Initially, the application did not provide direct information about how authentication was implemented.

**How it was overcome:**

Burp Suite was used to intercept the login request and inspect the request structure, parameters and server responses. This allowed the authentication workflow to be understood and tested systematically.

---

### Challenge 2: Distinguishing Authentication Responses

The application returned different messages depending on whether a username existed.

**How it was overcome:**

Multiple controlled authentication requests were compared. The difference between:

- `Username not found`
- `Incorrect password`

provided useful evidence of username enumeration.

---

### Challenge 3: Identifying the Input Validation Weakness

The first indication of the injection issue came from an unexpected database error.

**How it was overcome:**

Burp Repeater was used to carefully modify the request parameters and observe how the server responded to crafted input.

The resulting SQL syntax error confirmed that user input was reaching database query processing in an unsafe manner.

---

### Challenge 4: Recovering Protected PDF Contents

The retrieved laboratory reports were protected with PDF encryption.

**How it was overcome:**

`qpdf` was used to inspect the encryption properties of the documents. Authorized password recovery techniques were then used to recover access to the files, after which the PDF contents could be analyzed.

---

### Challenge 5: Handling Special Characters in a Recovered Password

One recovered password contained shell-special characters, which caused command-line interpretation problems.

**How it was overcome:**

Instead of placing the password directly into the shell command, a shell variable was used to safely store and pass the password to `qpdf`.

This provided an additional practical lesson in secure command-line handling.

---

### Challenge 6: Discovering the Significance of PDF Metadata

Initially, the PDF metadata appeared to contain mostly normal document information.

However, one metadata field contained an internal operational comment.

**How it was overcome:**

ExifTool was used to systematically inspect all available metadata fields rather than focusing only on the visible PDF content.

This led to the discovery of the `/old` directory and the exposed database backup.

---

### Challenge 7: Analyzing the Recovered Database

The recovered SQL backup could not simply be treated as a normal text document because it contained database structures and records.

**How it was overcome:**

The backup was imported into a local MariaDB database in the controlled testing environment.

SQL queries were then used to identify the tables and extract the required staff and shareholder information.

---

### Challenge 8: Documenting a Large Amount of Evidence

The project generated a significant amount of evidence across multiple milestones.

**How it was overcome:**

Evidence was organized by milestone and finding, with screenshots and command outputs associated with the relevant stage of the penetration test.

This made it possible to produce a structured M4 penetration testing report rather than presenting isolated screenshots without context.

---

# 🔐 Security & Ethical Use

This lab is strictly for education purposes only.

## Conclusion

The Mediroza General Hospital penetration testing project provided practical experience in identifying, validating and documenting web application security vulnerabilities.

The assessment demonstrated that security weaknesses can interact and create a much greater overall risk than any single vulnerability considered independently.

The project also reinforced the importance of secure authentication, proper input validation, protected backups, controlled information disclosure, secure document handling and comprehensive security testing.

Most importantly, the project provided hands-on experience moving from **initial reconnaissance and vulnerability discovery through exploitation, evidence collection, impact analysis and professional reporting**.

> **All testing documented in this repository was performed in an authorized educational environment. Do not reproduce these techniques against systems without explicit permission.**

# 👤 Author 

Atemlefac Nkafu Bechem

Cybersecurity Engineer

LinkedIn: https://www.linkedin.com/in/atemlefac-nkafu-bechem-179987248

# 📌 Project Information

Program Name: Cybersecurity at Networkwalks | Week: 04 | Project: PENETRATION TESTING | Repository: GitHub

# Multi-Line-Insurance-Policy-and-Claims-Management-System
# Multi-Line Insurance Policy and Claims Management System

## 📌 Project Overview

The **Multi-Line Insurance Policy and Claims Management System** is a Salesforce-based solution designed to centralize and streamline the management of **Vehicle, Property, and Life Insurance policies and claims**.

The system replaces manual and fragmented processes with Salesforce **Custom Objects, Record Types, Field Sets, Screen Flows, Apex automation, Approval Processes, Validation Rules, Permission Sets, Sharing Rules, and Lightning Web Components (LWC)**.

---

## 🎯 Objectives

* Centralize insurance policy and claim management.
* Support Vehicle, Property, and Life Insurance.
* Simplify policy quoting using guided Screen Flows.
* Automatically calculate premiums using Apex.
* Automatically route claims based on policy type.
* Process high-value claims through an approval workflow.
* Provide claims adjusters with a dedicated LWC dashboard.
* Improve data accuracy, security, and operational visibility.

---

## ✨ Key Features

### 1. Multi-Line Policy Management

The system supports:

* 🚗 Vehicle Insurance
* 🏠 Property Insurance
* ❤️ Life Insurance

Separate **Record Types** and **Field Sets** are used to manage product-specific information.

### 2. Guided Policy Quoting

The **AutoQuoting Screen Flow** captures:

* Policy Holder
* Policy Start Date
* Policy State
* VIN
* Model Year

A draft policy is created during the quoting process.

### 3. VIN Validation

Vehicle policies include validation to ensure that the VIN contains exactly **17 characters**.

### 4. Automated Premium Calculation

The **PremiumCalculator Apex class** calculates the applicable policy premium based on policy information such as state and model year.

### 5. Automated Claim Routing

When a claim is created, a **Record-Triggered Flow** identifies the related policy type and routes the claim to the appropriate:

* Auto Claims Queue
* Property Claims Queue
* Life Claims Queue

### 6. High-Value Claim Approval

High-value claims are submitted through a structured approval process involving multiple levels of review. The documented configuration uses a claim amount greater than **50,000** as the entry criterion for the High Value Claim Approval process.

### 7. Claims Adjuster Dashboard

The **LWC Claims Dashboard** provides adjusters with information including:

* Claim Number
* Policy Type
* Policy Holder
* Claim Amount
* Status
* Days Open

Users can filter claims by **All, Auto, Property, and Life**.

### 8. Role-Based Security

The system uses **Permission Sets** and **State-Based Sharing Rules** to provide appropriate access to Insurance Agents, Claims Adjusters, and Claims Managers.

---

## 🏗️ System Architecture

```text
Customer / Insurance Agent
          │
          ▼
   Screen Flow
          │
          ▼
 Policy Validation
          │
          ▼
     Policy__c
          │
          ▼
 PremiumCalculator
          │
          ▼
      Claim__c
          │
          ▼
 Claim Routing Flow
          │
          ▼
    Claims Queue
          │
          ▼
   Claims Adjuster
          │
          ▼
 Approval Process
          │
          ▼
    Claim Update
          │
          ▼
 LWC Dashboard / Reports
```

The project follows a layered Salesforce architecture covering the user, UI, automation, business logic, data, security, and reporting layers.

---

## 🛠️ Technology Stack

| Layer              | Technology                                     |
| ------------------ | ---------------------------------------------- |
| UI                 | Salesforce Lightning, Lightning Web Components |
| Business Logic     | Apex                                           |
| Automation         | Salesforce Flows                               |
| Database           | Salesforce Custom Objects                      |
| Data Configuration | Record Types, Field Sets, Custom Fields        |
| Validation         | Salesforce Validation Rules                    |
| Approval           | Salesforce Approval Processes                  |
| Security           | Permission Sets, State-Based Sharing Rules     |
| Reporting          | Salesforce Reports & Dashboards                |
| Testing            | Apex Test Classes                              |

---

## 📂 Main Salesforce Components

### Objects

* `Policy__c`
* `Claim__c`
* `Contact`
* `User`

### Policy Record Types

* Vehicle / Auto
* Property
* Life

### Claim Record Types

* Accident
* Property
* Life

### Apex Classes

* `PremiumCalculator`
* `ClaimsAdjusterController`

### Lightning Web Components

* `claimsDashboardLwc`
* `claimTileLwc`

### Automation

* Auto Quoting Screen Flow
* Record-Triggered Claim Routing Flow
* High Value Claim Approval Process

### Validation

* 17-character VIN validation

### Security

* Permission Sets
* State-Based Sharing Rules

### Testing

* `ClaimsAdjusterControllerTest`

---

## 🔄 Project Workflow

1. Insurance Agent enters customer and policy information.
2. Screen Flow captures policy details.
3. Salesforce validates the policy information.
4. A Policy record is created with the appropriate Record Type.
5. Apex calculates the policy premium.
6. A Claim record can be created against the policy.
7. The claim is automatically routed according to policy type.
8. Claims Adjuster reviews the assigned claim.
9. High-value claims go through the approval process.
10. Approvers approve or reject the claim with comments.
11. Claim information is displayed through the LWC dashboard and Salesforce reports.

---

## 👥 User Roles

### Insurance Agent

* Create and manage policies
* Perform guided quoting
* Capture customer and policy information

### Claims Adjuster

* View assigned claims
* Review claim information
* Manage claim workload through the dashboard

### Claims Manager

* Manage claims
* Review high-value claims
* Handle approvals and reporting

---

## ✅ Advantages

* Centralized insurance management
* Automated policy quoting
* Automated premium calculation
* Automated claim routing
* Faster claim processing
* Improved claims visibility
* Better data accuracy
* Flexible insurance data model
* Role-based security
* Scalable Salesforce architecture

---

## 🚀 Future Scope

The project can be extended with:

* External vehicle and property database integration
* Additional insurance products
* Advanced claims automation
* Enhanced analytics and dashboards
* Customer-facing policy and claim tracking
* Mobile accessibility
* AI-based assistance
* API-based integrations with external insurance systems

---

## 📊 Project Outcome

The system provides a centralized Salesforce platform for managing multiple insurance lines and automating important policy and claims processes. It combines **Flows, Apex, LWC, Record Types, Field Sets, Validation Rules, Approval Processes, Permission Sets, and Sharing Rules** to improve policy processing, claim handling, security, and operational visibility.

---

## 📄 Project Documentation

The complete project documentation contains the requirements, architecture, development milestones, Salesforce configuration steps, Apex implementation, LWC development, security configuration, testing, advantages, limitations, and future scope.

---

## 👩‍💻 Project

**Project:** Multi-Line Insurance Policy and Claims Management System
**Platform:** Salesforce CRM
**Domain:** Insurance
**Architecture:** Salesforce Layered Architecture
**Methodology:** Agile / Sprint-Based Development
public class ClaimsAdjusterControllerTest {
@isTest
private class ClaimsAdjusterControllerTest {
    @testSetup
    static void setupTestData() {
        // Create a real active test user
        Profile p = [SELECT Id FROM Profile WHERE Name = 'Standard User' LIMIT 1];
        User u = new User(
            FirstName = 'Test',
            LastName = 'User',
            Alias = 'tuser',
            Username = 'testuser1234343@example.com.test',
            Email = 'testuser123@example.com',
            TimeZoneSidKey = 'America/Los_Angeles',
            LocaleSidKey = 'en_US',
            EmailEncodingKey = 'UTF-8',
            LanguageLocaleKey = 'en_US',
            ProfileId = p.Id
        );
        insert u;

        // Query Policy__c RecordType
        Id policyRT = Schema.SObjectType.Policy__c.getRecordTypeInfosByDeveloperName()
            .get('Auto')
            .getRecordTypeId();
        Id claimRT = Schema.SObjectType.Claim__c.getRecordTypeInfosByDeveloperName()
            .get('Accident') 
            .getRecordTypeId();

        // Create Contact owned by same user
        Contact con = new Contact(
            FirstName = 'John',
            LastName = 'Doe',
            OwnerId = u.Id
        );
        insert con;

        // Create Policy owned by same user
        Policy__c policy = new Policy__c(
            Customer__c = con.Id,
            RecordTypeId = policyRT,
            OwnerId = u.Id,
            VIN__c = '1A903284375893532'
        );
        insert policy;

        // Create Claim owned by same user
        Claim__c claim = new Claim__c(
            Policy__c = policy.Id,
            RecordTypeId = claimRT,
            Claim_Amount__c = 5000,
            Date_of_Loss__c = Date.today().addDays(-10),
            OwnerId = u.Id
        );
        insert claim;
        System.debug('Claim inserted: '+claim.Id);
    }
    @isTest
    static void testGetAssignedClaims() {
        User u = [SELECT Id FROM User WHERE Alias = 'tuser' LIMIT 1];
        System.runAs(u) {
            Test.startTest();
            List<ClaimsAdjusterController.ClaimWrapper> results =
                ClaimsAdjusterController.getAssignedClaims();
            System.debug('Result is: '+results);
            Test.stopTest();
            //System.assert(results.size() > 0,
                //'Expected at least one wrapper returned');

            ClaimsAdjusterController.ClaimWrapper wrap = results[0];

            System.assertNotEquals(null, wrap.claimId);
            System.assertNotEquals(null, wrap.claimNumber);
            System.assertEquals('New', wrap.status);
            System.assertEquals(5000, wrap.claimAmount);
            System.assert(wrap.policyHolderName.contains('John'));
            System.assertNotEquals('Unknown', wrap.policyType);
        }
    }
}

}

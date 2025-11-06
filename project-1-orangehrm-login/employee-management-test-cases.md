# OrangeHRM Employee Management - Test Cases

## Test Environment
- **Application URL:** https://opensource-demo.orangehrmlive.com/
- **Browser:** Chrome 142.0.7444.61
- **Operating System:** Windows 11
- **Test Date:** 6/11/2025
- **Test Type:** Manual Functional Testing with 2-value BVA

## Test Objectives
- Verify Employee creation functionality
- Validate field-level boundaries and constraints
- Test form validation and error handling

## Test Execution Summary
- **Total Test Cases:** 13
- **Passed:** 12
- **Failed:** 1
- **Success Rate:** 92%
- **Defects Found:** 1

## Prerequisites

- Navigate to the Application URL: https://opensource-demo.orangehrmlive.com/
- Log in to the app using the following credentials: Admin / admin123
- Navigate to PIM -> Add Employee: https://opensource-demo.orangehrmlive.com/web/index.php/pim/addEmployee

## Detailed Test Cases

### Name Fields (1-30 character limit)

| ID | Scenario | Test Steps | Test Data | Expected Result | Status | BVA Point |
|----|----------|-------------|-----------|----------------|--------|-----------|
| TC-EM-01 | First Name - Min | 1. Add Employee<br>2. Enter 1 char First Name<br>3. Save | First: "A"<br>Last: "User" | Employee created | Pass | Min |
| TC-EM-02 | First Name - Max | 1. Add Employee<br>2. Enter 30 char First Name<br>3. Save | First: "A"×30<br>Last: "User" | Employee created | Pass | Max |
| TC-EM-03 | First Name - Max+1 | 1. Add Employee<br>2. Enter 31 char First Name<br>3. Save | First: "A"×31<br>Last: "User" | Validation error | Pass | Max+1 |

### Employee ID Field (0-10 character limit)

| ID | Scenario | Test Steps | Test Data | Expected Result | Status | BVA Point |
|----|----------|-------------|-----------|----------------|--------|-----------|
| TC-EM-04 | Employee ID - Min | 1. Add Employee<br>2. Leave ID empty (0 chars)<br>3. Save | First: "John"<br>Last: "Doe"<br>ID: "" | Employee created | Pass | Min |
| TC-EM-05 | Employee ID - Max | 1. Add Employee<br>2. Enter 10 char ID<br>3. Save | ID: "A"×10 | Employee created | Pass | Max |
| TC-EM-06 | Employee ID - Max+1 | 1. Add Employee<br>2. Enter 11 char ID<br>3. Save | ID: "A"×11 | Validation error | Pass | Max+1 |
| TC-EM-07 | Employee ID - Duplicate Min | 1. Create Employee 1 with empty ID<br>2. Create Employee 2 with empty ID | Both: Empty Employee ID | Second should be rejected | **Fail** | Min |

### Username Field (5-40 character limit)

| ID | Scenario | Test Steps | Test Data | Expected Result | Status | BVA Point |
|----|----------|-------------|-----------|----------------|--------|-----------|
| TC-EM-08 | Username - Min | 1. Toggle Login ON<br>2. Enter 5 char username<br>3. Save | Username: "test1" | Employee created | Pass | Min |
| TC-EM-09 | Username - Max | 1. Toggle Login ON<br>2. Enter 40 char username<br>3. Save | Username: "a"×40 | Employee created | Pass | Max |
| TC-EM-10 | Username - Max+1 | 1. Toggle Login ON<br>2. Enter 41 char username<br>3. Save | Username: "a"×41 | Validation error | Pass | Max+1 |

### Password Field (7-64 characters with 1 digit)

| ID | Scenario | Test Steps | Test Data | Expected Result | Status | BVA Point |
|----|----------|-------------|-----------|----------------|--------|-----------|
| TC-EM-11 | Password - Min | 1. Toggle Login ON<br>2. Enter 7 char + digit<br>3. Save | Password: "abcde1f" | Employee created | Pass | Min |
| TC-EM-12 | Password - Max | 1. Toggle Login ON<br>2. Enter 64 char + digit<br>3. Save | Password: "a"×63 + "1" | Employee created | Pass | Max |
| TC-EM-13 | Password - Max+1 | 1. Toggle Login ON<br>2. Enter 65 char + digit<br>3. Save | Password: "a"×64 + "1" | Validation error | Pass | Max+1 |

## Key Findings
- **Data Integrity Issue:** Employee ID allows duplicate empty values

## Defect Identified
- **[TC-EM-07:](../bug-reports/employee-id-duplicate-validation.md)** Employee ID field inconsistently validates duplicate empty values at Min boundary
- **Impact:** Data integrity compromise allowing multiple null identifiers

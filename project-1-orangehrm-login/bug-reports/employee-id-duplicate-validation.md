# Defect: Inconsistent Duplicate Validation in Employee ID Field

**Defect ID:** BUG-EM-001  
**Priority:** Medium  
**Severity:** Medium  
**Status:** Open  
**Environment:** Windows 11, Chrome 142.0.7444.61  
**Module:** PIM → Add Employee  
**Defect Type:** Functional  
**Reporter:** Bart  
**Date Reported:** 6/11/2025

## Description
The Employee ID field exhibits inconsistent duplicate validation behavior. While it correctly prevents duplicate non-empty Employee IDs, it fails to validate duplicate empty/null Employee IDs, allowing multiple employees to have identical null identifiers.

## Impact
- **Data Integrity:** Multiple employees can have null Employee IDs, violating database normalization principles
- **System Reliability:** Potential issues with reporting, search, and data retrieval functions
- **User Confusion:** Inconsistent behavior within the same field may confuse users
- **Future System Upgrades:** May cause issues during data migration or integration

## Steps to Reproduce
1. Navigate to the **[application URL:](https://opensource-demo.orangehrmlive.com/web/index.php/auth/login)**
2. Login to the app using:
    - **Username: Admin**
    - **Password: admin123**
3. Navigate to **PIM → [Add Employee:](https://opensource-demo.orangehrmlive.com/web/index.php/pim/addEmployee)** 
4. Create first employee with empty Employee ID:
   - First Name: `John`
   - Last Name: `Doe`
   - Employee ID: *leave empty*
   - Click **Save** (observe successful creation)
5. Create second employee with empty Employee ID:
   - First Name: `Jane`
   - Last Name: `Smith`
   - Employee ID: *leave empty*
   - Click **Save** (observe successful creation)
6. Verify both employees exist with null Employee IDs in the system

## Expected Result
System should consistently validate Employee ID duplicates by either:
- Requiring Employee ID field (preferred solution), OR
- Auto-generating unique Employee IDs, OR
- Treating empty as a unique value and allowing only one null Employee ID

## Actual Result
Both employees are successfully created with null Employee IDs, creating duplicate "empty" records in the system.

## Test Case Reference
- **Related Test Case:** [TC-EM-07](../../employee-management-test-cases.md#employee-id-field-0-10-character-limit) (Employee ID - Duplicate Min)
- **Test Data:** Empty Employee ID for multiple employees
- **Expected:** Second creation should be rejected
- **Actual:** Both creations successful

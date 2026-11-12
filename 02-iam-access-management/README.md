# AWS IAM User Groups & Access Management

## Project Overview

This project demonstrates how to manage user permissions in Amazon Web Services (AWS) using Identity and Access Management (IAM).

The objective was to create an IAM user group with read-only access to Amazon EC2 resources, assign a test user to the group, and verify that the user could perform authorized actions while being restricted from unauthorized operations.

This project focuses on understanding group-based access control and the principle of least privilege.

## AWS Services and Tools Used

- **AWS IAM** — Managing users, groups, and access permissions.
- **IAM Policies** — Defining permissions for AWS resources.
- **IAM Policy Simulator** — Testing whether specific actions are allowed or denied.
- **Amazon EC2** — The service used to evaluate read-only permissions.

## Configuration

### 1. IAM User Group

Created an IAM user group named `EC2-Viewers`.

Attached the AWS-managed `AmazonEC2ReadOnlyAccess` policy to the group, granting permissions to view EC2 resources without allowing instance modification or termination.

### 2. IAM Test User

Created an IAM user named `ec2-viewer-test` and added the user to the `EC2-Viewers` group.

The user inherited the group's permissions without requiring the policy to be attached directly to the individual user.

Console access was disabled, and no access keys were created for the test user.

### 3. Permission Testing

Used the IAM Policy Simulator to evaluate the permissions assigned to `ec2-viewer-test`.

Two EC2 actions were tested:

| Action | Expected Result | Actual Result |
|---|---|---|
| `ec2:DescribeInstances` | Allowed | Allowed |
| `ec2:TerminateInstances` | Denied | Implicitly Denied |

**Allowed Action:** The `DescribeInstances` operation was explicitly allowed by the attached read-only policy.

**Denied Action:** The `TerminateInstances` operation was implicitly denied because no applicable policy statement granted permission to terminate EC2 instances.

These results confirmed that the tested permissions behaved as intended.

## Architecture Diagram

The following diagram illustrates the relationship between the IAM user, group, attached policy, and permission simulation results.

![IAM Architecture Diagram](IAM%20architecture%20diagram.png)

## Screenshots

### 1. IAM User Group

Created the `EC2-Viewers` group and attached the `AmazonEC2ReadOnlyAccess` policy.

![IAM User Group](screenshots/EC2%20viewers%20group.png)

### 2. IAM Test User

The `ec2-viewer-test` user inherits permissions through membership in the `EC2-Viewers` group.

![IAM Test User](screenshots/Test%20user.png)

### 3. Allowed Action

The IAM Policy Simulator confirms that `ec2:DescribeInstances` is allowed.

![Allowed Action](screenshots/Allowed-action.png)

### 4. Denied Action

The IAM Policy Simulator confirms that `ec2:TerminateInstances` is implicitly denied.

![Denied Action](screenshots/Denied-action.png)

## What I Learned

Through this project, I gained practical experience managing AWS identities and permissions.

Key takeaways include:

- Understanding how IAM user groups simplify permission management.
- Learning how users inherit permissions from policies attached to their groups.
- Applying the principle of least privilege by granting only the permissions required for a specific purpose.
- Understanding the difference between explicitly allowed and implicitly denied actions.
- Using the IAM Policy Simulator to verify permissions without performing potentially destructive operations.

This project strengthened my understanding of AWS access management and how IAM policies help control interactions with cloud resources.

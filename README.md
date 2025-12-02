# Create a Custom IAM Role in Google Cloud

This repository contains my hands-on lab for creating and assigning a **custom IAM role** in Google Cloud and then verifying access using **Policy Analyzer**.

## Objective

- Create a custom IAM role that gives read-only access to Firebase database resources.
- Assign the custom role to a specific user (student account).
- Use Policy Analyzer to confirm which permissions and roles are applied to the user.

## Lab Environment

- Platform: Google Cloud (Qwiklabs temporary project)
- Service: IAM & Admin
- Tools used:
  - IAM → Roles
  - IAM → Permissions (View by principals)
  - Policy Analyzer

---

## Steps Performed

### 1. View existing IAM roles

1. Open the **Google Cloud Console**.
2. Go to **IAM & Admin → Roles**.
3. Review the list of predefined roles available in the project.

📸 `screenshots/01-iam-roles-list-project.png`

---

### 2. Create a custom IAM role

1. In **IAM & Admin → Roles**, click **Create role**.
2. Fill in the basic information:
   - **Title:** `Custom Firebase ReadOnly Role`
   - **ID:** `CustomRole`
   - **Role launch stage:** `General Availability`
3. Click **Add permissions** and add:
   - `firebase.clients.list`
   - `firebasedatabase.instances.list`
4. Save the role by clicking **Create**.

📸 `screenshots/02-create-custom-role-firebase-readonly.png`

---

### 3. Understand missing permissions

1. While trying to view some IAM resources, the console showed a **“You need additional access”** page.
2. The message listed missing permissions such as:
   - `resourcemanager.projects.get`
   - `resourcemanager.projects.getIamPolicy`
3. Google Cloud suggested applicable roles like **Role Viewer** that would satisfy these permissions.

📸 `screenshots/03-missing-permissions-role-viewer.png`

---

### 4. Review project IAM bindings

1. Go to **IAM & Admin → IAM**.
2. Under **Permissions for project**, check the list of principals:
   - Service accounts (e.g., Compute Engine default service account)
   - Qwiklabs user service account
   - Student accounts
3. Confirm that:
   - Owners and Viewers are correctly assigned.
   - The **Audit Team Reviewer** or custom role is granted to the target student account.

📸 `screenshots/04-project-iam-bindings-with-custom-role.png`

---

### 5. Explore Policy Analyzer

1. Open **IAM & Admin → Policy Analyzer**.
2. On the main page, review the available templates:
   - Custom query
   - Who can impersonate a service account?
   - Who can change firewall rules in my project?
   - What access does my employee have?

📸 `screenshots/05-policy-analyzer-home.png`

---

### 6. Run a custom query to verify access

1. In Policy Analyzer, choose **Custom query**.
2. Set the query parameters:
   - **Scope:** the Qwiklabs project
   - **Principal:** the student account email
   - Other fields left with default values (no specific roles or permissions filter).
3. Run the query to see which roles the principal has on the project.
4. Confirm that the student account has the expected **Audit Team Reviewer** (or related) role grant.

📸 `screenshots/06-policy-analyzer-query-results-audit-team-reviewer.png`

---

## What I learned

- How to create a **custom IAM role** with only the required permissions.
- How Google Cloud shows **missing permissions** and suggests roles that contain them.
- How to view **IAM bindings** by principal at the project level.
- How to use **Policy Analyzer** to answer questions like “What access does this user have on this resource?”.

---

## How to use this repo

This repository is mainly for documentation and learning purposes.  
You can follow the steps in this README in your own Google Cloud project to practice IAM role creation and policy analysis.

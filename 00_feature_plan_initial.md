# Feature Plan

## a. User Management & Roles
- **Roles:** Admin (full control), Inspector (audit only), Dynamic Business Role (CEO → Managers → Workers).
- **Profiles:** Company/personal details, training status, signature keys.
- **Authentication:** Secure login with 2FA (optional), GDPR-compliant data handling.

## b. Document Management
- **Templates:** Upload/manage Word/Excel with placeholders, version control.
- **Generation:** Auto-fill with user/company data, batch support.
- **Signing:** AES/QES integration, workflows (employee only or employee + supervisor).
- **Storage:** Documents + metadata.
- **Distribution:** Download by employee, supervisor, inspector (assigned), admin.

## c. Certification Packages
- **Definition:** Bundles of training, tests, and/or documents. Modular (can include 1–3 components).
- **Content:** Video, PDF, text, auto-generated documents.
- **Validation:** Quiz/checkbox tests, lock docs until complete.
- **Configs:** Training only, Test only, Documents only, or any mix.
- **Reporting:** Dashboards for admins/supervisors, export to Excel/PDF.

## d. Inspector Tools
- **Audit role only:** Assigned companies.
- **Features:** View Certification Package status, download signed docs, export compliance reports.
- **No workflow participation.**

## e. Admin Tools
- **Manage templates & versions.**
- **Upload company hierarchy (Excel).**
- **Create & assign Certification Packages.**
- **Assign inspectors to companies.**
- **Upload/assign training modules.**
- **Export compliance reports.**
- **Notifications (in-app, email, optional SMS).**

# User Roles

## 1. Admin
- Full system access.
- Responsible for configuration, template management, certification package creation, and system-level monitoring.

## 2. Inspector
- Independent reviewer, not part of training/signing workflows.
- Access limited to assigned companies during audits.

## 3. Dynamic Business Role (company hierarchy users)
- All company employees belong to this role.
- Functionality depends on hierarchy position (worker vs. supervisor).

**Base User (Worker):**
- Completes assigned Certification Packages.
- Signs personal documents.
- Downloads personal documents.

**User Plus (Manager/CEO):**
- All base user rights.
- Sees subordinate statuses (Certification Package progress, documents signed/pending).
- Sends reminders.
- Downloads subordinate documents.

# Admin Workflow

## 1. Manage Templates
- Upload new templates (Word/Excel with placeholders).
- Version control of templates.
- Assign templates to Certification Packages.

## 2. Create Certification Package
- Name, description, validity period (e.g., yearly).
- Add training modules, tests, documents (any combination).
- Configure signing chain (employee only, employee + supervisor).
- Assign to individuals, groups, or entire company.

## 3. Monitor Compliance
- View package completion status (global or per company).
- Check which users have pending trainings, failed tests, or unsigned docs.

## 4. Notifications
- Send reminders to users (manual or automated).
- Configure notification triggers (package assigned, package nearing expiry, document pending signature).

# Document Workflow

1. **Document Generation** → System fills in company/user data, generates draft.
2. **Assignment** → Document linked to a Certification Package or assigned directly.
3. **User Signature** → Employee signs after required training/test (if any).
4. **Supervisor Signatures (if configured)** → Supervisor(s) sign documents in sequence until completion.
5. **Distribution** → Final documents downloadable by:
   - The employee (personal copy).
   - Supervisor (subordinate copies).
   - Inspector (if assigned by Admin).
   - Admin (always).

# Inspector Flow
- **Login** → Inspector enters assigned dashboard.
- **Company Overview** → Sees documents assigned by Admin.

# User Workflow (Dynamic Business Role)
- Assigned Certification Package appears in user dashboard.
- User completes steps in sequence depending on package configuration:
  - Training → Test → Documents.
  - If package includes only documents → sign directly.
  - If package includes only training → complete module → done.
- Once all required components are finished → package marked Completed.

# User Plus Workflow
- Monitor subordinate Certification Package progress.
- Send reminders for pending items.
- Download subordinate documents.
- All base user rights

# 1. Application Menus

## 1.1. Admin
- Dashboard
- Clients (upload/view hierarchy)
- Templates (upload, version, manage)
- Certification Packages (create, assign, manage)
- Inspectors
- Reports (export)
- Notifications Config

## 1.2. Inspector
- Dashboard
- Documents (view/download signed copies)

## 1.3. Dynamic Business Role

**Base User (Worker):**
- Dashboard
- Certification Packages (assigned, in progress, completed)
- My Documents (signed archive)

**Supervisor (Manager/CEO):**
- All base menus
- Company (Top Level/view hierarchy)
- Team Overview (subordinate package progress)
- Reminders (send training/doc reminders)
- Team Documents (view/download subordinate docs)

# Role-to-Menu Matrix

| Menu / Feature | Admin | Inspector | Worker (Base) | Supervisor (Manager/CEO) |
|---|---|---|---|---|
| Dashboard | ✔ | ✔ | ✔ | ✔ |
| Clients | ✔ | ✖ | ✖ | ✖ |
| Templates | ✔ | ✖ | ✖ | ✖ |
| Certification Packages | ✔ (create, assign, manage) | ✖ | ✔ (assigned, complete) | ✔ (own + subordinates) |
| My Documents | ✔ | ✖ | ✔ | ✔ |
| Team Overview | ✖ | ✖ | ✖ | ✔ |
| Reminders | ✖ | ✖ | ✖ | ✔ |
| Team Documents | ✖ | ✖ | ✖ | ✔ |
| Inspectors | ✖ | ✖ | ✖ | ✔ |
| Reports | ✔ | ✖ | ✖ | ✔ (team scope) |
| Notifications Config | ✖ | ✖ | ✖ | ✔ |
| Documents (view/download signed copies) | ✔ | ✔ | ✔ (own only) | ✔ (own + subordinates) |

# Implementation Layers

| Layer | What Needs to Be Built |
|---|---|
| **Landing Page** | - Public landing page (marketing + product info)<br>- App Login entry point<br>- Blog/Knowledge base (articles on safety law, updates)<br>- Contact & support section |
| **Main Application** | - Secure login & onboarding flow<br>- Role-based dashboards (Worker, Supervisor, Inspector, Admin)<br>- Certification Package viewer & progress flow (training → test → documents)<br>- Document list & viewer<br>- Digital signing flow (integration with Romanian providers)<br>- In-app notifications<br>- Offline caching (mobile workers)<br>- Multi-role handling (single app, role-based views)<br><br>**Admin Console (inside app):**<br>- Template management UI (upload, version, assign)<br>- Company hierarchy import (Excel upload → tree parser)<br>- Certification Package builder UI (training + test + docs)<br>- Training management UI (upload/edit content)<br>- Reports & analytics dashboards (completion, document status)<br>- Inspector assignment panel<br>- Notification settings UI |
| **Backend** | - Role-based access control (RBAC) with dynamic hierarchy<br>- User/company profiles<br>- Company hierarchy parser (Excel → tree structure)<br>- Document template storage (object + metadata)<br>- Document generation (fill placeholders with user/company data)<br>- Digital signing integration (AES/QES, store hashes & timestamps)<br>- Document storage (final signed PDFs + metadata)<br>- Certification Package logic (bundle trainings/tests/docs)<br>- Training content storage (video/pdf/text)<br>- Training/test completion logs<br>- Notification service (email, push, optional SMS)<br>- Reporting queries (status by user, company, inspector)<br>- Export endpoints (Excel/PDF for audits) |
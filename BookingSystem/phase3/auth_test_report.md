# Authorization Test Report - Booking System Phase 3

## 🧑‍🦲 Guest (Not Logged In)

### ✅ Can do

| Action | Location | Observation / Matches Spec? |
| :--- | :--- | :--- |
| View public resource list | `/` | Displays booked resources. **MISMATCH / FAILURE**. **Fails Spec 8** (Does not show reserver identity) and **GDPR/PbD** principles. |
| Access login form | `/login` | Access granted. Matches Spec. |
| Register a new user | `/register` | Registration form is accessible and submissions work. Matches Spec (Users can register). |
| **Access Hidden Resource API** | **`/api/resources`** | **CRITICAL FAILURE (IDOR). Gobuster/wfuzz found endpoint. Access Granted (200 OK) to resource names, IDs, and descriptions.** Fails all security requirements (Spec 8, PbD, Authorization). |

### ❌ Cannot do

| Action | Location | Observation / Matches Spec? |
| :--- | :--- | :--- |
| Make a reservation | `/reservation` | Redirects to `/login`. Correctly blocked. |
| Access Admin page (Direct URL) | `../admin/user` | Access Failed / Blocked (403 Forbidden expected). Correctly blocked. |
| POST /api/reservations | API Endpoint | 401 Unauthorized. Correctly blocked. |

## 🧑‍💼 Reserver (Logged In)

### ✅ Can do

| Action | Location | Observation / Matches Spec? |
| :--- | :--- | :--- |
| **Make a reservation** | `/reservation` (Form) | Reservation successfully made and saved. Matches Spec (Reserver can book a resource). |
| **Edit/Delete Own Reservation** | `/reservation/edit/:id` | **Confirmed: Reserver can edit/delete their own reservation.** Matches expected functionality. |
| View own profile/reservations | `/` | Shows own name (e.g., `guest@a.com`) on the booked resources list. Matches Spec. |

### ❌ Cannot do

| Action | Location | Observation / Matches Spec? |
| :--- | :--- | :--- |
| **Horizontal IDOR (Delete/Edit)** | `/reservation/delete/:id` | **Confirmed: Cannot delete or edit another user's reservation.** **CORRECTLY BLOCKED.** Matches security requirement. |
| Vertical Access Control | `../admin/user` | Access Failed / Blocked (403 Forbidden expected). Correctly blocked. |
| Escalate Privileges (Tampering) | Hidden Form Fields | **[TEST RESULT PENDING: Critical test required with BurpSuite.]** |
| Delete a Reserver | `/api/admin/users/:id` | **[TEST RESULT PENDING: Test required.]** |

## 🧑‍💼🛡️ Administrator (Logged In)

### ✅ Can do

| Action | Location | Observation / Matches Spec? |
| :--- | :--- | :--- |
| **Add/Modify/Delete Resources** | `/admin/resources/*` | **CONFIRMED: Admin can perform all resource management.** Matches Spec (Admin can add, remove, and modify resources). |
| **Delete a Reserver** | `/admin/users/delete/:id` | **CONFIRMED: Admin can delete a Reserver.** Matches Spec (Admin can delete the reserver). |
| Delete a Reservation | `/admin/reservations/delete/:id` | Administrator was able to delete a reservation. Matches Spec (Admin can remove and modify reservations). |
| View Role/Privileges | Homepage | **Displays: "Your role is administrator".** Confirms high privilege status. |

### ❌ Cannot do

| Action | Location | Observation / Matches Spec? |
| :--- | :--- | :--- |
| **CRITICAL SECURITY RISK: SSTI/RCE Injection Points** | `/reservation` (Resource Field) | **CRITICAL FAILURE.** ZAP payloads for **Server-Side Template Injection (SSTI)** and **Remote Code Execution (RCE)** are present in the Resource field. |
| **Public Disclosure of Identity (GDPR Violation)** | `/` (Homepage) | **FAILURE.** The Admin's user role is clearly displayed on the homepage when logged in. Violates general security/PbD principles. |
| **Public Disclosure of Identity (GDPR Violation)** | `/` (Homepage) | **FAILURE.** The Reserver's identity (email) is displayed, violating **Spec 8** and **GDPR / PbD** principles. |
| Access unnecessary logs (PbD) | Discovered Endpoint | **[TEST RESULT PENDING: Need to run Gobuster/wfuzz and test access.]** |

***

### 2️⃣ ZAP Scan Report Link

[**zap\_report\_round4.md**](zap_report_round4.md)

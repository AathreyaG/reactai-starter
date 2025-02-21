### **Title: Submit Applicant Information**###

User Role: As an Applicant, I want to submit my information through the portal so that I can enroll in the assimilation program.

Functional Description:

The system should allow applicants to fill out and submit a form with their personal information. The data should be validated on the frontend and stored securely in the backend database upon submission. This functionality aims to streamline the enrollment process for applicants.

**GIVEN-WHEN-THEN Scenario**:

GIVEN I am on the applicant submission page

WHEN I fill out the form with valid information and click "Submit"

THEN the system should validate the data, send it to the backend, and display a confirmation message

**Acceptance Criteria**:

- The form must include fields for name, email, phone number, and address.
- The system must prevent submission if any required fields are empty.
- Upon successful submission, data should be stored in PostgreSQL.
- A confirmation message must appear after successful submission.
- Validation errors must be displayed for incorrect or incomplete inputs.

Story Points: 5 (Moderate complexity)

**Impact Analysis**:

Backend Implications:

- Create an API endpoint in Node.js (Express) to handle form submissions.
- Implement data validation and storage logic.
- Store applicant data in PostgreSQL (via Sequelize ORM).

Frontend Implications:

- Implement a form UI using React.
- Validate form inputs (required fields, correct format).
- Display success and error messages based on submission status.

**Development Subtasks**:

- Frontend: Build the form component with fields for name, email, phone number, and address.
- Frontend: Implement input validation and error handling.
- Backend: Create Express API to handle form submissions.
- Backend: Implement logic to store data in PostgreSQL.

**Testing Subtasks**:

- Test successful form submission with valid data.
- Test form submission with missing required fields.
- Test form submission with invalid email format.
- Test backend data storage and query performance.
- Perform security tests (data validation, SQL injection protection).

---

### **Title: Real-Time Enrollment Counter**###

User Role: As an Applicant, I want to see a real-time counter of enrollments so that I can know how many people have enrolled.

Functional Description:

The system should display a real-time enrollment counter on the applicant portal. It should update dynamically as new enrollments are processed, providing users with immediate feedback on the current number of enrollments.

**GIVEN-WHEN-THEN Scenario**:

GIVEN I am on the applicant portal page

WHEN the page loads

THEN the system should display the current enrollment count and update it in real-time

**Acceptance Criteria**:

- The counter must display the correct number of enrollments.
- The counter should update dynamically in real-time.
- The system must handle at least 100K concurrent users updating/viewing the counter.

Story Points: 3 (Low complexity)

**Impact Analysis**:

Backend Implications:

- Implement WebSocket or similar technology for real-time updates.
- Create a service to count enrollments in the database.

Frontend Implications:

- Implement a UI component to display the real-time counter.
- Connect the UI component to the WebSocket for live updates.

**Development Subtasks**:

- Frontend: Build the real-time counter component.
- Frontend: Connect the counter to WebSocket for updates.
- Backend: Implement WebSocket service for real-time updates.
- Backend: Create service logic to count enrollments.

**Testing Subtasks**:

- Test initial counter value on page load.
- Test real-time updates as new enrollments are processed.
- Test counter accuracy under high concurrency.
- Perform security tests (WebSocket security, data integrity).

---

### **Title: Automated Scheduling for Assimilation**###

User Role: As an Applicant, I want the system to automatically schedule my assimilation appointment so that I can know when and where to go.

Functional Description:

The system should automatically schedule assimilation appointments across three ports of entry. It should distribute applicants evenly and notify them of their scheduled time and location.

**GIVEN-WHEN-THEN Scenario**:

GIVEN I have successfully submitted my application

WHEN the system processes my application

THEN I should receive a notification with my scheduled assimilation appointment

**Acceptance Criteria**:

- The system must schedule applicants evenly across three ports.
- Each assimilation should be scheduled for 45 minutes.
- Applicants must receive an email notification with their appointment details.
- The system should handle rescheduling if an appointment slot is full.

Story Points: 8 (High complexity)

**Impact Analysis**:

Backend Implications:

- Develop scheduling logic to distribute applicants across ports.
- Create notification service to send appointment details via email.
- Implement rescheduling logic for full appointment slots.

Frontend Implications:

- Display scheduled appointment details in the applicant portal.
- Provide a UI for viewing and managing appointments.

**Development Subtasks**:

- Backend: Implement scheduling algorithm and logic.
- Backend: Develop email notification service.
- Backend: Implement rescheduling logic.
- Frontend: Build UI component to display appointment details.

**Testing Subtasks**:

- Test scheduling logic for even distribution.
- Test email notifications for accuracy and timeliness.
- Test rescheduling functionality.
- Perform edge case tests (overbooking, cancellations).

---

### **Title: Internal Dashboard for Processing Times and Queues**###

User Role: As an Internal User, I want to view processing times and queues so that I can manage and adjust scheduling.

Functional Description:

The dashboard should provide internal users with insights into processing times and current queues. This will enable efficient management of resources and scheduling adjustments as needed.

**GIVEN-WHEN-THEN Scenario**:

GIVEN I am logged into the internal dashboard

WHEN I navigate to the processing times section

THEN I should see current processing times and queues, with options to adjust scheduling

**Acceptance Criteria**:

- The dashboard must display current processing times and queues.
- Users must be able to adjust scheduling parameters.
- Changes should be reflected in real-time on the dashboard.

Story Points: 5 (Moderate complexity)

**Impact Analysis**:

Backend Implications:

- Develop API endpoints to provide processing time and queue data.
- Implement logic to handle scheduling adjustments.

Frontend Implications:

- Build a dashboard UI to display processing times and queues.
- Provide controls for adjusting scheduling parameters.

**Development Subtasks**:

- Backend: Create API endpoints for dashboard data.
- Backend: Implement logic for scheduling adjustments.
- Frontend: Build dashboard UI with data visualizations.
- Frontend: Implement controls for scheduling adjustments.

**Testing Subtasks**:

- Test accuracy of dashboard data.
- Test real-time updates on scheduling adjustments.
- Test user interface for ease of use and accessibility.
- Perform edge case tests (extreme queue sizes, rapid changes).
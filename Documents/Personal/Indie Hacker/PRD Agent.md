Okay, let's design that workflow. This process heavily involves integrating with the **Meta Embedded Signup** flow, which is the standard, secure way for businesses (your customers) to grant your platform (acting via a BSP) permission to manage their WhatsApp Business Account (WABA).

Here’s a breakdown of the workflow from your customer's perspective, along with the necessary backend actions on your platform:

**Phase 1: User Registration on Your Platform**

1. **Visit Website:** The potential customer lands on your website (e.g., `yourplatform.com`).
2. **Learn About Service:** They browse information about your WhatsApp business solutions (chatbot builder, shared inbox, automation tools, etc.).
3. **Sign Up:** The customer clicks "Sign Up" or "Create Account".
4. **Account Creation:** They provide necessary details (email, password, company name, etc.) and complete your platform's registration process.
5. **Login & Dashboard:** The customer logs into their newly created account on your platform and accesses their dashboard.

**Phase 2: Initiating WhatsApp Business Account Onboarding**

6. **Navigate to WhatsApp Section:** Inside your platform's dashboard, the customer finds a section dedicated to connecting communication channels, specifically "WhatsApp".
7. **Call-to-Action:** They see a clear button like **"Connect WhatsApp Business Account"** or **"Set up WhatsApp Channel"**.
    - _(Optional but Recommended)_: Provide brief info nearby explaining the process: "This will guide you through connecting your Facebook Business account and verifying a phone number to use with WhatsApp via our official integration." List prerequisites:
        - A Facebook account.
        - Admin access to a Meta Business Account (or willingness to create one).
        - A phone number _not_ currently registered with the consumer WhatsApp app or another WABA, which they can verify via SMS or phone call.
8. **Customer Clicks "Connect":** This action triggers the core onboarding flow.

**Phase 3: Embedded Signup Flow (Managed by Meta via BSP)**

9. **Trigger Embedded Signup (Your Backend):**
    - When the customer clicks "Connect", your platform's backend makes an API call to your BSP (or directly to the Meta Graph API if you are a Solution Partner yourself) to initiate the **Embedded Signup** flow.
    - You will typically pass configuration details, including a `state` parameter (a unique, unguessable string) for security (CSRF protection) and potentially pre-filled information if available.
10. **Meta Popup Window Appears:** A secure popup window managed by Meta/Facebook opens. Your platform's main window should show a "waiting" or "in progress" state.
11. **Facebook Login:** The customer is prompted to log into the Facebook account associated with their business.
12. **Permissions Grant (Initial):** The customer grants your Meta Developer App (associated with your BSP integration) initial permissions.
13. **Select/Create Meta Business Account:** The customer chooses an existing Meta Business Account they manage or is guided to create a new one.
14. **Select/Create WABA:** Within the chosen Meta Business Account, they select an existing WABA or create a new one.
15. **Create/Confirm Business Profile:** They enter or confirm the details for their WhatsApp Business Profile (Display Name - subject to review, Category, Description, etc.).
16. **Select & Verify Phone Number:**
    - The customer provides the phone number they want to use for this WABA.
    - They choose a verification method (SMS or Voice Call).
    - They enter the verification code received on that phone number into the Meta popup.
    - _(Error Handling within Meta Flow):_ Meta handles checks like "number already in use on consumer WhatsApp". If verification fails, the customer can retry or try a different number within the Meta flow.
17. **Grant Final Permissions:** The customer explicitly grants your platform (via the BSP/your Meta App) permission to manage this WABA and phone number on their behalf (e.g., `whatsapp_business_management`, `whatsapp_business_messaging`).
18. **Flow Completion & Redirect/Callback:**
    - Upon successful completion, the Meta popup closes or redirects.
    - Meta calls a pre-configured `redirect_uri` or sends a signal back to the initiating window.
    - Crucially, your backend receives a **callback** from Meta/BSP containing an **authorization code** (or similar credential) and the `state` parameter you initially sent.

**Phase 4: Finalizing Connection on Your Platform**

19. **Verify Callback & Exchange Code (Your Backend):**
    - Your backend receives the callback from Meta/BSP.
    - **Crucially, validate the received `state` parameter** against the one stored for that user's session to prevent CSRF attacks.
    - Exchange the received authorization code for necessary access tokens (like a System User Access Token or BSP-specific API keys) required to manage the customer's WABA. Follow your BSP's or Meta's documentation for this step.
20. **Retrieve WABA Details (Your Backend):** Using the obtained token/credentials, make API calls to retrieve essential details like the WABA ID, verified Phone Number ID, and Display Name.
21. **Store Credentials Securely (Your Backend):** Store the necessary identifiers (WABA ID, Phone Number ID, potentially access tokens or BSP identifiers) securely in your database, associating them with the customer's account on your platform. **Never store sensitive tokens insecurely.**
22. **Update UI (Your Frontend):**
    - Once the backend confirms successful onboarding and credential storage, update the customer's dashboard UI.
    - Change the status from "Connect WhatsApp" to "Connected" or similar.
    - Display the connected WhatsApp number and its status (e.g., "Verified", "Display Name Pending Review").
23. **Guide Next Steps:** Provide clear next steps within your platform, such as "Configure your Chatbot", "Import Contacts", "View Conversations", etc.

**Error Handling (Your Platform):**

- If the callback indicates an error (e.g., user cancelled, permission denied, verification failed persistently), update the UI with a clear error message.
- Provide guidance or links to troubleshooting documentation or your support channel.
- Log errors on your backend for debugging.

This workflow leverages Meta's secure Embedded Signup, ensuring compliance and a relatively seamless experience for your customer while giving your platform the necessary permissions via your BSP integration. Remember to consult your specific BSP's documentation for the exact API calls and procedures for initiating Embedded Signup and handling the callbacks.


# PRD: WhatsApp Business Account (WABA) Onboarding via Embedded Signup

**Version:** 1.0
**Date:** 2025-04-16
**Author:** Gemini
**Status:** Draft
**Relevant Location Context:** Medellin, Antioquia, Colombia (Consider local regulations like data privacy under Law 1581 of 2012 if applicable to stored data).

## 1. Introduction

This document outlines the requirements for the WhatsApp Business Account (WABA) Onboarding feature. This feature allows users of our platform to securely connect their new or existing WABA to their platform account using Meta's official Embedded Signup flow, facilitated through our integrated Business Solution Provider (BSP). This enables users to leverage our platform's tools (e.g., chatbot builder, shared inbox) for their WhatsApp business communications.

## 2. Goals

### 2.1. Business Goals

* Increase adoption and utility of the platform by enabling WhatsApp channel integration.
* Provide a secure, compliant, and user-friendly method for WABA onboarding.
* Establish the foundation for offering value-added WhatsApp services (automation, support tools).
* Reduce manual setup effort and potential errors compared to non-integrated methods.
* Potentially create new revenue streams based on WhatsApp feature usage.

### 2.2. User Goals

* Easily connect my WhatsApp Business presence to the platform without complex technical steps.
* Securely grant necessary permissions for the platform to manage my WhatsApp communications.
* Onboard a new WABA if I don't have one already, guided through the process.
* Manage my business's WhatsApp interactions centrally through the platform dashboard.

## 3. User Stories

* **As a new platform user,** I want to connect my existing WhatsApp Business Account after signing up, so I can start managing customer conversations through the platform's interface.
* **As a business owner new to WhatsApp Business,** I want the platform to guide me through creating and verifying a new WhatsApp Business Account and phone number, so I can use WhatsApp as a communication channel via the platform.
* **As a platform user,** I want the connection process to be secure and transparent, so I feel confident granting permissions to manage my business communications.
* **As a platform administrator,** I want a reliable and Meta-compliant onboarding flow, so we can ensure service stability and adherence to WhatsApp policies for our users.

## 4. Requirements

### 4.1. Functional Requirements

| ID    | Requirement Description                                                                                                                               | Details                                                                                                                                                                                                                               | Priority |
| :---- | :---------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------- |
| FR-01 | **User Registration/Login:** Users must be registered and logged into the platform to initiate the WABA onboarding flow.                               | Assumes existing authentication system.                                                                                                                                                                                               | Must Have  |
| FR-02 | **Initiate Onboarding UI:** Provide a clear UI element (e.g., button "Connect WhatsApp Business Account") within the user's dashboard/settings area. | Button should be clearly visible in the relevant section (e.g., "Channels", "Integrations").                                                                                                                                         | Must Have  |
| FR-03 | **Trigger Embedded Signup:** Clicking the UI element initiates the Meta Embedded Signup flow via the integrated BSP.                                    | Platform backend calls the appropriate BSP API endpoint to start Embedded Signup. Must pass a unique, unguessable `state` parameter tied to the user session for CSRF protection. May pass other config/pre-fill data as allowed by BSP/Meta. | Must Have  |
| FR-04 | **Display Meta Popup:** The Meta-controlled Embedded Signup flow must be displayed to the user (typically in a popup window).                           | Platform frontend should handle opening the popup/redirect as directed by the backend/BSP response.                                                                                                                                   | Must Have  |
| FR-05 | **Handle Callback:** Platform backend must receive and process the callback from Meta/BSP upon completion (success or failure) of the Embedded Signup flow. | Requires a dedicated, secure callback endpoint (HTTPS). Must handle various scenarios: success, user cancellation, permissions denied, errors.                                                                                       | Must Have  |
| FR-06 | **Validate State Parameter:** The `state` parameter received in the callback must be validated against the one generated in FR-03 for that user session. | Critical security step to prevent CSRF attacks. If validation fails, abort the process and log a security event.                                                                                                                    | Must Have  |
| FR-07 | **Exchange Authorization Code:** On successful callback validation, exchange the received authorization code for required access tokens/credentials.      | Backend calls the appropriate BSP/Meta API endpoint to perform the code-to-token exchange. Specifics depend on BSP/Meta implementation.                                                                                              | Must Have  |
| FR-08 | **Retrieve WABA Details:** Use the obtained credentials to fetch essential WABA information.                                                            | Backend calls BSP/Meta API to get WABA ID, verified Phone Number ID, Display Name, verification status, etc.                                                                                                                          | Must Have  |
| FR-09 | **Secure Credential Storage:** Securely store the necessary WABA identifiers and potentially access tokens associated with the user's platform account.   | Use industry best practices for storing sensitive data (e.g., encryption at rest, appropriate access controls). Do not store raw tokens insecurely. Follow BSP/Meta guidelines.                                                        | Must Have  |
| FR-10 | **Update Platform UI:** Reflect the outcome of the onboarding flow in the user's platform dashboard.                                                    | **Success:** Show connected status, display number, name, status (e.g., Verified). Provide clear next steps. **Failure:** Show user-friendly error message, suggest retry or support.                                                 | Must Have  |
| FR-11 | **Logging:** Log key events throughout the workflow for monitoring and debugging.                                                                       | Log initiation attempts, Meta popup launch, callback received (success/error), state validation results, credential exchange outcomes, storage success/failure, final UI update state.                                                 | Must Have  |

### 4.2. Non-Functional Requirements

| ID    | Requirement Description | Details                                                                                                                                                                | Priority |
| :---- | :---------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- |
| NFR-01| **Security** | Implement CSRF protection (`state` parameter). Securely store credentials (encryption). Use HTTPS for all communication. Adhere to Meta/BSP security standards.          | Must Have  |
| NFR-02| **Reliability** | Robust error handling for all API calls (Meta/BSP, internal). Graceful degradation if Meta/BSP services are temporarily unavailable. High availability for callback endpoint. | Must Have  |
| NFR-03| **Usability** | Clear instructions and feedback throughout the process. Minimize user effort. Seamless transition between platform UI and Meta popup.                                        | Must Have  |
| NFR-04| **Performance** | Callback processing and credential exchange should be timely to provide prompt UI feedback. API calls should be optimized.                                               | Should Have|
| NFR-05| **Compliance** | Adhere to Meta Platform Terms, WhatsApp Business Platform policies, and BSP agreements. Comply with relevant data privacy regulations (e.g., Colombia's Law 1581 of 2012). | Must Have  |

### 4.3. UI/UX Requirements

* A dedicated section in the user dashboard for managing connected channels, including WhatsApp.
* A clearly labelled button ("Connect WhatsApp Business Account" or similar) to start the flow.
* Informative helper text explaining the process, prerequisites (Facebook account, admin access, valid phone number), and that a Meta popup will appear.
* Visual indicator (e.g., spinner, message) on the platform page while the Meta Embedded Signup popup is active.
* **Success Screen/State:**
    * Clear confirmation message (e.g., "WhatsApp Account Connected Successfully!").
    * Display the connected WhatsApp Display Name and Phone Number.
    * Show the verification status (e.g., "Verified", "Display Name Pending Review").
    * Provide clear calls-to-action for next steps (e.g., "Configure Chatbot", "Go to Inbox").
* **Error Screen/State:**
    * User-friendly error message explaining the issue (e.g., "Connection failed: Permissions denied.", "Verification failed. Please try again or use a different number."). Avoid technical jargon.
    * Option to retry the process.
    * Link to troubleshooting documentation or support contact.

## 5. Design Considerations

* UI mockups are required for the platform screens involved in the workflow (pre-initiation state, waiting state, success state, error state).
* The UI/UX of the Embedded Signup popup itself is controlled by Meta and cannot be customized significantly, but the surrounding platform experience needs careful design.
* Ensure the design is responsive and works well on different screen sizes.

## 6. Open Issues/Questions

* What are the specific API endpoints, request/response formats, and authentication methods for our chosen BSP's Embedded Signup implementation?
* How will specific error codes from Meta/BSP be mapped to user-friendly messages?
* What is the detailed credential storage and rotation strategy?
* Are there specific rate limits from Meta/BSP we need to handle?
* How will users manage/disconnect an already connected WABA? (See Future Considerations)

## 7. Future Considerations

* Support for connecting multiple WABAs to a single platform account.
* Workflow for disconnecting or replacing a connected WABA.
* Displaying more detailed WABA profile information (address, email, website, about text).
* Real-time monitoring and alerting for changes in WABA status (e.g., disconnected by user, banned by WhatsApp, display name approved/rejected).
* Integration with platform billing based on WABA connection/usage.

## 8. Success Metrics

* **Onboarding Completion Rate:** (# Successful WABA connections / # Initiated onboarding flows) * 100%.
* **Average Time to Complete Onboarding:** Measured from clicking "Connect" to seeing the success state.
* **User Activation Rate:** % of users who connect a WABA and subsequently use a core WhatsApp feature (e.g., send/receive message, configure bot) within X days.
* **Support Ticket Reduction:** Decrease in support tickets related to manual WhatsApp setup or connection issues.
* **Error Rate:** Frequency of errors encountered during the onboarding flow (logged internally).


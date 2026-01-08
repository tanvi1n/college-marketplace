# Student Marketplace App: Project Plan

This document outlines the requirements for each phase of the project, structured into vertical slices for efficient teamwork.

---

### Phase 1: Project Setup & Foundation (All Team Members)
*This phase is collaborative to ensure everyone is on the same page.*

**Objective:** Create a stable foundation for the project.
-   [ ] **Task:** All team members set up their Android Studio environment with the correct Kotlin and Jetpack Compose configurations.
-   [ ] **Task:** One team member creates the Firebase project and shares access with the others.
-   [ ] **Task:** Connect the Android app to the Firebase project (add `google-services.json` and required dependencies).
-   [ ] **Task:** Agree on and document coding conventions (naming, formatting).
-   [ ] **Task:** Agree on the core app architecture (MVVM) and set up the basic package structure (e.g., `ui`, `viewmodel`, `data`, `di`).

---

### Phase 2: MVP Implementation (Vertical Slice Assignments)
*Divide these three core features among your team. Each person owns their feature from UI to backend.*

#### Feature Owner 1: User Identity & Profiles
**Objective:** Allow users to create an account and manage their profile.
-   [ ] **Feature: User Authentication**
    -   **UI:** Create Login and Registration screens using Jetpack Compose.
    -   **Logic:** Implement a `UserViewModel` to handle input validation, including the `.edu` email check.
    -   **Backend:** Use Firebase Authentication to handle user creation, sign-in, and sign-out.
-   [ ] **Feature: User Profile Management**
    -   **UI:** Build a "View Profile" screen and an "Edit Profile" screen.
    -   **Logic:** Extend `UserViewModel` to load profile data from Firestore and save updates.
    -   **Backend:** Upon registration, create a `users` collection in Firestore and store user details (name, department, graduation year). Implement read and write functions for this data.

#### Feature Owner 2: Item Listings & Discovery
**Objective:** Allow users to list items and for others to see them.
-   [ ] **Feature: Create and View Listings**
    -   **UI:** Build the "Create New Listing" form, a main feed screen (list view), and a detailed view screen for a single item.
    -   **Logic:** Implement a `ListingsViewModel` to manage form state, handle image selection from the device, and fetch listings for the feed.
    -   **Backend:** Create a `listings` collection in Firestore. When a user creates a listing, upload images to Firebase Storage and store the image URLs along with other item details in a new Firestore document.

#### Feature Owner 3: Communication & Listing Management
**Objective:** Enable user communication and allow sellers to manage what they've posted.
-   [ ] **Feature: In-App Chat**
    -   **UI:** Design a "Conversations" screen listing all chats and a real-time messaging screen for individual chats.
    -   **Logic:** Implement a `ChatViewModel` to send and receive messages in real-time.
    -   **Backend:** Set up Firestore or Realtime Database to structure and handle live chat messages between users. When a buyer starts a chat, create a new chat channel/document linked to the two users and the item.
-   [ ] **Feature: Seller's Listing Management**
    -   **UI:** Create a "My Listings" screen. Add "Mark as Sold" and "Delete" buttons to the item detail view (visible only to the owner).
    -   **Logic:** Extend `ListingsViewModel` to handle deleting or changing the status of a listing.
    -   **Backend:** Implement functions to update a listing's status field (e.g., from `active` to `sold`) or delete the document from the `listings` collection in Firestore.

---

### Phase 3: Advanced Features (Continue Vertical Ownership)
*Assign these features, ideally to the owner whose MVP work is most related.*

#### Feature Owner 1: Trust & Safety
**Objective:** Build mechanisms to ensure a trustworthy community.
-   [ ] **Feature: Ratings and Reviews**
    -   **UI:** Design a dialog or screen for users to submit a rating (1-5 stars) and a text review after a transaction is marked "Sold". Display the average rating on User Profiles.
    -   **Logic:** `UserViewModel` handles submitting the review data.
    -   **Backend:** When a listing is marked "Sold", trigger a state that allows buyer and seller to review each other. Store reviews in a `reviews` sub-collection within the reviewed user's document in Firestore.

#### Feature Owner 2: Advanced Discovery
**Objective:** Make it easier for users to find what they need.
-   [ ] **Feature: Search and Filtering**
    -   **UI:** Add a search bar to the main feed. Create a UI for applying filters (e.g., category, price range).
    -   **Logic:** `ListingsViewModel` now takes search/filter parameters and updates the feed accordingly.
    -   **Backend:** Write and optimize Firestore queries to support keyword search and filtering on multiple fields.

#### Feature Owner 3: User Engagement
**Objective:** Keep users informed and coming back to the a-pp.
-   [ ] **Feature: Push Notifications**
    -   **UI:** (System-level) Configure how notifications appear on the device.
    -   **Logic:** Integrate the Firebase Cloud Messaging (FCM) SDK to receive and handle notifications.
    -   **Backend:** Implement Cloud Functions for Firebase. The first trigger should be: when a new message is added to a chat, send a push notification to the recipient.

---

### Phase 4 & 5: Testing, Launch & Maintenance (All Team Members)
*This is a final collaborative push to ensure quality and a successful launch.*

-   [ ] **Task: Code Review & Polishing**
    -   Each member reviews the code for the features they *didn't* build to catch bugs and suggest improvements.
    -   Everyone polishes the UI/UX for their owned features.
-   [ ] **Task: Testing**
    -   Each member writes unit tests for the ViewModels of their assigned features.
    -   Collaboratively write and run through a manual testing plan that covers all features and addresses the risks in `challenges_risks.md`.
-   [ ] **Task: Launch Preparation**
    -   Divide the tasks for creating Play Store assets: one person on screenshots, another on the app icon, another on writing the description.
-   [ ] **Task: Deployment & Monitoring**
    -   Walk through the release process together.
    -   Set up dashboards in Firebase (Crashlytics, Analytics) to monitor the app's health post-launch.

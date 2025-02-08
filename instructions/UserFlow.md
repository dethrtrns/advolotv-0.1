# User Journey Flow Summary

## Detailed Flow Summary

### Entry Points & Landing Pages
- **Base URL:** Users land on the **UserLandingPage** (client-focused) that includes:
  - **Hero Section:** Engaging introduction.
  - **Location Selector:** Choose the region.
  - **Issue Categories Cards:** Display common legal concerns.
  - **Specialization Cards:** Highlight various legal specialties.
  - **Featured Lawyers Section:** Showcases selected lawyers.
  - **"Help me Find the Right Lawyer" Button:** Initiates the matching wizard.
  - **Navigation Options:** Buttons for "I'm a Lawyer" or "Join as Lawyer" for legal professionals.

### Lawyer-Side Flow (via "I'm a Lawyer" Button)
- **LawyerLandingPage:**
  - Register/Login options with marketing/info content tailored for lawyers.
- **Post-Authentication:**
  - Redirect to a protected **LawyerDashboard** which includes:
    - Profile Management.
    - Booking Management.
    - Communication Tools (for interacting with clients).

### Client-Side Main Flow

#### A. Discovery Phase (No Authentication Required)
- **LawyerList Page:**
  - **Search Bar:** Keyword-based search.
  - **Filter Options:** Narrow results by criteria (location, specialization, etc.).
  - **Sort Options:** Order results by ratings, experience, etc.
  - **Lawyer Cards:** Display limited basic info (professional overview, specializations, and experience) with critical details hidden for non-authenticated users.
  - **"Help me Find" Modal/Form:** A step-by-step method to refine search conditions.

#### B. Interaction Phase
- **LawyerDetails Page:**
  - Provides comprehensive profile information.
  - Displays a **"Sign-in to view/consult" Button** to reveal full details.
  - Post-sign-in, clients can access Booking/Scheduling options.

### Auxiliary Features
- **"Help me Find the Right Lawyer" Wizard:**  
  - A linear step-by-step guide where users define their issues, assess needs, and get matched automatically.
- **Enquiry Modal:**  
  - Available during discovery to refine search queries or request additional assistance.

### Authentication Points
- **Optional until Critical Actions:**  
  - Viewing full lawyer details.
  - Booking consultations.
  - Accessing communication features.

---

## Extended Flow: Post-Sign-In & Post-Booking (Clients)
- **Post-Sign-In (Clients):**
  - Full access to lawyer profiles (reviews, detailed specializations).
  - **Booking/Schedule Process:**
    - Select an available appointment slot through a calendar view.
    - Proceed to Payment (handled via a secure gateway like Stripe).
    - Receive a Confirmation with appointment details (email and in-app notification).
- **Post-Booking Actions:**
  - Automated notifications (email and push).
  - In-app Chat and Document Sharing to facilitate ongoing communication.

## Extended Flow: Post-Sign-In (Lawyers)
- **Dashboard Access:**
  - Manage profile details, adjust availability, and view incoming appointment requests.
  - Use integrated communication tools to interact with clients.
  - Manage case documents and update scheduling.

---

## Simple Arrow Diagram of the User Flow:

Base URL
    |
    v
UserLandingPage
    |
    +----------------> [I'm a Lawyer] -----> LawyerLanding -----> Register/Login -----> LawyerDashboard
    |                                                                                        |
    |                                                                                        v
    +---> LawyerList <---------------------[Help Me Find]------------------------> Communication
    |      (Cards)    \                                                                      ^
    |         |        \                                                                     |
    |         v         \                                                                    |
    |    LawyerDetails   \                                                                  |
    |         |           \                                                                 |
    |         v            \                                                                |
    +---> [Sign In] --------+-> Booking/Schedule -------> Payment -------> Confirmation ----+
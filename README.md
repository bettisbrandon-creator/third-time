# Form & Workflow Builder

This project is a comprehensive, React-based application for creating dynamic forms, designing approval workflows, and managing submissions. It uses Firebase for backend services and Tailwind CSS for styling.



## ✨ Features

* **Drag-and-Drop Form Builder**: Easily create complex forms with various field types.
* **Visual Workflow Designer**: Design multi-step approval processes with conditional logic.
* **Dynamic Previews**: Instantly preview forms on both desktop and mobile layouts.
* **Submission Management**: View, filter, sort, and export form submissions.
* **Role-Based Access Control**: Simulate Admin, Designer, and Viewer roles.
* **Task Management**: Users can view and act on submissions assigned to them.
* **Dashboard Analytics**: Visualize submission data with charts and graphs.

---

## 🚀 Getting Started

Follow these instructions to get a copy of the project up and running on your local machine.

### Prerequisites

* [Node.js](https://nodejs.org/) (v18.x or later recommended)
* [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
* A [Firebase](https://firebase.google.com/) project with Firestore enabled.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    # or
    yarn install
    ```

3.  **Set up Firebase Configuration:**
    * Create a new file named `.env.local` in the root of your project.
    * Go to your Firebase project settings and find your web app's configuration object.
    * Add your Firebase credentials to the `.env.local` file. **All variables must start with `REACT_APP_`**.

    ```env
    # .env.local

    REACT_APP_FIREBASE_API_KEY="your-api-key"
    REACT_APP_FIREBASE_AUTH_DOMAIN="your-auth-domain"
    REACT_APP_FIREBASE_PROJECT_ID="your-project-id"
    REACT_APP_FIREBASE_STORAGE_BUCKET="your-storage-bucket"
    REACT_APP_FIREBASE_MESSAGING_SENDER_ID="your-messaging-sender-id"
    REACT_APP_FIREBASE_APP_ID="your-app-id"
    ```

4.  **Update the Firebase Initialization Code:**
    * The provided code was designed to work with globally injected variables (like `__firebase_config`). You'll need to modify the main `App.js` component to use the environment variables you just set up.

    * Find this `useEffect` block in `App.js`:
      ```javascript
      useEffect(() => {
        try {
            const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
            // ...
      ```
    * Replace it with this code to read from your `.env.local` file:
      ```javascript
      useEffect(() => {
        try {
          const firebaseConfig = {
            apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
            authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
            projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
            storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
            messagingSenderId: process.env.REACT_APP_FIREBASE_MESSAGING_SENDER_ID,
            appId: process.env.REACT_APP_FIREBASE_APP_ID
          };

          if (!firebaseConfig.apiKey) {
            console.warn("Firebase config is missing from .env.local. App will not connect to Firebase.");
            return;
          }

          const app = initializeApp(firebaseConfig);
          // ... rest of the function
      ```

5.  **Run the application:**
    ```bash
    npm start
    ```
    This will open the app in your browser at `http://localhost:3000`.

---
## 建议的项目结构

For better maintainability, consider organizing your code into folders. The current implementation has all components in one file. A more scalable structure would be:

```
src/
├── components/         # Reusable UI components
│   ├── builder/        # Form builder specific components
│   ├── common/         # Generic components (Icon, StatusBadge)
│   ├── views/          # Top-level views (DashboardView, LibraryView, etc.)
│   └── App.js          # Main application component
├── config/             # Configuration files (Firebase, constants)
├── hooks/              # Custom React hooks
└── index.js            # Entry point
```

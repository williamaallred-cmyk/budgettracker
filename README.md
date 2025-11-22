# Budget Tracker

A simple, shared budget tracking application for couples. Track expenses across multiple categories with real-time updates using Firebase.

## Features

- 💸 Quick expense logging across 7 categories
- 🎯 Monthly budget goals for each category
- 📊 Real-time spending tracking
- 👥 Shared database for multiple users
- 📱 Responsive design for mobile and desktop

## Setup Instructions

### 1. Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project (or use an existing one)
3. Enable **Authentication** → **Sign-in method** → Enable **Anonymous**
4. Create a **Firestore Database** (start in production mode)
5. Set up Firestore security rules (see below)
6. Go to **Project Settings** → **General** → **Your apps** → **Web app**
7. Copy your Firebase configuration

### 2. Configure Your App

Create a file named `firebase-config.js` in this directory with your Firebase credentials:

\`\`\`javascript
// firebase-config.js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};
\`\`\`

**Important:** Never commit `firebase-config.js` to Git. It's already in `.gitignore`.

### 3. Firestore Security Rules

In Firebase Console → Firestore Database → Rules, use these rules to allow both you and your wife to access the shared data:

\`\`\`
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow authenticated users to read/write their own data
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
\`\`\`

### 4. Running the App

Simply open `index.html` in your web browser. Both you and your wife can access it from the same URL and share the same database by using the same user ID.

## Categories

- 🛍️ Shopping
- ⛽ Gas
- 🍕 Dining Out
- ⚽ Activities
- 🏥 Medical
- 🐾 Pets
- 🛒 Groceries

## Usage

1. **Set Monthly Budgets**: Click "Set Monthly Budgets" to configure spending goals
2. **Log Expenses**: Tap a category and enter the amount
3. **Track Progress**: View remaining budget for each category and recent transactions

## Tech Stack

- HTML5
- Tailwind CSS
- Firebase (Firestore & Authentication)
- Vanilla JavaScript

## License

MIT

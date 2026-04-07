# A2A Logistics — Firebase Setup Guide
## Replace YOUR_API_KEY placeholders in both index.html and admin.html

### Step 1: Create Firebase Project
1. Go to https://console.firebase.google.com
2. Click "Add project" → name it e.g. "a2a-logistics"
3. Enable Google Analytics if desired

### Step 2: Enable Firestore
1. In Firebase console → Firestore Database
2. Click "Create database"
3. Choose "Start in test mode" (for development)
4. Select a region (e.g. australia-southeast1)

### Step 3: Get your Firebase Config
1. In Firebase console → Project Settings (gear icon)
2. Scroll to "Your apps" → Click </> (Web)
3. Register your app name → Copy the firebaseConfig object

### Step 4: Replace placeholders in both files
In index.html AND admin.html, replace:

```javascript
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",           ← replace
  authDomain:        "YOUR_PROJECT_ID.firebaseapp.com",  ← replace
  projectId:         "YOUR_PROJECT_ID",        ← replace
  storageBucket:     "YOUR_PROJECT_ID.appspot.com",  ← replace
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",  ← replace
  appId:             "YOUR_APP_ID"             ← replace
};
```

With your actual values from Firebase, e.g.:
```javascript
const firebaseConfig = {
  apiKey:            "AIzaSyAbc123...",
  authDomain:        "a2a-logistics.firebaseapp.com",
  projectId:         "a2a-logistics",
  storageBucket:     "a2a-logistics.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc123"
};
```

### Step 5: Deploy to Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Set public directory to: . (current folder)
# Configure as SPA: No
firebase deploy
```

### Step 6: Connect Custom Domain
1. Firebase console → Hosting → Add custom domain
2. Enter: a2alogistics.com.au
3. Follow DNS verification steps (add TXT record)
4. Add A records and CNAME for www

### Firestore Security Rules (for production)
Replace test mode rules with:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /leads/{leadId} {
      allow create: if true;  // Allow form submissions
      allow read, update, delete: if false;  // Protect from public reads
    }
  }
}
```

### Files in this package:
- index.html    → Main website
- admin.html    → Admin panel (view all leads)
- sitemap.xml   → For Google Search Console
- robots.txt    → SEO crawler instructions
- FIREBASE_SETUP.md → This file

### WhatsApp Number
All "Contact via WhatsApp" links go to: https://wa.me/61431986606
To change: search "61431986606" in index.html and replace.

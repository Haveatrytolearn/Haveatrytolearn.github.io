# Firebase setup for the contact form

## Step 1 — Create a Firebase project
1. Go to https://console.firebase.google.com/
2. Click "Add project" (or "Create project").
3. Give the project a name, for example `maria-portfolio`.
4. Skip Google Analytics for this tutorial (optional).
5. Finish creating the project.

## Step 2 — Enable Firestore Database
1. In the left-hand menu open **Firestore Database**.
2. Click **Create database**.
3. Choose a region (for example, Europe — `europe-west1`).
4. Start in **test mode** for development (remember to tighten rules before production).
5. Create the database.

## Step 3 — Get your Firebase config
1. Click the gear icon (Project settings) in the Firebase Console.
2. Scroll to the **Your apps** section and add a web app (`</>`).
3. Give the app a name (for example, `Portfolio`).
4. Firebase will show a configuration object (`firebaseConfig`) — copy it.

## Step 4 — Enable Authentication (optional but recommended)
1. In the left menu open **Authentication** → **Get started**.
2. Enable **Anonymous** sign-in (or another provider you prefer).

## Step 5 — Security rules
1. In **Firestore Database** open the **Rules** tab.
2. For quick testing you can use permissive rules, but restrict them for production. Example (open during development only):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /feedback/{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Publish the rules. (Important: update these rules before deploying publicly.)

## Step 6 — Add the config to your site
1. Open `index.html` in this repository.
2. Replace the placeholder `firebaseConfig` values with the values you copied from the Firebase Console.

## Step 7 — Test the form
1. Open your site locally or deployed (GitHub Pages or other).
2. Fill out the contact form and click Submit.
3. Open the Firebase Console → Firestore Database and check the `feedback` collection — submissions should appear there.

## (Optional) Step 8 — Email notifications
If you want email notifications for new submissions, add a Cloud Function (or third-party integration) to send emails when documents are created in the `feedback` collection.



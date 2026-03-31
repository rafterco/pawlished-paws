# Pawlished Paws Website — Setup Guide

## Files in this project

| File | Purpose |
|------|---------|
| `index.html` | Homepage |
| `services.html` | Services & Pricing page |
| `booking.html` | Booking form (Firebase-connected) |
| `admin.html` | Private admin dashboard |
| `contact.html` | Contact page with map |
| `css/style.css` | All styling |
| `images/logo.png` | **Replace this with your actual logo file** |

---

## Step 1 — Add Your Logo

Replace `images/logo.png` with your actual logo image file (keep the filename as `logo.png`).

---

## Step 2 — Connect Firebase

### Create your Firebase project:
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → name it "pawlished-paws"
3. Click the **Web** icon (`</>`) to add a web app
4. Copy the `firebaseConfig` object shown

### Paste your config into BOTH:
- `booking.html` — replace the placeholder firebaseConfig
- `admin.html` — replace the placeholder firebaseConfig

### Set up Firestore:
1. In Firebase Console → **Firestore Database** → Create database
2. Start in **test mode** (you can tighten rules later)
3. The collection `bookings` will be created automatically on first booking

### Set up Firebase Auth (for admin login):
1. Firebase Console → **Authentication** → Get Started
2. Enable **Email/Password** sign-in
3. Add your email (hello.pawlishedpaws@gmail.com) as a user with a password

### Firestore Security Rules (recommended):
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /bookings/{doc} {
      allow create: if true;           // anyone can submit a booking
      allow read, update, delete: if request.auth != null;  // only logged-in admin
    }
  }
}
```

---

## Step 3 — Deploy to Vercel

1. Push this folder to a GitHub repository
2. Go to [vercel.com](https://vercel.com) → **Add New Project**
3. Import your GitHub repo
4. Leave all settings as default (it's a static site)
5. Click **Deploy**
6. Connect your custom domain in Vercel settings if you have one

That's it — your site is live!

---

## Optional: Contact Form Emails

The contact form on `contact.html` currently shows a success message but doesn't send emails.
To actually receive contact messages, sign up for [Formspree](https://formspree.io) (free plan available):

1. Create a Formspree form and get your form ID
2. Change the `<form>` tag in contact.html to:
   ```html
   <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```

---

## Updating Prices & Services

All prices are in `services.html` and `index.html`. Search for `€` to find and update them.

---

## Questions?

Your site was built by Claude (Anthropic). To make changes, describe what you'd like updated and Claude can edit the files for you.

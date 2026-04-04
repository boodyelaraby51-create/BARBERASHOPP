# M-Ragab Barber

Production-ready barber shop website built with Next.js, Tailwind CSS, and Firebase.

## Features

- Modern dark UI, responsive design
- Dynamic gallery (regular + before/after)
- Booking system with:
  - no double booking
  - minimum 1-hour gap
- Reviews with stars + comments
- Protected admin route (`/admin`) with password login
- Admin controls:
  - upload/delete gallery images
  - manage bookings
  - dashboard stats (total, daily, busy hours)
- WhatsApp quick contact button

## Local Setup

1. Install dependencies:

```bash
npm install
```

2. Create env file:

```bash
cp .env.example .env.local
```

3. Fill Firebase values in `.env.local`.
4. Run app:

```bash
npm run dev
```

5. Open [http://localhost:3000](http://localhost:3000).

## Firebase Setup

- Create Firestore collections:
  - `bookings`
  - `gallery`
  - `reviews`
- Enable Firebase Storage for image upload
- Set `NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET` from Firebase Console exactly
  - preferred format: `your-project-id.firebasestorage.app`
  - older projects may use: `your-project-id.appspot.com`
- Create Firestore index for gallery sorting:
  - collection: `gallery`
  - field: `createdAtMs` (descending)
- Add basic Firestore indexes if prompted by Firebase console

### Storage Rules (quick test)

Use temporary rules while testing uploads:

```txt
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if true;
    }
  }
}
```

After confirming uploads work, lock rules down based on your auth policy.

## Deploy

Deploy on Vercel:

1. Import this project in Vercel
2. Add all `.env.local` variables in Vercel Project Settings
3. Deploy

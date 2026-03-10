# MODELITE Backend

This is the backend for the MODELITE modeling agency website with Firebase integration, user authentication, and admin panel.

## Setup

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Firebase Setup:**
   - Create a Firebase project at https://console.firebase.google.com/
   - Enable Firestore Database
   - Enable Firebase Authentication
   - Go to Project Settings > Service Accounts > Generate new private key
   - Download the JSON file and copy its contents to `.env`
   - The project ID is already configured as `modelite-a1887`

3. **Configure environment variables:**
   - Fill in your Firebase service account details from the downloaded JSON
   - Configure email settings for notifications
   - Set a secure SESSION_SECRET

4. **Create Admin User:**
   - In Firebase Console > Authentication, create a user account for admin
   - In Firestore, create a document in `users` collection with the user's UID as document ID
   - Set the document data: `{ role: "admin" }`

5. **Start the server:**
   ```bash
   npm start
   ```

   For development with auto-restart:
   ```bash
   npm run dev
   ```

6. **Access the application:**
   - Main site: `http://localhost:3000`
   - Admin login: `http://localhost:3000/login`
   - Admin panel: `http://localhost:3000/admin` (requires login)

## Features

- **User Authentication:** Session-based admin authentication
- **Database Integration:** Firebase Firestore for data storage
- **Contact Form:** Saves submissions to database and sends email notifications
- **Admin Panel:** Dashboard to manage contact form submissions
- **Email Notifications:** Automatic emails for new inquiries

## API Endpoints

### Public
- `GET /` - Main website
- `POST /contact` - Submit contact form

### Authentication
- `GET /login` - Admin login page
- `POST /auth/login` - Admin login
- `POST /auth/logout` - Admin logout

### Admin (Protected)
- `GET /admin` - Admin dashboard
- `GET /api/contacts` - Get all contact submissions
- `PUT /api/contacts/:id` - Update contact status

## Firebase Collections

- `contacts` - Contact form submissions
- `users` - User accounts with roles

## Environment Variables

See `.env` file for all required variables. Key ones:

```
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n..."
FIREBASE_CLIENT_EMAIL=firebase-adminsdk-xxxxx@your-project.iam.gserviceaccount.com
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password
SESSION_SECRET=your-secure-random-string
```
- `POST /contact` - Handles contact form submission
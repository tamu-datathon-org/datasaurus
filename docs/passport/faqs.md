---
sidebar_label: 'FAQs'
sidebar_position: 2
---
# FAQs

## How is it used?
Passport provides a simple user interface for volunteers to check people into an event. Once navigating to the passport page, the QR code of participants is scanned using a camera, and all that needs to be done is click the designated button for the event that they are attending.

## How do I get started?
Populate the .env.* files and remove the .example extension.
Run the following commands
```
npm install
npm run dev
```
Visit http://localhost:3000/passport on your browser.

## How do I bypass authentication locally?
1. Remove `<UserProvider>` from `/pages/_app.tsx`
2. Remove not operator (`!`) from `!user?.isAdmin` in `/pages/index.tsx`

## How does scanning work?
By importing [react-qr-reader](https://www.npmjs.com/package/react-qr-reader), we are able to read in their assigned QR code with a webcam and access their passport data
(e.g., name, email, authentication ID).

From there, we handle any errors that may occur with the scanning. If everything succeeds, then we're finished,
and we can check in participants to events or add/remove volunteers.

## How do database updates work?
Database updates work by fetching the participant's authentication ID (obtained through the QR code) and sending an API request
to our database depending on if we're adding, deleting, etc. 

Upon a successful update, we will display a success message, or the corresponding error message if the update fails.


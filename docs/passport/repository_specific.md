---
sidebar_label: 'Repository Specific Material'
sidebar_position: 6
---
# Repository Specific Material

## How does scanning work?
By importing [react-qr-reader](https://www.npmjs.com/package/react-qr-reader), we are able to read in their assigned QR code with a webcam and access their passport data
(e.g., name, email, authentication ID).

From there, we handle any errors that may occur with the scanning. If everything succeeds, then we're finished,
and we can check in participants to events or add/remove volunteers.

## How do database updates work?
Database updates work by fetching the participant's authentication ID (obtained through the QR code) and sending an API request
to our database depending on if we're adding, deleting, etc. 

Upon a successful update, we will display a success message, or the corresponding error message if the update fails.
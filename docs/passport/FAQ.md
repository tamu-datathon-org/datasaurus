---
sidebar_label: 'FAQ'
sidebar_position: 5
---
# FAQ

## How is it used?

Passport provides a simple user interface for volunteers to check people into an event. Once navigating to the passport page, the QR code of participants is scanned using a camera, and all that needs to be done is click the designated button for the event that they are attending. 

## How do I bypass authentication locally?

1. Remove `<UserProvider>` from `/pages/_app.tsx`
2. Remove not operator (`!`) from `!user?.isAdmin` in `/pages/index.tsx`
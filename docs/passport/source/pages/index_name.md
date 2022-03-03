# Contains the documentation for pages/index.tsx

## Imports

```ts
1. import { Text, Page, Divider, useToasts, Card, Link } from '@geist-ui/react';
2. import { useState, useEffect } from 'react';
3. import { orgName } from '../components/constants';
4. import { Navbar } from '../components/Navbar';
5. import { useActiveUser } from '../components/UserProvider';
6. import dynamic from 'next/dynamic';
7. import moment from 'moment';
8. const QrReader: any = dynamic(() => import('react-qr-reader'), { ssr: false });
```
1. Imported from react for aesthetics
2. Imported from react for aesthetics
3. Retrieve our org name 'TAMU Datathon'
4. Ensures Navbar is on the top of the page
5. Finds out which user we are providing the page to (if we decide to provide personalized stuff later)
6. Allows for dynamic client-side scripting.
7. Retrieve time/date (i.e, an event start time)
8. Reads QR codes with react (server side rendering is false)

## Functions

**defaultParticipantData**

```ts
const defaultParticipantData: participantPassportDataInterface = {
  authId: '404',
  name: 'Participant Not Found',
  email: '404@tamudatathon.com',
  yearsAttended: [],
  diningAttended: []
};
```

This is what a participant's passport looks like if they're not registered in our system

-----

**updateDatabase**


```ts
const updateDatabase = (authId: string, updatedObject, setToast) => {
  fetch(`/passport/api/${authId}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ updatedObject: updatedObject })
  })
    .then((response) => response.json())
    .then(() => {
      setToast({ text: 'Participant data updated!', type: 'warning', delay: 3000 });
    })
    .catch((error) => {
      console.error('Error:', error);
      setToast({ text: 'Could not update participant data.', type: 'error', delay: 3000 });
    });
};
```

The above function is used to update a user's information in the DB when we declare that they are attending an event (as well as its error handling)

-----

**updateAttendedEvents and removeAttendedEvents**

```ts
const updateAttendedEvents = (authId: string, eventId: string, setToast) => {
  fetch(`/passport/api/${authId}`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ eventId, userAuthId: authId })
  })
    .then((response) => response.json())
    .then(() => {
      setToast({ text: 'Participant data updated!', type: 'warning', delay: 3000 });
    })
    .catch((error) => {
      console.error('Error:', error);
      setToast({ text: 'Could not update participant data.', type: 'error', delay: 3000 });
    });
};

const updateAttendedEvents = (authId: string, eventId: string, setToast) => {
  fetch(`/passport/api/${authId}`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ eventId, userAuthId: authId })
  })
    .then((response) => response.json())
    .then(() => {
      setToast({ text: 'Participant data updated!', type: 'warning', delay: 3000 });
    })
    .catch((error) => {
      console.error('Error:', error);
      setToast({ text: 'Could not update participant data.', type: 'error', delay: 3000 });
    });
};
```

This allows us to update the events that the user is attending or no longer attending (on the website that we use for check-in NOT in the DB)

-----

**addVolunteer and removeVolunteer**

```ts
  const addVolunteer = () => {
    setIsParticipantVolunteer(true);
    fetch(`/passport/api/volunteer`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ userAuthId: scannedCode })
    })
      .then((response) => response.json())
      .then(() => {
        setToast({ text: 'User data updated!', type: 'warning', delay: 3000 });
      })
      .catch((error) => {
        console.error('Error:', error);
        setToast({ text: 'Could not update user data.', type: 'error', delay: 3000 });
      });
  };

  const removeVolunteer = () => {
    setIsParticipantVolunteer(false);
    fetch(`/passport/api/volunteer?userAuthId=${scannedCode}`, {
      method: 'DELETE',
      headers: {
        'Content-Type': 'application/json'
      }
    })
      .then((response) => response.json())
      .then(() => {
        setToast({ text: 'User data updated!', type: 'warning', delay: 3000 });
      })
      .catch((error) => {
        console.error('Error:', error);
        setToast({ text: 'Could not update user data.', type: 'error', delay: 3000 });
      });
  };
```

These give us the ability to add/remove users as our volunteers for the event!

-----

:::tip Other functions

The rest of the functions are essentially identical, serving the purpose of updating a participant's data when they attend/unattend an event in our DB. Additionally,
it looks for admin authentication.

:::

:::tip Need Local Admin Authentication?

If you are trying to access http://localhost:3000/passport, and it says you're not an admin, refer to the instructions in the FAQ page.

:::
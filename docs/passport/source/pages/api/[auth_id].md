# Contains the documentation for pages/api/[auth_id].tsx

## Imports

```ts
1. import nextConnect from 'next-connect';
2. import { deleteOneObject, findOneObject, findQueriedObjects, insertOneObject, updateOneObject } from './helper';
3. import { NextApiRequest, NextApiResponse } from 'next';
4. import { authenticatedFetch, getBaseUrl } from '../../libs';
5. import { GatekeeperRequestError, User } from '../../components/UserProvider';
```

1. Handles API requests and API responses.
2. Imported from our helper function, with self-explanatory function names.
3. Handles API requests and API responses.
4. Authenticates the user route.
5. Handles errors received from [gatekeeper](https://github.com/tamu-datathon-org/gatekeeper)

## Functions

**sendParticipantPassportData**

```ts
const sendParticipantPassportData = async (req: NextApiRequest, res: NextApiResponse, user: User) => {
  const filteredVolunteers = await findQueriedObjects('volunteers', { userAuthId: user.authId });
  const userIsVolunteer = filteredVolunteers.length > 0;
  if (user.isAdmin || userIsVolunteer) {
    const participantAuthId = req.query.auth_id;
    const participantData = await findOneObject('users', { authId: participantAuthId });

    if (!participantData) {
      res.json({ passportData: defaultParticipantData, attendedEventsData: [] });
    } else {
      let participantName = 'Not Provided';
      if (participantData.firstName && participantData.lastName) participantName = `${participantData.firstName} ${participantData.lastName}`;

      const participantPassportData: participantPassportDataInterface = await findOneObject('passport', { authId: participantAuthId });
      const participantAttendedEventsData = await findQueriedObjects('attendedevents', { userAuthId: participantAuthId });
      const participantAttendedEventIds = participantAttendedEventsData.map((d) => d.eventId);

      // if participant passport doesn't exist yet, create one
      if (!participantPassportData) {
        await insertOneObject('passport', {
          authId: participantAuthId,
          yearsAttended: [],
          diningAttended: []
        });
        res.json({
          passportData: {
            authId: participantData.authId,
            name: participantName,
            email: participantData.email,
            yearsAttended: [],
            diningAttended: []
          },
          attendedEventsData: participantAttendedEventIds
        });
      } else {
        res.json({
          passportData: {
            authId: participantData.authId,
            name: participantName,
            email: participantData.email,
            yearsAttended: participantPassportData.yearsAttended,
            diningAttended: participantPassportData.diningAttended
          },
          attendedEventsData: participantAttendedEventIds
        });
      }
    }
  } else {
    res.json({ success: false, message: 'Need admin permissions.' });
  }
};
```

Firstly, this checks for if a user is an admin or a volunteer to allow access. Otherwise, we send an error message.

Then, if a user is registered, their data is updated accordingly.

If a user isn't registered (their passport data does not exist), then we create a passport for them.

-----

**updateParticipantPassportData**

```ts
const updateParticipantPassportData = async (req: NextApiRequest, res: NextApiResponse, user: User) => {
  const filteredVolunteers = await findQueriedObjects('volunteers', { userAuthId: user.authId });
  const userIsVolunteer = filteredVolunteers.length > 0;
  if (user.isAdmin || userIsVolunteer) {
    const updatedObject = req.body.updatedObject;
    try {
      await updateOneObject('passport', { authId: updatedObject.authId }, updatedObject);
      res.json({ success: true });
    } catch (error) {
      console.log(error);
      res.json({ success: false });
    }
  } else {
    res.json({ success: false, message: 'Need admin permissions.' });
  }
};
```

This updates the participant's passport data in our DB.

-----

**addParticipantAttendedEvents**

```ts
const addParticipantAttendedEvents = async (req: NextApiRequest, res: NextApiResponse, user: User) => {
  const filteredVolunteers = await findQueriedObjects('volunteers', { userAuthId: user.authId });
  const userIsVolunteer = filteredVolunteers.length > 0;
  if (user.isAdmin || userIsVolunteer) {
    const eventId = req.body.eventId;
    const userAuthId = req.body.userAuthId;
    console.log('eventId:', eventId, 'userAuthId:', userAuthId);
    try {
      await insertOneObject('attendedevents', { eventId, userAuthId, timeStamp: new Date() });
      res.json({ success: true });
    } catch (error) {
      console.log(error);
      res.json({ success: false });
    }
  } else {
    res.json({ success: false, message: 'Need admin permissions.' });
  }
};
```

This adds an event attended to the participant's passport data in our DB.

-----

**deleteParticipantAttendedEvents**

```ts
const deleteParticipantAttendedEvents = async (req: NextApiRequest, res: NextApiResponse, user: User) => {
  const filteredVolunteers = await findQueriedObjects('volunteers', { userAuthId: user.authId });
  const userIsVolunteer = filteredVolunteers.length > 0;
  if (user.isAdmin || userIsVolunteer) {
    const eventId = req.body.eventId;
    const userAuthId = req.body.userAuthId;
    try {
      await deleteOneObject('attendedevents', { userAuthId, eventId });
      res.json({ success: true });
    } catch (error) {
      console.log(error);
      res.json({ success: false });
    }
  } else {
    res.json({ success: false, message: 'Need admin permissions.' });
  }
};
```

This deletes an attended event from our participant's passport data in our DB.

:::tip Fun Fact

Each of the functions have error handlers, which go through [gatekeeper](https://github.com/tamu-datathon-org/gatekeeper)

:::
# Contains the documentation for pages/api/volunteer.tsx

## Imports

```ts
1. import nextConnect from 'next-connect';
2. import { deleteOneObject, findOneObject, findQueriedObjects, insertOneObject, updateOneObject } from './helper';
3. import { NextApiRequest, NextApiResponse } from 'next';
4. import { authenticatedFetch, getBaseUrl } from '../../libs';
5. import { GatekeeperRequestError, User } from '../../components/UserProvider';
```

1. Handles API requests and Responses
2. Helper file with self-explanatory function names
3. Handles API requests and Responses
4. Authenticates the user route
5. Catches errors with [gatekeeper](https://github.com/tamu-datathon-org/gatekeeper)

## Functions

**addUserAsVolunteer**

```ts
const addUserAsVolunteer = async (req: NextApiRequest, res: NextApiResponse, user: User) => {
  if (user.isAdmin) {
    const userAuthId = req.body.userAuthId;
    try {
      await insertOneObject('volunteers', { userAuthId });
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

This allows us to add a specific user as a volunteer to handle event check-in

-----

**removeUserAsVolunteer**

```ts
const addUserAsVolunteer = async (req: NextApiRequest, res: NextApiResponse, user: User) => {
  if (user.isAdmin) {
    const userAuthId = req.body.userAuthId;
    try {
      await insertOneObject('volunteers', { userAuthId });
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

This allows us to remove a specific user as a volunteer that used to handle event check-in

-----

:::tip Fun Fact

The rest of the code is handlers, which uses nextconnect and works alongside the above functions.

:::
# Contains the documentation for libs/middleware.ts

## Imports
```ts
1. import { VercelResponse, VercelRequest } from '@vercel/node';
2. import { User, GatekeeperRequestError } from '../components/UserProvider';
3. import { getBaseUrl, authenticatedFetch } from './fetcher';
```
1. Provides communication with [Vercel](https://vercel.com/docs)
2. Verifies if there's a [gatekeeper](https://github.com/tamu-datathon-org/gatekeeper) error
3. Imported from our [fetcher](fetcher) to ensure that the URL they are trying to reach is valid

## Functions

**authenticatedRoute**

```ts
export const authenticatedRoute =
  (handler: AuthenticatedRouteHandler) =>
  async (req: VercelRequest, res: VercelResponse): Promise<void> => {
    const response: User | GatekeeperRequestError = await authenticatedFetch(`${getBaseUrl(req)}/auth/user`, req);

    if ((response as GatekeeperRequestError).statusCode === 401)
      return res
        .writeHead(302, {
          Location: `/auth/login?r=${req.url}`
        })
        .end();

    return handler(req, res, response as User);
  };
```

:::tip Purpose

Essentially, this checks if the route is valid by checking if there is a [Gatekeeper](https://github.com/tamu-datathon-org/gatekeeper) error and handles errors accordingly.

:::
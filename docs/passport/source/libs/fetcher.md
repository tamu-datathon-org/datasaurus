# Contains the documentation for libs/fetcher.ts

## Imports


```ts title
1. import fetch from 'isomorphic-unfetch';
2. import { VercelRequest } from '@vercel/node';
```

1. This is imported as we needed a package to dynamically switch between JS 'fetch' and 'node-fetch' based on usage.
2. This is imported so that we can send API requests to [Vercel](https://vercel.com/docs)


## Functions

**fetcher and authenticatedFetch**

```ts
export async function fetcher<JSON = unknown>(input: RequestInfo, init?: RequestInit): Promise<JSON> {
  const res = await fetch(input, {
    ...init,
    headers: {
      ...init?.headers,
      accept: 'application/json'
    }
  });
  return res.json();
}

export const authenticatedFetch = <JSON = unknown>(input: RequestInfo, req: VercelRequest, init?: RequestInit): Promise<JSON> => {
  const { accessToken } = req.cookies;
  return fetcher(input, {
    ...init,
    headers: {
      ...init?.headers,
      Cookie: `accessToken=${accessToken}`
    }
  });
};
```

These two functions work together by fetching/requesting information as well as checking if the fetch is valid.

-----

**getBaseUrl**

```ts
export const getBaseUrl = (req: VercelRequest): string => {
  const httpProto = req.headers['x-forwarded-proto'] || 'https';
  return `${httpProto}://${req.headers.host}`;
};
```

This function is so that we can retrieve our base URL.

:::tip Purpose

The purpose of this file is to fetch data as needed such as base URL and access tokens.

:::
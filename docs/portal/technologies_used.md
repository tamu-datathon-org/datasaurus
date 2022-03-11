---
sidebar_label: 'Technologies Used'
sidebar_position: 3
---
# Technologies Used

* @fortawesome
    - styles
    - [https://www.npmjs.com/package/fortawesome](https://www.npmjs.com/package/fortawesome)
* @googlecloud/firestore
    - connect with database
    - [https://www.npmjs.com/package/@google-cloud/firestore](https://www.npmjs.com/package/@google-cloud/firestore)
* gray-matter
    - parsing md (src/libs/activitiesApi.ts)
    - [https://www.npmjs.com/package/gray-matter/v/0.5.2](https://www.npmjs.com/package/gray-matter/v/0.5.2)
* react-markdown
    - files are stored as markdown (TODO confirm this)
    - renders these markdown files (src/common/ActivityInfo/ActivityInfo.tsx)
    - [https://www.npmjs.com/package/react-markdown](https://www.npmjs.com/package/react-markdown)
* express
    - Routes API with Next.js to create serverless functions
    - [https://expressjs.com/en/5x/api.html](https://expressjs.com/en/5x/api.html)
* http-proxy
    - Connects to the host through a proxy
    - [https://www.npmjs.com/package/http-proxy](https://www.npmjs.com/package/http-proxy)
* isomorphic-unfetch
    -  Dynamically switches between JS 'fetch' and 'node-fetch'
    - [https://openbase.com/js/isomorphic-unfetch/documentation](https://openbase.com/js/isomorphic-unfetch/documentation)
* moment
    - Accesses date and time for things like event start time
    - [https://momentjs.com/docs/](https://momentjs.com/docs/)
* next
    - Dynamic routing, Rest API, server-side rendering etc.
    - [https://nextjs.org/docs](https://nextjs.org/docs)
* @vercel/node
    - Requests and gets a response from Vercel with a node.js runtime
    - [https://vercel.com/docs/runtimes#official-runtimes/](https://vercel.com/docs/runtimes#official-runtimes/)

:::tip Fun Fact

This information is "heavily inspiried" by work [Chris](https://github.com/S1nthesis) did on the [passport documentation](https://tamudatathon.com/docs/passport/overview)

:::
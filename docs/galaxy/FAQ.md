---
sidebar_label: 'FAQ'
sidebar_position: 2
---
# FAQs

### How is it used?
Galaxy serves to be the central network point where all requests sent to Galaxy will be redirected to the respective places.

### How do I install Galaxy?
1. Clone the repository ``` $ git clone --recurse-submodules https://github.com/tamu-datathon-org/galaxy.git ```
2. Install [Docker](https://docs.docker.com/get-docker/)
3. Install [Docker_Compose](https://docs.docker.com/compose/install/)
4. Enter this command `$ docker-compose up `

### How do I create a new route?
1. Go to the vercel.json file
2. Either on the redirect or the rewrite array, copy paste the code below
```
{source: "/route", destination: "url"}
```
3. Change the route value to what you would like the route to be and change the destination url to a valid url that you want the user to be directed to if they have route value.

:::tip
To understand the difference between rewrite and array, check the vercel.json page.
:::
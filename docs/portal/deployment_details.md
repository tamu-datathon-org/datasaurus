---
sidebar_label: 'Deployment Details'
sidebar_position: 4
---
# Deployment Details

* Environment Variables (view secrets repository - portal.env.local file)
    - GATEKEEPER_INTEGRATION_SECRET (needed to authenticate so that user can have special interactions with portal (sign up for event reminders) (TODO figure this out))
    - FIRESTORE_CREDENTIALS (needed to access firestore database (I think event info/generation is stored here (TODO figure this out)))

* Deployed using vercel at [https://dev.tamudatathon.com/events](https://dev.tamudatathon.com/events)
    - Github: [https://github.com/tamu-datathon-org/portal](https://github.com/tamu-datathon-org/portal)
    - Production branch: master
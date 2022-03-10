---
sidebar_label: 'addEvent'
sidebar_position: 1
---
# addEvent

* adds an event to the database by adding a document of the specified form to the 'ScheduledEvents' collection of the database (goes through [https://dev.tamudatathon.com/auth/user](https://dev.tamudatathon.com/auth/user) (TODO confirm endpoint) and has the structure:
    - eventId (identifier of the event)
    - userAuthId (unique id of user trying to add this event)
* the document reference inside the 'ScheduledEvents' collection is a md5 hash of res.query.eventId + user.authId
* the document content is the structure specified above
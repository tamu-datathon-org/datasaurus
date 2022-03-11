---
sidebar_label: 'removeEvent'
sidebar_position: 4
---
# removeEvent


* removes(unadds) the event for the user in our database by deleting the associated document
* the document reference inside the 'ScheduledEvents' collection is a md5 hash of res.query.eventId + user.authId
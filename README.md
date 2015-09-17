# Conference Central App

Conference Central is an application using Google APP Engine (GAE). The functionality of this application allows users to view and create conferences from various locations and topics. Users can register for conferences, view the associated sessions, and add the sessions they are interested in to their wishlist.

Upon successful creation of a session an automated email is sent to that user to confirm the addition of their conference, this is done utilizing the task functionality of GAE. A cron job has been implemented to monitor the available remaining tickets to each conference, this number is stored in Memcache and announcements are in place to notify users of conferences that will potentially be sold out.

Finally, an additional task utilizing Memcache has been implemented to set the featured speaker for each session where applicable.

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Functionality

Udacity provided base functionality, I have implementing the following additional endpoints:

* Task 1 - Sessions:
  * createSession
  * getConferenceSessions
  * getConferenceSessionsByType
  * getSessionsBySpeaker
* Task 2 - Wishlist:
  * addSessionToWishlist
  * getSessionsInWishlist
* Task 3 - Additional Queries:
  * getConferenceSessionsByName
  * getConferenceSessionsByDuration
  * Problem Statement - How can we query sessions not after 7 PM and not workshops?: Unfortunately the App Engine does not support multiple inequality queries. A potential workaround is to build a complex query and respective front end form in which the user can select the start and end times of their availability. The user could then choose the types of sessions they are interested in, allowing multiples to be selected. Making each of these fields optional would allow the user for this use case the ability to insert 7 PM as their end time, and select every type of session that isn't a workshop.
* Task 4 - Featured Speaker:
  * getFeaturedSpeaker()  

Design Choices:
For the sake of simplicity, and code readability, I decided to implement each endpoint and query as a stand alone solution. Furthermore each added functionality is entirely segregated from the starting functionality, wherever possible. For example, instead of integrating Sessions to use the Conference's copy to form method I implemented a separate copy to form method for Sessions. This provided the added benefit of streamlined troubleshooting. Future work could include refactoring these two methods together, as well as reducing the number of separate queries for Sessions and their respective forms.

As for the properties of a Session, they are each saved as Strings, Integers, and Date/Time fields. No entities have been created throughout the added Session functionality.

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
2. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
3. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
4. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
5. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
6. (Optional) Generate your client library(ies) with [the endpoints tool][6].
7. Deploy your application.

## Authors

Jasen Carroll  
jasen.c@icloud.com  
Sept 15, 2015  


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool

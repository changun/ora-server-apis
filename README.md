Ora-Server-APIs
===============

Ora APIs can be breakdown into three groups: *Lifestreams Login*, *Oauth*, and *Ora* described below. An Ora server is up and running at http://lifestreams.smalldata.io; and an Ora-client demo app is running at http://lifestreams.smalldata.io/ora-demo/.  

#1. Lifestreams Login

  * **GET** */login* (required parameter ***redirect***)
      * This API starts the login process of Lifestreams. An Ora client should have a *"Sign-in with Google"* button which, upon click, directs user to this API. A ***redirect*** parameter should be given to let Lifestreams server know where the user should be redirected to after login. 
      
      * If sign-in succeeded, the server will redirect the user to the ***redirect*** url with ***key*** and ***uid*** paramters appended. The ***key*** is a temporary token for the client to interact with Lifestreams server in behalf of the user. The ***uid*** is the unique identifier of the user in the system. Please remember both of them as they will be needed in the subsequent requests.
      
      * If sign-in failed, the server will redirect the user to the ***redirect*** url with ***error*** parameter appended, which specifies the reason of failure. 
      *
      * Note that the redirect parameter must be a full and properly encoded url. **Example**: http://lifestreams.smalldata.io/login?redirect=http%3A%2F%2Fwww.google.com%0A
        
#2. Oauth
  * **GET** */oauth/check-auth* (required parameter ***key*** and ***provider***)
      * This API allows a client to check wheter the user has connected a specific data provider with Lifestreams or not. Currently, the supported providers are *gmail* and *moves* (case sensitive).
      
      * A Ora client should prevent the user from entering the Ora main UI if the user has not connected either gmail or moves with Lifestreams.
      
      * **Example**: http://lifestreams.smalldata.io/oauth/check-auth?provider=gmail&key=[KEY_RETURNED_BY_LOGIN_API]
      
  *  **GET** */oauth/auth* (required parameter ***key***, ***provider***, and ***redirect***)
      * This API starts the OAuth procedure for the user to connect his account on a specific data provider with Lifestreams and redirects the user to the ***redirect*** url when procedure finished.
      * **Example**: http://lifestreams.smalldata.io/oauth/check-auth?provider=gmail&key=[KEY_RETURNED_BY_LOGIN_API]&redirect=http%3A%2F%2Fwww.google.com%0A

#3. Ora
  * **GET** */ora/users* (required paramter: ***key***)
      * Returns a JSON array containing all the exisitng Ora users' uids (including the requesting user him or herself).
      * **Sample Response**
      
        ```json
        ["c8fcd06d-ed99-4575-bb95-1a33a033b0a8"]
        ```
        
  * **GET** */ora/* ***:uid:*** */profile* (required paramter: ***key***. The ***uid*** segment of the url must be a valid uid returned in the previous API)
      * Returns a JSON object that contains the profile of a specific user.
      * **Sample Response**  
      
        ```json   
        {
          "gender": "male",
          "kind": "plus#person",
          "etag": "\"L2Xbn8bDuSErT6QA3PEQiwYKQxM/9SHkEZNOlNTsRKphI_BpoXRbWlw\"",
          "circledByCount": 301,
          "name": {
            "familyName": "Hsieh",
            "givenName": "Cheng-Kang"
          },
          "placesLived": [
            {
              "value": "Westwood, Los Angeles",
              "primary": true
            }
          ],
          "image": {
            "url": "https://lh5.googleusercontent.com/-avgCwMqBMeU/AAAAAAAAAAI/AAAAAAAADeY/tOOV8UzYiE8/photo.jpg?sz=50",
            "isDefault": false
          },
          "urls": [
            {
              "value": "http://picasaweb.google.com/changun.tw",
              "type": "otherProfile",
              "label": "Picasa ç¶²é ç›¸ç°¿"
            }
          ],
          "language": "en",
          "displayName": "Cheng-Kang Hsieh (Andy)",
          "emails": [
            {
              "value": "changun.tw@gmail.com",
              "type": "account"
            }
          ],
          "nickname": "Andy",
          "url": "https://plus.google.com/108274213374340954232",
          "uid": "c8fcd06d-ed99-4575-bb95-1a33a033b0a8",
          "organizations": [
            {
              "name": "University of California, Los Angeles",
              "type": "school",
              "endDate": "2012",
              "primary": false
            },
            {
              "name": "UCLA",
              "title": "PhD Student",
              "type": "work",
              "startDate": "2011",
              "primary": true
            }
          ],
          "isPlusUser": true,
          "verified": false,
          "id": "108274213374340954232",
          "objectType": "person"
        }
        ```
        
  * **GET** */ora/* ***:uid:*** */daily*  (required paramter: ***key***. Optional parameters: ***start*** and ***end*** in ISO8601 local date format e.g. 2014-09-09)
      * Returns everyday's daily summary of a Ora user in the time range specified by ***start*** and ***end*** parameters.
      * **Sample Response**
      
      ```json
      {
        "vars": [
          "local_date",
          "time_leave_home",
          "time_return_home",
          "backhome_dur",
          "if_detect_home",
          "mobility_data_coverage",
          "geodiameter",
          "exercise_dur",
          "email_sent_count",
          "liwc_posmo_count",
          "liwc_negemo_count",
          "liwc_anx_count",
          "liwc_anger_count",
          "liwc_sad_count",
          "liwc_family_count",
          "liwc_health_count",
          "liwc_work_count",
          "liwc_home_count",
          "liwc_social_count",
          "total_wordcount",
          "distinct_recipients"
        ],
        "bindings": [
          {
            "email_sent_count": "3",
            "geodiameter": "4537.000329780274e0",
            "total_wordcount": "72",
            "if_detect_home": "false",
            "local_date": "2014-09-03",
            "time_return_home": "2014-09-03T23:42:34-04:00",
            "distinct_recipients": "2",
            "mobility_data_coverage": "0.355775462962962962962960",
            "exercise_dur": "42.666666666666666666666665",
            "time_leave_home": "2014-09-03T13:01:12-04:00"
          },
          {
            "email_sent_count": "1",
            "geodiameter": "4482.50208215825e0",
            "total_wordcount": "11",
            "if_detect_home": "true",
            "local_date": "2014-09-04",
            "time_return_home": "2014-09-04T19:24:14-04:00",
            "distinct_recipients": "1",
            "mobility_data_coverage": "0.999976851851851851851846",
            "exercise_dur": "100.399999999999999999999996",
            "time_leave_home": "2014-09-04T10:30:56-04:00"
          },
          {
            "email_sent_count": "1",
            "geodiameter": "629.4482199809705e0",
            "total_wordcount": "12",
            "liwc_social_count": "2",
            "if_detect_home": "true",
            "local_date": "2014-09-05",
            "time_return_home": "2014-09-05T16:50:18-04:00",
            "distinct_recipients": "1",
            "liwc_posmo_count": "1",
            "mobility_data_coverage": "0.884050925925925925925923",
            "exercise_dur": "34.666666666666666666666664",
            "time_leave_home": "2014-09-05T13:12:24-04:00"
          },
          {
            "email_sent_count": "5",
            "geodiameter": "238.95624696551278e0",
            "total_wordcount": "287",
            "liwc_social_count": "15",
            "if_detect_home": "true",
            "local_date": "2014-09-07",
            "time_return_home": "2014-09-07T12:33:28-04:00",
            "distinct_recipients": "5",
            "mobility_data_coverage": "0.919351851851851851851849",
            "exercise_dur": "15.649999999999999999999998",
            "time_leave_home": "2014-09-07T12:07:25-04:00"
          },
          {
            "email_sent_count": "11",
            "geodiameter": "4537.000329780274e0",
            "total_wordcount": "1368",
            "if_detect_home": "true",
            "local_date": "2014-09-08",
            "time_return_home": "2014-09-08T19:25:58-04:00",
            "distinct_recipients": "6",
            "mobility_data_coverage": "0.907337962962962962962959",
            "exercise_dur": "93.466666666666666666666658",
            "time_leave_home": "2014-09-08T09:11:13-04:00"
          },
          {
            "email_sent_count": "6",
            "geodiameter": "4482.50208215825e0",
            "total_wordcount": "509",
            "if_detect_home": "false",
            "local_date": "2014-09-09",
            "time_return_home": "2014-09-09T18:17:27-04:00",
            "distinct_recipients": "5",
            "mobility_data_coverage": "0.409293981481481481481479",
            "exercise_dur": "39.449999999999999999999997",
            "time_leave_home": "2014-09-09T17:04:04-04:00"
          },
          {
            "email_sent_count": "8",
            "geodiameter": "4482.50208215825e0",
            "total_wordcount": "157",
            "if_detect_home": "true",
            "local_date": "2014-09-10",
            "time_return_home": "2014-09-10T21:56:26-04:00",
            "distinct_recipients": "3",
            "mobility_data_coverage": "0.999976851851851851851845",
            "exercise_dur": "84.333333333333333333333327",
            "time_leave_home": "2014-09-10T09:04:38-04:00"
          },
          {
            "email_sent_count": "6",
            "geodiameter": "4482.50208215825e0",
            "total_wordcount": "119",
            "backhome_dur": "278.983333333333333333333333",
            "if_detect_home": "true",
            "local_date": "2014-09-11",
            "time_return_home": "2014-09-11T23:23:25-04:00",
            "distinct_recipients": "5",
            "mobility_data_coverage": "0.987974537037037037037033",
            "exercise_dur": "82.016666666666666666666663",
            "time_leave_home": "2014-09-11T10:06:52-04:00"
          },
          {
            "email_sent_count": "12",
            "geodiameter": "4523.834801616812e0",
            "total_wordcount": "326",
            "if_detect_home": "true",
            "local_date": "2014-09-12",
            "time_return_home": "2014-09-12T23:06:22-04:00",
            "distinct_recipients": "7",
            "mobility_data_coverage": "0.981979166666666666666663",
            "exercise_dur": "78.599999999999999999999993",
            "time_leave_home": "2014-09-12T14:57:11-04:00"
          },
          {
            "email_sent_count": "5",
            "geodiameter": "165.5365950618983e0",
            "total_wordcount": "227",
            "if_detect_home": "false",
            "local_date": "2014-09-13",
            "time_return_home": "2014-09-13T14:03:34-04:00",
            "distinct_recipients": "3",
            "mobility_data_coverage": "0.609131944444444444444443",
            "exercise_dur": "7.383333333333333333333332",
            "time_leave_home": "2014-09-13T13:56:30-04:00"
          },
          {
            "email_sent_count": "2",
            "geodiameter": "482.72855195706654e0",
            "total_wordcount": "61",
            "liwc_social_count": "11",
            "if_detect_home": "true",
            "local_date": "2014-09-14",
            "time_return_home": "2014-09-14T21:23:42-04:00",
            "distinct_recipients": "2",
            "mobility_data_coverage": "0.401585648148148148148146",
            "exercise_dur": "26.666666666666666666666666",
            "time_leave_home": "2014-09-14T20:50:59-04:00"
          },
          {
            "email_sent_count": "6",
            "geodiameter": "4482.50208215825e0",
            "total_wordcount": "208",
            "if_detect_home": "true",
            "local_date": "2014-09-15",
            "time_return_home": "2014-09-15T21:01:20-04:00",
            "distinct_recipients": "6",
            "mobility_data_coverage": "0.999988425925925925925921",
            "exercise_dur": "90.949999999999999999999998",
            "time_leave_home": "2014-09-15T12:01:41-04:00"
          },
          {
            "email_sent_count": "10",
            "geodiameter": "4482.50208215825e0",
            "total_wordcount": "504",
            "if_detect_home": "true",
            "local_date": "2014-09-16",
            "time_return_home": "2014-09-16T19:32:54-04:00",
            "distinct_recipients": "9",
            "mobility_data_coverage": "0.999988425925925925925923",
            "exercise_dur": "81.116666666666666666666664",
            "time_leave_home": "2014-09-16T10:29:13-04:00"
          },
          {
            "email_sent_count": "4",
            "geodiameter": "3980869.891739659e0",
            "total_wordcount": "307",
            "if_detect_home": "false",
            "local_date": "2014-09-17",
            "time_return_home": "2014-09-17T18:14:45-04:00",
            "distinct_recipients": "3",
            "mobility_data_coverage": "0.716354166666666666666664",
            "exercise_dur": "63.416666666666666666666660",
            "time_leave_home": "2014-09-17T05:53:56-04:00"
          },
          {
            "email_sent_count": "10",
            "geodiameter": "564.7134810415039e0",
            "total_wordcount": "530",
            "if_detect_home": "false",
            "local_date": "2014-09-18",
            "time_return_home": "2014-09-18T18:09:52-07:00",
            "distinct_recipients": "5",
            "mobility_data_coverage": "0.296828703703703703703702",
            "exercise_dur": "39.183333333333333333333332",
            "time_leave_home": "2014-09-18T17:33:47-07:00"
          }
        ]
      }
        ```

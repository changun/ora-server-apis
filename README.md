Ora-Server-APIs
===============

Ora APIs can be breakdown into three groups: *Lifestreams Login*, *Oauth*, and *Ora* described below. An Ora server is up and running at http://lifestreams.smalldata.io; and an Ora-client demo app is running at http://lifestreams.smalldata.io/ora-demo/.  

#1. Lifestreams Login

  * **GET** */login* (required parameter ***redirect***)
      * This API starts the login process of Lifestreams. An Ora client should have a *"Sign-in with Google"* button which, upon click, directs user to this API. A ***redirect*** parameter should be specified to let Lifestreams server know where the user should be redirected to after login. 
      
      * If sign-in succeeded, the server will redirect the user to the ***redirect*** url with ***key*** and ***uid*** paramters appended. The ***key*** is a temporary token for the client to interact with Lifestreams server on behalf of the user. The ***uid*** is the unique identifier of the user in the system. Please remember both of them as they will be needed in the subsequent requests.
      
      * If sign-in failed, the server will redirect the user to the ***redirect*** url with ***error*** parameter appended, which specifies the reason of failure. 
      *
      * Note that the redirect parameter must be a full and properly encoded url. 
      * **Example**: http://lifestreams.smalldata.io/login?redirect=http%3A%2F%2Fwww.google.com%0A
        
#2. OAuth
  * **GET** */oauth/check-auth* (required parameter ***key*** and ***provider***)
      * This API allows the client to check wheter the user has connected a specific data provider with Lifestreams or not. Currently, the supported providers are *gmail* and *moves* (case sensitive).
      
      * A Ora client should prevent the user from entering the Ora main UI if the user has not connected either gmail or moves with Lifestreams.
      
      * **Example**: http://lifestreams.smalldata.io/oauth/check-auth?provider=gmail&key=[KEY_RETURNED_BY_LOGIN_API]
      
  *  **GET** */oauth/auth* (required parameter ***key***, ***provider***, and ***redirect***)
      * This API starts the OAuth procedure for the user to connect his a specific data provider with Lifestreams and redirects the user to the ***redirect*** url when procedure finished.
      * **Example**: http://lifestreams.smalldata.io/oauth/check-auth?provider=gmail&key=[KEY_RETURNED_BY_LOGIN_API]&redirect=http%3A%2F%2Fwww.google.com%0A

#3. Ora
  * **GET** */ora/users* (required paramter: ***key***)
      * Returns a JSON array containing all the exisitng Ora users' uids (including the requesting user him or herself).
      * **Sample Response**
      
        ```json
        ["c8fcd06d-ed99-4575-bb95-1a33a033b0a8"]
        ```
        
  * **GET** */ora/users* (required paramter: ***key***)
      * Returns a JSON array that contains the profile of every ora user.
      * **Sample Response**  
      
        ```json   
        [
         {
          "image": {
           "url": "https://lh3.googleusercontent.com/-XdUIqdMkCWA/AAAAAAAAAAI/AAAAAAAAAAA/XXXXXXX/photo.jpg?sz=50",
           "isDefault": true
          },
          "nickname": null,
          "name": {
           "familyName": "Lin",
           "givenName": "Jeremy"
          },
          "uid": "80ea77a6-ec6e-413d-976a-6db1eb312742"
         }]
        ```
        
  * **GET** */ora/daily/* ***:uid:*** (required paramter: ***key***)
      * Returns the ora values for the past one month.
      
 ```json
 [
  {
    "date": "2014-09-11",
    "ora": 0.6904825267906114
  },
  {
    "date": "2014-09-12",
    "ora": 0.9983850400237735
  },
  {
    "date": "2014-09-13",
    "ora": -1.0652965608000242
  },
  {
    "date": "2014-09-14",
    "ora": -0.6704432406572466
  },
  {
    "date": "2014-09-15",
    "ora": 0.2948324335736158
  },
  {
    "date": "2014-09-16",
    "ora": 0.7322439274906163
  },
  {
    "date": "2014-09-17",
    "ora": 0.8631033887312078
  },
  {
    "date": "2014-09-18",
    "ora": 0.1894859517698796
  },
  {
    "date": "2014-09-19",
    "ora": -1.0575117490605168
  },
  {
    "date": "2014-09-20",
    "ora": -0.368981300926988
  },
  {
    "date": "2014-09-21",
    "ora": -0.08740587778399556
  },
  {
    "date": "2014-09-22",
    "ora": -0.48279126049581383
  },
  {
    "date": "2014-09-23",
    "ora": -0.7200818636079014
  },
  {
    "date": "2014-09-24",
    "ora": -0.38208321135884626
  },
  {
    "date": "2014-09-25",
    "ora": 0.27015282379153865
  },
  {
    "date": "2014-09-26",
    "ora": -0.13717963029869706
  },
  {
    "date": "2014-09-27",
    "ora": -0.3458113928832
  },
  {
    "date": "2014-09-28",
    "ora": -1.049114971780712
  },
  {
    "date": "2014-09-29",
    "ora": 0.021082441763395687
  },
  {
    "date": "2014-09-30",
    "ora": -0.30131719331778894
  },
  {
    "date": "2014-10-01",
    "ora": 0.4667103756762252
  },
  {
    "date": "2014-10-02",
    "ora": -1.1921080312813321
  },
  {
    "date": "2014-10-03",
    "ora": 0.11989589218418342
  },
  {
    "date": "2014-10-04",
    "ora": -0.3609193668400114
  },
  {
    "date": "2014-10-05",
    "ora": 0
  },
  {
    "date": "2014-10-06",
    "ora": 0.24551167468515997
  },
  {
    "date": "2014-10-07",
    "ora": 0.39983378173445805
  },
  {
    "date": "2014-10-08",
    "ora": 0.2074980757279516
  },
  {
    "date": "2014-10-09",
    "ora": 0.176879477414204
  },
  {
    "date": "2014-10-10",
    "ora": 0.4797198426317008
  },
  {
    "date": "2014-10-11",
    "ora": 1.2023778774220553
  },
  {
    "date": "2014-10-12",
    "ora": -0.43883080921768935
  },
  {
    "date": "2014-10-13",
    "ora": -0.47546237054572926
  },
  {
    "date": "2014-10-14",
    "ora": 0.2447810850361717
  },
  {
    "date": "2014-10-15",
    "ora": -0.10409858586981963
  },
  {
    "date": "2014-10-16",
    "ora": -0.10340031020685661
  },
  {
    "date": "2014-10-17",
    "ora": 0.3455487446405206
  },
  {
    "date": "2014-10-18",
    "ora": 0.6513959493417607
  },
  {
    "date": "2014-10-19",
    "ora": -0.5439557739967691
  },
  {
    "date": "2014-10-20",
    "ora": 1.080517794983472
  },
  {
    "date": "2014-10-21",
    "ora": 0.4020704384266858
  },
  {
    "date": "2014-10-22",
    "ora": -0.13647972937403677
  },
  {
    "date": "2014-10-23",
    "ora": -0.03667111926250302
  },
  {
    "date": "2014-10-24",
    "ora": -0.13797706940704735
  },
  {
    "date": "2014-10-25",
    "ora": -0.7226651169451276
  },
  {
    "date": "2014-10-26",
    "ora": -0.03584873021587659
  },
  {
    "date": "2014-10-27",
    "ora": -1.019570526627818
  },
  {
    "date": "2014-10-28",
    "ora": -0.06667618346283878
  },
  {
    "date": "2014-10-29",
    "ora": 1.4146674875726584
  },
  {
    "date": "2014-10-30",
    "ora": 0.3837695015649585
  },
  {
    "date": "2014-10-31",
    "ora": 0.18584750234606656
  },
  {
    "date": "2014-11-01",
    "ora": -0.7335007467241814
  },
  {
    "date": "2014-11-02",
    "ora": 0.3402905658090582
  },
  {
    "date": "2014-11-03",
    "ora": 0.15059782991972054
  },
  {
    "date": "2014-11-04",
    "ora": -0.006667472100237604
  },
  {
    "date": "2014-11-05",
    "ora": 0.35935313836660365
  },
  {
    "date": "2014-11-06",
    "ora": 0.5178483068770896
  },
  {
    "date": "2014-11-07",
    "ora": -0.527689461231148
  },
  {
    "date": "2014-11-08",
    "ora": 0
  },
  {
    "date": "2014-11-09",
    "ora": 0
  }
]
      ```
  * **GET** */ora/hourly/* ***:uid:*** */* ***:iso-date:*** (required paramter: ***key***)
      * Returns the hourly ora values for the given day.
     
 ```json
{

  "0": 0,
  "1": 0,
  "2": 0,
  "3": 0,
  "4": 0,
  "5": 0,
  "6": 0,
  "7": 0,
  "8": 0,
  "9": 0,
  "10": 0,
  "11": 0,
  "12": 0,
  "13": 0.38611007690429844,
  "14": 0,
  "15": 0.39000000000000234,
  "16": 0.0025005340576171875,
  "17": 0.129999999999999,
  "18": 0.26805580139160057,
  "19": 0.01027679443359375,
  "20": 0,
  "21": 0.9569435119628906,
  "22": 0.485834960937499,
  "23": 0.042499542236328125

}
      ```


#3. Features
 * **Mobility Features**
  * local_date, 
  * mobility_data_coverage
     * the coverage of mobility data. One should take the accuracy of mobility features (especially the home-related features) with a grain of salt if the coverage is lower than a threshold (says 60%).
  * geodiameter
  * exercise_dur
     * how much time (**in minutes**) the user spent exercising (walking/running/cycling etc.)
  * if_detect_home
     * whether the user stays at the same location at the begining and at the end of the day. Only consider the home-related features below meaningful, when this value is *true*.
  * time_leave_home
     * the first time in the day the user left home.
  * time_return_home
     * the last time the user returned home.
     * Note that, when *time_return_home < time_leave_home*, it means the user stays at home whole day.
  * backhome_dur
     * the amount of time (**in minutes**), between the above leave/return home interval, the user was at home.
 * **Email Features**
  * email_sent_count
     * number of emails sent.
  * liwc_posmo_count
     * number Positive Emotions words wrriten. (See: http://www.liwc.net/comparedicts.php)
  * liwc_negemo_count
  * liwc_anx_count
  * liwc_anger_count
  * liwc_sad_count
  * liwc_family_count
  * liwc_health_count
  * liwc_work_count
  * liwc_home_count
  * liwc_social_count
  * total_wordcount
     * total number of words.
  * distinct_recipients
     * total number of distince recipients (including cced).
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

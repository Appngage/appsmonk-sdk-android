# Push Campaign API

The Appsmonk Push Campaign API is an API that allows users to send push campaigns from your own systems.

##Prerequisites

- Appsmonk Push API token.

- Live API key corresponding to the app from which you want to push.


> Both can be obtained from the settings page of the [Appsmonk DashBoard](https://dashboard.appsmonk.com/)

##Calling Push Campaign API
 
Appsmonk Push Campaign POST at:

[https://dashboard.appsmonk.com/run_campaign](https://dashboard.appsmonk.com/run_campaign)

###Request structure

Request content-type must be 'application/json'.

###Body

The body of the request must contain a valid POST parameters as example mentioned below :

```
{
	"api_key":"YOUR APP live key",
	"campaign_name":"this campaign is called by",
	push_date_time":"now",
	"target":'All',
	"creative_heading":["Monday Special Offer","Monday Speacial Offer"],
	"creative_img":["http://path/to/some_file_name.png","http://path/to/other_file_name.png"],
	"deeplink":[],
	"creative_text":["Flat 50% sale on shoes","Monday Special offer. Buy any shoe and get flat 50% off "],
	"creative_percentage":["50","50"]
}
```
###parameters
-<b>api_key</b>: Unique api_key(live_key) of app obtained from [Appsmonk DashBoard](https://dashboard.appsmonk.com/)
- <b>campaign_name</b> (string): Unique name of the campaign.
- <b>push_date_time</b> (string): Time that Appsmonk servers will start sending push notifications GMT (UTC+0000). Format is "yyyy-MM-dd HH:mm:ss eg:2015-09-29 05:09:19". Alternatively, if "now" is assigned, the campaign will activate and send immediately .
- <b>group_target[]</b> (array/string,optional): if passing Email ids pass array example array('test@example.com') | if mentioned 'All'(string) it'll be sent to All users 

> creatives 

- <b>creative_heading[]</b>:Heading of the creative number 1				
- <b>creative_img[]</b>: A link/URL of an image which apears in the push notifications expanded view (Optional)
- <b>deeplink[]</b>:A link/URL based on a URL scheme that you specify within your app. Appsmonk Push campaigns can accept this link scheme to direct users to a particular area within your app upon opening the push notification. (Optional)
- <b>creative_text[]</b>: The Message that will be displayed upon opening the push notification. 
- <b>creative_percentage[]</b>:Percentage of users that this variant will be sent

> For multiple creatives(Fallow the same schema. Maximum number of creatives can be 10)

- <b>creative_heading[]</b>:Heading of the creative number 2
- <b>creative_img[]</b>:A link/URL of an image which apears in the push notifications expanded view (Optional)
- <b>deeplink[]</b>:A link/URL based on a URL scheme that you specify within your app. Appsmonk Push campaigns can accept this link scheme to direct users to a particular area within your app upon opening the push notification. (Optional)
- <b>creative_text[]</b>:The Message that will be displayed upon opening the push notification. 
- <b>creative_percentage[]</b>: Percentage of users that this variant will be sent 

###Responses

####Success</b>

If the POST to the API endpoint is successfull you will receieve an 
```json
{"resp":{"status":0,"msg":"Push sent successfully to 'total_sent(number)' users"}}
```
Or
```json
{"resp":{"status":0,"msg":"Push successfully Recorded"}}
```
####Failure

```
If the POST data does not meet the API requirements you will receive an actionable error message. Contact us at hello@appsmonk.com if you need further support.

INVALID_DATE {"resp":{"status":0,"msg":"Invalid Date"}} //Date it should be equal to current date or higher
Invalid_COUNTRY_CODE {"resp":{"status":0,"msg":"Invalid Country Code"}} //Country Code should be from the list given below
SEGMENT_INVAID {"resp":{"status":0,"msg":"Invalid Segment Id"}} // SEGMENT Id should be between 1-4
API_KEY_INVALID {"resp":{"status":0,"msg":"Invalid API Key"}} // Must provide Valid api_key
```


###CURL example for PHP

```php
                $post = array(
		    'api_key' => 'Your App LIVE KEY',
                    'campaign_name' => 'this campaign is called by API',
                    'push_date_time' => 'now',
                    'target' => 'All',
                    'creative_heading' => array('creative heading number 1','creative heading number 2'),             
                    'creative_img' => array('http://somewhere/path/to/some_file_name.png','http://somewhere/path/to/other_file_name.png'),
                    'deeplink' => array(),
                    'creative_text' => array('Flat 50% sale on shoes','Monday Special offer. Buy any shoe and get flat 50% off'),
                    'creative_percentage' => array('50','50')
                    );

                    $headers = array(
                            'Content-Type: application/json'
                    );
                    $url = 'https://dashboard.appsmonk.com/run_campaign_api';
                    $ch = curl_init();
                    curl_setopt( $ch, CURLOPT_URL, $url );
                    curl_setopt( $ch, CURLOPT_POST, true );
                    curl_setopt( $ch, CURLOPT_SSL_VERIFYPEER, 0);
                    curl_setopt( $ch, CURLOPT_HTTPHEADER, $headers );
                    curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
                    curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode($post));
                   	echo $result = curl_exec( $ch );
                    if ( curl_errno( $ch ) )
                    {
                         echo 'Error: ' . curl_error( $ch );
                    }
                    curl_close( $ch );
```


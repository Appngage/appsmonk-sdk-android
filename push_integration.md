# Push Campaign API

The Appngage Push Campaign API is an API that allows users to send push campaigns from your own systems.

###Prerequisites

- Appngage Push API token.

- Live API key corresponding to the app from which you want to push.


> Both can be obtained from the settings page of the [Appngage DashBoard](https://dashboard.appngage.com/)

###Calling Push Campaign API
 
Appngage Push Campaign POST at:

[https://dashboard.appngage.com/run_campaign](https://dashboard.appngage.com/run_campaign)

####Request structure

Request content-type must be 'application/x-www-form-urlencoded; charset=UTF-8'.

####Body

The body of the request must contain a valid POST parameters mentioned below:

```
campaign_name:hellooo 
push_time:specify
push_date_time:2015-09-29 12:54:55
user_target:all
group_target[]:1
group_target[]:3
group_target[]:4
location_target[]:IN
location_target[]:US
creative_heading[]:Creative Number 1					
creative_img[]:http://somewhere/here/there/some_file_name.png
deeplink[]:
creative_text[]:Hello How is it going .?
creative_percentage[]:50
creative_heading[]:Creative Number 2	
creative_img[]:http://somewhere/elseWhere/there/here/other_file_name.png
deeplink[]:
creative_text[]:Can we help you with anything ?
creative_percentage[]:50
```
####parameters
- <b>campaign_name</b>: Unique name of the campaign (string).
- <b>push_date_time</b>: Time that Appngage servers will start sending push notifications GMT (UTC+0000). Format is "yyyy-MM-dd HH:mm:ss eg:2015-09-29 05:09:19". Alternatively, if "now" is assigned, the campaign will activate and send immediately (string).
- <b>group_target[]</b>: {0 - All | 1 - New | 2 - Engaged | 3 - Inactive | 4 - One-Time }  (number,optional)
- <b>location_target[]</b>: (county code, optional)

> creatives 

- <b>creative_heading[]</b>:Heading of the creative number 1				
- <b>creative_img[]</b>: A link/URL of an image which apears in the push notifications expanded view (Optional)
- <b>deeplink[]</b>:A link/URL based on a URL scheme that you specify within your app. Appngage Push campaigns can accept this link scheme to direct users to a particular area within your app upon opening the push notification. (Optional)
- <b>creative_text[]</b>: The Message that will be displayed upon opening the push notification. 
- <b>creative_percentage[]</b>:Percentage of users that this variant will be sent

> For multiple creatives(Fallow the same schema. Maximum number of creatives can be 10)

- <b>creative_heading[]</b>:Heading of the creative number 2
- <b>creative_img[]</b>:A link/URL of an image which apears in the push notifications expanded view (Optional)
- <b>deeplink[]</b>:A link/URL based on a URL scheme that you specify within your app. Appngage Push campaigns can accept this link scheme to direct users to a particular area within your app upon opening the push notification. (Optional)
- <b>creative_text[]</b>:The Message that will be displayed upon opening the push notification. 
- <b>creative_percentage[]</b>: Percentage of users that this variant will be sent 

####CURL example for PHP

```php
                $post = array(
      							'campaign_name' => 'hellooo', 
                    'push_date_time' => '2015-09-29 12:54:55'
                    'group_target' => array(1,2,3,4),
                    'location_target' => array('IN','US'),
                    'creative_heading' => array('creative heading 1','creative heading 2'),				
                    'creative_img' => array('http://somewhere/here/there/some_file_name.png','http://somewhere/elseWhere/there/here/other_file_name.png'),
                    'deeplink' => array(),
                    'creative_text' => array('Hello How is it going .?','can we help with anything'),
                    creative_percentage[] => array('50','50')
					);
					
                    $headers = array(
							'Authorization: key=' . $apiKey,
							'Content-Type: application/x-www-form-urlencoded; charset=UTF-8'
					);
					$url = 'https://dashboard.appngage.com/run_campaign';
					$ch = curl_init();
					curl_setopt( $ch, CURLOPT_URL, $url );
					curl_setopt( $ch, CURLOPT_POST, true );
					curl_setopt( $ch, CURLOPT_SSL_VERIFYPEER, 0);
					curl_setopt( $ch, CURLOPT_HTTPHEADER, $headers );
					curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
					curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode( $post ) );
					echo $result = curl_exec( $ch );
					if ( curl_errno( $ch ) )
					{
						echo 'Error: ' . curl_error( $ch );
					}
					curl_close( $ch );
```

#### Valid Country Codes

```
* AD    Andorra
* AE    United Arab Emirates
* AF    Afghanistan
* AG    Antigua and Barbuda
* AI    Anguilla
* AL    Albania
* AM    Armenia
* AN    Netherlands Antilles
* AO    Angola
* AR    Argentina
* AS    American Samoa
* AT    Austria
* AU    Australia
* AW    Aruba
* AX    Åland Islands
* AZ    Azerbaijan
* BA    Bosnia and Herzegovina
* BB    Barbados
* BD    Bangladesh
* BE    Belgium
* BF    Burkina Faso
* BG    Bulgaria
* BH    Bahrain
* BI    Burundi
* BL    Saint Barthélemy
* BM    Bermuda
* BN    Brunei
* BO    Bolivia
* BR    Brazil
* BS    Bahamas
* BT    Bhutan
* BV    Bouvet Island
* BW    Botswana
* BY    Belarus
* BZ    Belize
* CA    Canada
* CC    Cocos [Keeling] Islands
* CD    Congo - Kinshasa
* CF    Central African Republic
* CG    Congo - Brazzaville
* CH    Switzerland
* CI    Côte d’Ivoire
* CK    Cook Islands
* CL    Chile
* CM    Cameroon
* CN    China
* CO    Colombia
* CR    Costa Rica
* CU    Cuba
* CV    Cape Verde
* CX    Christmas Island
* CY    Cyprus
* CZ    Czech Republic
* DE    Germany
* DJ    Djibouti
* DK    Denmark
* DM    Dominica
* DO    Dominican Republic
* DZ    Algeria
* EC    Ecuador
* EE    Estonia
* EG    Egypt
* EH    Western Sahara
* ER    Eritrea
* ES    Spain
* ET    Ethiopia
* FI    Finland
* FJ    Fiji
* FK    Falkland Islands
* FM    Micronesia
* FO    Faroe Islands
* FR    France
* GA    Gabon
* GB    United Kingdom
* GD    Grenada
* GE    Georgia
* GF    French Guiana
* GH    Ghana
* GI    Gibraltar
* GL    Greenland
* GM    Gambia
* GN    Guinea
* GP    Guadeloupe
* GQ    Equatorial Guinea
* GR    Greece
* GS    South Georgia and the South Sandwich Islands
* GT    Guatemala
* GU    Guam
* GW    Guinea-Bissau
* GY    Guyana
* HK    Hong Kong SAR China
* HM    Heard Island and McDonald Islands
* HN    Honduras
* HR    Croatia
* HT    Haiti
* HU    Hungary
* ID    Indonesia
* IE    Ireland
* IL    Israel
* IN    India
* IO    British Indian Ocean Territory
* IQ    Iraq
* IR    Iran
* IS    Iceland
* IT    Italy
* JM    Jamaica
* JO    Jordan
* JP    Japan
* KE    Kenya
* KG    Kyrgyzstan
* KH    Cambodia
* KI    Kiribati
* KM    Comoros
* KN    Saint Kitts and Nevis
* KP    North Korea
* KR    South Korea
* KW    Kuwait
* KY    Cayman Islands
* KZ    Kazakhstan
* LA    Laos
* LB    Lebanon
* LC    Saint Lucia
* LI    Liechtenstein
* LK    Sri Lanka
* LR    Liberia
* LS    Lesotho
* LT    Lithuania
* LU    Luxembourg
* LV    Latvia
* LY    Libya
* MA    Morocco
* MC    Monaco
* MD    Moldova
* ME    Montenegro
* MG    Madagascar
* MH    Marshall Islands
* MK    Macedonia
* ML    Mali
* MM    Myanmar [Burma]
* MN    Mongolia
* MO    Macau SAR China
* MP    Northern Mariana Islands
* MQ    Martinique
* MR    Mauritania
* MS    Montserrat
* MT    Malta
* MU    Mauritius
* MV    Maldives
* MW    Malawi
* MX    Mexico
* MY    Malaysia
* MZ    Mozambique
* NA    Namibia
* NC    New Caledonia
* NE    Niger
* NF    Norfolk Island
* NG    Nigeria
* NI    Nicaragua
* NL    Netherlands
* NO    Norway
* NP    Nepal
* NR    Nauru
* NU    Niue
* NZ    New Zealand
* OM    Oman
* PA    Panama
* PE    Peru
* PF    French Polynesia
* PG    Papua New Guinea
* PH    Philippines
* PK    Pakistan
* PL    Poland
* PM    Saint Pierre and Miquelon
* PN    Pitcairn Islands
* PR    Puerto Rico
* PS    Palestinian Territories
* PT    Portugal
* PW    Palau
* PY    Paraguay
* QA    Qatar
* RE    Réunion
* RO    Romania
* RS    Serbia
* RU    Russia
* RW    Rwanda
* SA    Saudi Arabia
* SB    Solomon Islands
* SC    Seychelles
* SD    Sudan
* SE    Sweden
* SG    Singapore
* SH    Saint Helena
* SI    Slovenia
* SJ    Svalbard and Jan Mayen
* SK    Slovakia
* SL    Sierra Leone
* SM    San Marino
* SN    Senegal
* SO    Somalia
* SR    Suriname
* ST    São Tomé and Príncipe
* SV    El Salvador
* SY    Syria
* SZ    Swaziland
* TC    Turks and Caicos Islands
* TD    Chad
* TF    French Southern Territories
* TG    Togo
* TH    Thailand
* TJ    Tajikistan
* TK    Tokelau
* TL    Timor-Leste
* TM    Turkmenistan
* TN    Tunisia
* TO    Tonga
* TR    Turkey
* TT    Trinidad and Tobago
* TV    Tuvalu
* TW    Taiwan
* TZ    Tanzania
* UA    Ukraine
* UG    Uganda
* UM    U.S. Outlying Islands
* US    United States
* UY    Uruguay
* UZ    Uzbekistan
* VA    Vatican City
* VC    Saint Vincent and the Grenadines
* VE    Venezuela
* VG    British Virgin Islands
* VI    U.S. Virgin Islands
* VN    Vietnam
* VU    Vanuatu
* WF    Wallis and Futuna
* WS    Samoa
* YE    Yemen
* YT    Mayotte
* ZA    South Africa
* ZM    Zambia
* ZW    Zimbabwe
```

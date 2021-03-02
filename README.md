# Enviar-POST-con-php
Enviar datos por POST usando PHP

## POST Con CURL

```php
$query = array(
		'client_id' => $apiKey,
		'client_secret' => $secret,
		'code' => $code
);

// Build access token URL
$access_token_url = "https://{$shop}/admin/oauth/access_token";

// Configure curl client and execute request
$curl = curl_init();
$curlOptions = array(
  	CURLOPT_RETURNTRANSFER => TRUE,
		CURLOPT_URL => $access_token_url,
		CURLOPT_POSTFIELDS => http_build_query($query)
);

curl_setopt_array($curl, $curlOptions);

$jsonResponse = json_decode(curl_exec($curl), TRUE);

curl_close($curl);

return $jsonResponse['access_token'];
  ```

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

## GET

```php
$url = "https://{$shop}/admin/api/{$api_version}/{$resource}.json";

$curlOptions = array(
	CURLOPT_RETURNTRANSFER => TRUE
);

if ($method == 'GET') {
	if (!is_null($params)) {
		$url = $url . "?" . http_build_query($params);
	}
} else {
	$curlOptions[CURLOPT_CUSTOMREQUEST] = $method;
}

$curlOptions[CURLOPT_URL] = $url;

$requestHeaders = array(
	"X-Shopify-Access-Token: ${token}",
	"Accept: application/json"
);

if ($method == 'POST' || $method == 'PUT') {
	$requestHeaders[] = "Content-Type: application/json";

	if (!is_null($params)) {
		$curlOptions[CURLOPT_POSTFIELDS] = json_encode($params);
	}
}

$curlOptions[CURLOPT_HTTPHEADER] = $requestHeaders;

$curl = curl_init();
curl_setopt_array($curl, $curlOptions);
$response = curl_exec($curl);
curl_close($curl);

return json_decode($response, TRUE);
```

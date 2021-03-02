# Enviar-POST-con-php
Enviar datos por POST usando PHP

## REQUEST Con CURL

```php
function doCurl($url, $post = null, $headers = null, $type = "POST")
{
	$ch = curl_init();

	if ($headers) {
		curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
	}

	if ($type == "POST") {
		curl_setopt($ch, CURLOPT_POST, true);
		curl_setopt($ch, CURLOPT_POSTFIELDS, $post);
		curl_setopt($ch, CURLOPT_URL, $url);
	}

	if ($type == "GET") {
		if ($post) {
			curl_setopt($ch, CURLOPT_URL, $url . "?" . http_build_query($post));
		} else {
			curl_setopt($ch, CURLOPT_URL, $url);
		}
	}

	if ($type == "PUT") {
		curl_setopt($ch, CURLOPT_URL, $url);
		curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PUT");
		curl_setopt($ch, CURLOPT_POSTFIELDS, $post);
	}

	curl_setopt($ch, CURLOPT_TIMEOUT, 30);
	curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 5);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);


	$output = curl_exec($ch);
	curl_close($ch);

	//    if($_SESSION['LOGIN_ADMIN']['user_id']=="1934") {
	////        echo curl_error($ch);
	////        print_r(curl_getinfo($ch));
	////        echo "output: ".$output;
	//    }

	return $output;
}
```

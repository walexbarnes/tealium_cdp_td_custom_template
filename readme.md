# Goal: 
Deploy the Treasure Data Customer Data Platform SDK on the website through Tealium IQ. Utilize `fetchUserSegments` method of `td` object to programatically access the CDP segments to which the user belongs, and pass them along to Adobe Target for use in A/B tests and personalization programs. 
# Constraint:
There is no Treasure Data Tag Template in Tealium. I have to use a custom template to accomplish this use case, modifying it as needed. 
# What We Receieved
Below is the code I receieved from Treasure Data. I have to manipulate this code into the custom tag template in Tealium.
```
!function(t,e){if(void 0===e[t]){e[t]=function(){e[t].clients.push(this),this._init=[Array.prototype.slice.call(arguments)]},e[t].clients=[];for(var r=function(t){return function(){return this["_"+t]=this["_"+t]||[],this["_"+t].push(Array.prototype.slice.call(arguments)),this}},s=["addRecord","blockEvents","fetchServerCookie","fetchGlobalID","fetchUserSegments","resetUUID","ready","setSignedMode","setAnonymousMode","set","trackEvent","trackPageview","trackClicks","unblockEvents"],n=0;n<s.length;n++){var c=s[n];e[t].prototype[c]=r(c)}var o=document.createElement("script");o.type="text/javascript",o.async=!0,o.src=("https:"===document.location.protocol?"https:":"http:")+"//cdn.treasuredata.com/sdk/2.5/td.min.js";var a=document.getElementsByTagName("script")[0];a.parentNode.insertBefore(o,a)}}("Treasure",this);
</script>
<script type="text/javascript">
  // Configure an instance for your database
  var td = new Treasure({
    host: 'withheld,
    writeKey: 'withheld',
    database: 'withheld'
  });
  if (YOUR_ONETRUST_CONSENT_VARIABLE = "Granted") // replace as per your setup 
  {
    td.setSignedMode()
  } else 
  {
    td.setAnonymousMode()
  }
  // Enable cross-domain tracking
  td.set('$global', 'td_global_id', 'td_global_id');
  // Track pageview information to 'pageviews' table
  td.trackPageview('pageviews');  


var SuccessCallback = function (res) {
    var segments = res[0].values   
    console.log("segments: " + segments)
    console.log("res: " + JSON.stringify(res))
}
td.fetchUserSegments({
    'audienceToken': ['withheld'],
    keys: {
        'td_client_id': getCookie('withheld'),
    }
}, SuccessCallback);
```

# The Tag Template
Out of the box, the custom template looks like this. I would have to adjust it, mixing it with the above Treasure Data code to accomplish my use case. 
```//~~tv:20010.20230630
//~~tc: Tealium Custom Container
//~~tc: Updated Tealium loader to 4.35 version

/*
  Tealium Custom Container Notes:
  - Add sending code between "Start Tag Sending Code" and "End Tag Sending Code".
  - Add JavaScript tag library code between "Start Tag Library Code" and "End Tag Library Code".
  - Add JavaScript code only, do not add HTML code in this file.
  - Remove any <script> and </script> tags from the code you place in this file.

  Loading external JavaScript files (Loader):
  - If you need to load an additional external JavaScript file, un-comment the singe-line JavaScript comments ("//") within the following Loader sections near the bottom of this file:
      - "Start Loader Function Call"
      - "End Loader Function Call"
      - "Start Loader Callback Function"
      - "End Loader Callback Function"
  - After un-commenting, insert the path to the external JavaScript file you want to load.
  - Finally, within the Loader callback function, insert the JavaScript code that should run after the external JavaScript file has loaded.
*/

/* Start Tag Library Code */
/* End Tag Library Code */

//tealium universal tag - utag.sender.custom_container ut4.0.##UTVERSION##, Copyright ##UTYEAR## Tealium.com Inc. All Rights Reserved.
try {
  (function (id, loader) {
    var u = {};
    utag.o[loader].sender[id] = u;

    // Please do not modify
    if (utag.ut === undefined) { utag.ut = {}; }
    // Start Tealium loader 4.35
    if (utag.ut.loader === undefined) { u.loader = function (o) { var b, c, l, a = document; if (o.type === "iframe") { b = a.createElement("iframe"); o.attrs = o.attrs || { "height" : "1", "width" : "1", "style" : "display:none" }; for( l in utag.loader.GV(o.attrs) ){ b.setAttribute( l, o.attrs[l] ); } b.setAttribute("src", o.src); }else if (o.type=="img"){ utag.DB("Attach img: "+o.src); b=new Image();b.src=o.src; return; }else{ b = a.createElement("script");b.language="javascript";b.type="text/javascript";b.async=1;b.charset="utf-8"; for( l in utag.loader.GV(o.attrs) ){ b[l] = o.attrs[l]; } b.src = o.src; } if(o.id){b.id=o.id}; if (typeof o.cb=="function") { if(b.addEventListener) { b.addEventListener("load",function(){o.cb()},false); }else { /* old IE support */ b.onreadystatechange=function(){if(this.readyState=='complete'||this.readyState=='loaded'){this.onreadystatechange=null;o.cb()}}; } } l = o.loc || "head"; c = a.getElementsByTagName(l)[0]; if (c) { utag.DB("Attach to "+l+": "+o.src); if (l == "script") { c.parentNode.insertBefore(b, c); } else { c.appendChild(b) } } } } else { u.loader = utag.ut.loader; }
    // End Tealium loader

    u.ev = {view: 1};

    u.initialized = false;

    ##UTGEN##

    u.send = function(a, b) {
      if (u.ev[a] || u.ev.all !== undefined) {
        //##UTENABLEDEBUG##utag.DB("send:##UTID##");

        var c, d, e, f, i;

        u.data = {
          /* Initialize default tag parameter values here */
          /* Examples: */
          /* "account_id" : "1234567" */
          /* "base_url" : "//insert.your.javascript.library.url.here.js" */
          /* A value mapped to "account_id" or "base_url" in TiQ will replace these default values. */
        };


        /* Start Tag-Scoped Extensions Code */
        /* Please Do Not Edit This Section */
        ##UTEXTEND##
        /* End Tag-Scoped Extensions Code */


        /* Start Mapping Code */
        for (d in utag.loader.GV(u.map)) {
          if (b[d] !== undefined && b[d] !== "") {
            e = u.map[d].split(",");
            for (f = 0; f < e.length; f++) {
              u.data[e[f]] = b[d];
            }
          }
        }
        /* End Mapping Code */


        /* Start Tag Sending Code */

          // Insert your tag sending code here.

        /* End Tag Sending Code */


        /* Start Loader Callback Function */
        /* Un-comment the single-line JavaScript comments ("//") to use this Loader callback function. */

        //u.loader_cb = function () {
          //u.initialized = true;
          /* Start Loader Callback Tag Sending Code */

            // Insert your post-Loader tag sending code here.

          /* End Loader Callback Tag Sending Code */
        //};

        /* End Loader Callback Function */


        /* Start Loader Function Call */
        /* Un-comment the single-line JavaScript comments ("//") to use Loader. */

          //if (!u.initialized) {
            //u.loader({"type" : "iframe", "src" : u.data.base_url + c.join(u.data.qsp_delim), "cb" : u.loader_cb, "loc" : "body", "id" : 'utag_##UTID##' });
            //u.loader({"type" : "script", "src" : u.data.base_url, "cb" : u.loader_cb, "loc" : "script", "id" : 'utag_##UTID##' });
          //} else {
            //u.loader_cb();
          //}

          //u.loader({"type" : "img", "src" : u.data.base_url + c.join(u.data.qsp_delim) });

        /* End Loader Function Call */


        //##UTENABLEDEBUG##utag.DB("send:##UTID##:COMPLETE");
      }
    };
    utag.o[loader].loader.LOAD(id);
  })("##UTID##", "##UTLOADERID##");
} catch (error) {
  utag.DB(error);
}
//end tealium universal tag
```
# The Finished Product
The finished product, fully merged and functioning tag template. 
```
//~~tv:20010.20140827
//~~tc: Tealium Custom Container

/*
  Tealium Custom Container Notes:
  - Add sending code between "Start Tag Sending Code" and "End Tag Sending Code".
  - Add JavaScript tag library code between "Start Tag Library Code" and "End Tag Library Code".
  - Add JavaScript code only, do not add HTML code in this file.
  - Remove any <script> and </script> tags from the code you place in this file.

  Loading external JavaScript files (Loader):
  - If you need to load an additional external JavaScript file, un-comment the singe-line JavaScript comments ("//") within the following Loader sections near the bottom of this file:
      - "Start Loader Function Call"
      - "End Loader Function Call"
      - "Start Loader Callback Function"
      - "End Loader Callback Function"
  - After un-commenting, insert the path to the external JavaScript file you want to load.
  - Finally, within the Loader callback function, insert the JavaScript code that should run after the external JavaScript file has loaded.
*/

/* Start Tag Library Code */
/* End Tag Library Code */

//tealium universal tag - utag.sender.custom_container ut4.0.##UTVERSION##, Copyright ##UTYEAR## Tealium.com Inc. All Rights Reserved.
try {
  (function (id, loader) {
    var u = {};
    utag.o[loader].sender[id] = u;

    // Start Tealium loader 4.32
    // Please do not modify
    if (utag === undefined) { utag = {}; } if (utag.ut === undefined) { utag.ut = {}; } if (utag.ut.loader === undefined) { u.loader = function (o) { var a, b, c, l; a = document; if (o.type === "iframe") { b = a.createElement("iframe"); b.setAttribute("height", "1"); b.setAttribute("width", "1"); b.setAttribute("style", "display:none"); b.setAttribute("src", o.src); } else if (o.type === "img") { utag.DB("Attach img: " + o.src); b = new Image(); b.src = o.src; return; } else { b = a.createElement("script"); b.language = "javascript"; b.type = "text/javascript"; b.async = 1; b.charset = "utf-8"; b.src = o.src; } if (o.id) { b.id = o.id; } if (typeof o.cb === "function") { if (b.addEventListener) { b.addEventListener("load", function () { o.cb(); }, false); } else { b.onreadystatechange = function () { if (this.readyState === "complete" || this.readyState === "loaded") { this.onreadystatechange = null; o.cb(); } }; } } l = o.loc || "head"; c = a.getElementsByTagName(l)[0]; if (c) { utag.DB("Attach to " + l + ": " + o.src); if (l === "script") { c.parentNode.insertBefore(b, c); } else { c.appendChild(b); } } }; } else { u.loader = utag.ut.loader; }
    // End Tealium loader

    u.ev = {'view' : 1, 'link' : 1};

    u.initialized = false;

    ##UTGEN##

    u.send = function(a, b) {
      if (u.ev[a] || u.ev.all !== undefined) {
        //##UTENABLEDEBUG##utag.DB("send:##UTID##");

        var c, d, e, f, i;

        u.data = {
          /* Initialize default tag parameter values here */
          /* Examples: */
          /* "account_id" : "whithheld_int" */
           "base_url" : "withheld.com" 
          /* A value mapped to "account_id" or "base_url" in TiQ will replace these default values. */
        };


        /* Start Tag-Scoped Extensions Code */
        /* Please Do Not Edit This Section */
        ##UTEXTEND##
        /* End Tag-Scoped Extensions Code */


        /* Start Mapping Code */
        for (d in utag.loader.GV(u.map)) {
          if (b[d] !== undefined && b[d] !== "") {
            e = u.map[d].split(",");
            for (f = 0; f < e.length; f++) {
              u.data[e[f]] = b[d];
            }
          }
        }
        /* End Mapping Code */


        /* Start Tag Sending Code */

          // Insert your tag sending code here.
          ! function (t, e) {
            if (void 0 === e[t]) {
                e[t] = function () {
                    e[t].clients.push(this), this._init = [Array.prototype.slice.call(arguments)]
                }, e[t].clients = [];
                for (var r = function (t) {
                    return function () {
                        return this["_" + t] = this["_" + t] || [], this["_" + t].push(Array.prototype.slice.call(arguments)), this
                    }
                }, s = ["addRecord", "blockEvents", "fetchServerCookie", "fetchGlobalID", "fetchUserSegments", "resetUUID", "ready", "setSignedMode", "setAnonymousMode", "set", "trackEvent", "trackPageview", "trackClicks", "unblockEvents"], n = 0; n < s.length; n++) {
                    var c = s[n];
                    e[t].prototype[c] = r(c)
                }
                /*var o = document.createElement("script");
                o.type = "text/javascript", o.async = !0, o.src = ("https:" === document.location.protocol ? "https:" : "http:") + "//cdn.treasuredata.com/sdk/2.5/td.min.js";
                var a = document.getElementsByTagName("script")[0];
                a.parentNode.insertBefore(o, a)*/
            }
        }("Treasure", this);

        /* End Tag Sending Code */


        /* Start Loader Callback Function */
        /* Un-comment the single-line JavaScript comments ("//") to use this Loader callback function. */

        u.loader_cb = function () {
          u.initialized = true;
            
                    /*BEGIN INITIALIZE*/
           if (window.td == undefined){
            var dynamicWriteKey = b.tealium_environment == "prod" ? "withheld_prod_key" : 'withheld_dev_key'
            var dynamicDatabase = b.tealium_environment == "prod" ? "withheld_prod_table" : 'withheld_dev_table'

            var td = new Treasure({
            host: 'in.treasuredata.com/',
            writeKey: dynamicWriteKey,
            database: dynamicDatabase});
        
            window.td = td
        

            /*END INITIALIZE*/

            /* BEGIN ONE TRUST*/
            var oneTrustResponse = b['cp.OptanonConsent']

            if (oneTrustResponse != undefined) {
                if (oneTrustResponse.toLowerCase().indexOf("c0004") > -1) {
                    td.setSignedMode()
                    console.debug('Tealium Status: Treasure Data Initialization: setting signed mode oneTrustResponse is ' +oneTrustResponse);
                } else {
                    td.setAnonymousMode()
                    console.debug('Tealium Status: Treasure Data Initialization: setting anon mode oneTrustResponse is ' +oneTrustResponse);
                }
            }
            else{
                td.setSignedMode();
                        console.debug('Tealium Status: Treasure Data Initialization: setting signed mode because oneTrustResponse is not there' +oneTrustResponse);
            
            }
            /* END ONE TRUST*/
            
            /* BEGIN SET*/
            td.set('$global', 'td_global_id', 'td_global_id');
            /* BEGIN SEGMENT FETCH*/
            var SuccessCallback = function (res) {

                function isEmpty(obj) {
                    return Object.keys(obj).length === 0;
                }
                var segments = res[0].values
                segments = isEmpty(segments) ? "Segments Blank" : segments.toString()
                var attributes = res[0].attributes
                attributes = isEmpty(attributes) ? "Attributes Blank" : JSON.stringify(attributes)
                console.debug("Tealium Status: Treasure Data Segments: " + segments)
                console.debug("Tealium Status: Treasure Data Attributes:" + attributes)
                utag_data.td_attributes = attributes
                utag_data.td_segments = segments
                localStorage.setItem("td_segments", segments)
                localStorage.setItem("td_attributes", attributes)
            }
            
            var myLookupCookie = b['cp.cp_rwd_id']

            window.td.fetchUserSegments({
                'audienceToken': ['withheld_token'],
            
                keys: {
                    'withheld_cookie_name': myLookupCookie,
                }
            }, SuccessCallback);}
            /* END SEGMENT FETCH*/

            if (window.td) {
                console.debug("Treasure data window.td exists")
                //Create an object of arrays... Exclude any local storage values ("ls."), and live person analytics values

                var data_array = Object.entries(b).filter(([key]) => !key.startsWith("ls.") && !key.startsWith("livePersonAnalytics")&& !key.startsWith("ss.")&& !key.startsWith("meta."));
                
     
                 var payload = {};
                 for (let i = 0; i < data_array.length - 1; i++) {
                     payload[data_array[i][0]] = b[data_array[i][0]];
                   }  
                   if (b.tealium_event == "view"){
                   //send TD pageview
                     trackTreasureData("view",payload)
                  
                   }
                     else {
                      trackTreasureData("link",payload)

                     }
                   }
        };

        function trackTreasureData(event_type, data_package)
        {
          setTimeout(function () {
            switch (event_type){
              case "view":
                td.set("withheld_table_name_PAGEVIEWS",data_package)
                td.trackPageview("withheld_table_name_PAGEVIEWS")
                console.debug("Treasure data TE is view")
                break;
              case "link":
                td.set("withheld_table_name_LINKCLICK",data_package)
                td.trackEvent("withheld_table_name_LINKCLICK",data_package)
                console.debug("Treasure data TE is link")
                break;
            }
        }, 1000);

        }
        /* End Loader Callback Function */


        /* Start Loader Function Call */
        /* Un-comment the single-line JavaScript comments ("//") to use Loader. */

          if (!u.initialized) {
            //u.loader({"type" : "iframe", "src" : u.data.base_url + c.join(u.data.qsp_delim), "cb" : u.loader_cb, "loc" : "body", "id" : 'utag_##UTID##' });
            u.loader({"type" : "script", "src" : u.data.base_url, "cb" : u.loader_cb, "loc" : "script", "id" : 'utag_##UTID##' });


          } else {
            u.loader_cb();
          }

          //u.loader({"type" : "img", "src" : u.data.base_url + c.join(u.data.qsp_delim) });

        /* End Loader Function Call */


        //##UTENABLEDEBUG##utag.DB("send:##UTID##:COMPLETE");
      }
    };
    utag.o[loader].loader.LOAD(id);
  })("##UTID##", "##UTLOADERID##");
} catch (error) {
  utag.DB(error);
}
//end tealium universal tag
```

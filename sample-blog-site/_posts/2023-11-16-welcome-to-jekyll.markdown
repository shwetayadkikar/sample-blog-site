---
layout: post
title:  "Welcome to Jekyll!"
date:   2023-11-16 03:48:57 +0000
categories: jekyll update
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

<div>
    <form id="comment-form">
      <label for="name">Name:</label><br>
      <input type="text" id="name" name="name" required=""><br>  
      <label for="email">Email:</label><br>
      <input type="email" id="email" name="email" required=""><br>
      <br>
      <textarea id="comment" name="comment" style="width:100%" placeholder="Enter your comment..." required=""></textarea><br>  
      <button type="submit">Submit</button>
  </form>
  </div> 
<br/>
<style>
.comment-item {
    border-bottom: 1px solid #e8e8e8;
    padding-bottom: 10px;
}
.comment-container {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
}
.comment-info {
    display: flex;
    align-items: center;
    margin-bottom: 8px;
}
.comment-info img {
    border-radius: 50%;
    margin-right: 8px;
}
.comment-text {
    margin-bottom: 8px;
}
.comment-date {
    color: #888;
}
</style>
<div id="comment-container-list">
 
</div>            
<script>  
 async function submitComment() {
          const nameInput = document.getElementById('name');
          const commentInput = document.getElementById('comment');
          const emailInput = document.getElementById('email');
          const name = nameInput.value;
          const comment = commentInput.value;             
          const email = emailInput.value;      
          try {
                const response = await fetch("/api/Comment?page=2023-11-16-welcome-to-jekyll", {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                        // Add any additional headers as needed
                    },                    
                    body: JSON.stringify({name,comment, email }) // Convert the data to JSON string
                });
                if (!response.ok) {
                    throw new Error(`HTTP error! Status: ${response.status}`);
                }
                const responseData = await response.json();
                console.log('Response:', responseData);
                 // Clear the form inputs
                nameInput.value = '';
                commentInput.value = '';
                emailInput.value = '';
            } catch (error) {
                console.error('Error:', error);
            }       
          fetchData();    
        }
 async function fetchData() {
            try {
                const response = await fetch('/api/GetComments?page=2023-11-16-welcome-to-jekyll');
                const data = await response.json();              
                processApiData(data);
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }       
        function processApiData(data) {
            const contentDiv = document.getElementById('comment-container-list');   
            contentDiv.innerHTML = "";         
            data.forEach((item, index) => {               
                var commentContainer = document.createElement('div');
                commentContainer.classList.add('comment-container');
                var commentInfo = document.createElement('div');
                commentInfo.classList.add('comment-info');              
                var nameDiv = document.createElement('div');
                nameDiv.innerHTML = item.commentBy;
                commentInfo.appendChild(nameDiv);
                // Create the comment-text div
                var commentText = document.createElement('div');
                commentText.classList.add('comment-text');
                // Create the paragraph inside comment-text
                var paragraph = document.createElement('p');
                paragraph.textContent = item.comment;
                commentText.appendChild(paragraph);
                // Create the comment-date div
                var commentDate = document.createElement('div');
                commentDate.classList.add('comment-date');
                // Create the small element inside comment-date
                var smallElement = document.createElement('small');
                smallElement.textContent = (new Date(item.timestamp)).toString();
                commentDate.appendChild(smallElement);
                // Append all the created elements to the main container
                commentContainer.appendChild(commentInfo);
                commentContainer.appendChild(commentText);
                commentContainer.appendChild(commentDate);
                // Append the main container to the body
                document.body.appendChild(commentContainer);
                contentDiv.appendChild(commentContainer);
            });           
        }
        // Call the fetchData function when the page loads
        fetchData();
document.getElementById("comment-form").addEventListener("submit", function(event) {
          event.preventDefault(); 
          console.log("Triggered"); 
          submitComment();
          })
</script>
<script type="text/javascript">
!(function (cfg){function e(){cfg.onInit&&cfg.onInit(i)}var S,u,D,t,n,i,C=window,x=document,w=C.location,I="script",b="ingestionendpoint",E="disableExceptionTracking",A="ai.device.";"instrumentationKey"[S="toLowerCase"](),u="crossOrigin",D="POST",t="appInsightsSDK",n=cfg.name||"appInsights",(cfg.name||C[t])&&(C[t]=n),i=C[n]||function(l){var d=!1,g=!1,f={initialize:!0,queue:[],sv:"7",version:2,config:l};function m(e,t){var n={},i="Browser";function a(e){e=""+e;return 1===e.length?"0"+e:e}return n[A+"id"]=i[S](),n[A+"type"]=i,n["ai.operation.name"]=w&&w.pathname||"_unknown_",n["ai.internal.sdkVersion"]="javascript:snippet_"+(f.sv||f.version),{time:(i=new Date).getUTCFullYear()+"-"+a(1+i.getUTCMonth())+"-"+a(i.getUTCDate())+"T"+a(i.getUTCHours())+":"+a(i.getUTCMinutes())+":"+a(i.getUTCSeconds())+"."+(i.getUTCMilliseconds()/1e3).toFixed(3).slice(2,5)+"Z",iKey:e,name:"Microsoft.ApplicationInsights."+e.replace(/-/g,"")+"."+t,sampleRate:100,tags:n,data:{baseData:{ver:2}},ver:4,seq:"1",aiDataContract:undefined}}var h=-1,v=0,y=["js.monitor.azure.com","js.cdn.applicationinsights.io","js.cdn.monitor.azure.com","js0.cdn.applicationinsights.io","js0.cdn.monitor.azure.com","js2.cdn.applicationinsights.io","js2.cdn.monitor.azure.com","az416426.vo.msecnd.net"],k=l.url||cfg.src;if(k){if((n=navigator)&&(~(n=(n.userAgent||"").toLowerCase()).indexOf("msie")||~n.indexOf("trident/"))&&~k.indexOf("ai.3")&&(k=k.replace(/(\/)(ai\.3\.)([^\d]*)$/,function(e,t,n){return t+"ai.2"+n})),!1!==cfg.cr)for(var e=0;e<y.length;e++)if(0<k.indexOf(y[e])){h=e;break}var i=function(e){var a,t,n,i,o,r,s,c,p,u;f.queue=[],g||(0<=h&&v+1<y.length?(a=(h+v+1)%y.length,T(k.replace(/^(.*\/\/)([\w\.]*)(\/.*)$/,function(e,t,n,i){return t+y[a]+i})),v+=1):(d=g=!0,o=k,c=(p=function(){var e,t={},n=l.connectionString;if(n)for(var i=n.split(";"),a=0;a<i.length;a++){var o=i[a].split("=");2===o.length&&(t[o[0][S]()]=o[1])}return t[b]||(e=(n=t.endpointsuffix)?t.location:null,t[b]="https://"+(e?e+".":"")+"dc."+(n||"services.visualstudio.com")),t}()).instrumentationkey||l.instrumentationKey||"",p=(p=p[b])?p+"/v2/track":l.endpointUrl,(u=[]).push((t="SDK LOAD Failure: Failed to load Application Insights SDK script (See stack for details)",n=o,r=p,(s=(i=m(c,"Exception")).data).baseType="ExceptionData",s.baseData.exceptions=[{typeName:"SDKLoadFailed",message:t.replace(/\./g,"-"),hasFullStack:!1,stack:t+"\nSnippet failed to load ["+n+"] -- Telemetry is disabled\nHelp Link: https://go.microsoft.com/fwlink/?linkid=2128109\nHost: "+(w&&w.pathname||"_unknown_")+"\nEndpoint: "+r,parsedStack:[]}],i)),u.push((s=o,t=p,(r=(n=m(c,"Message")).data).baseType="MessageData",(i=r.baseData).message='AI (Internal): 99 message:"'+("SDK LOAD Failure: Failed to load Application Insights SDK script (See stack for details) ("+s+")").replace(/\"/g,"")+'"',i.properties={endpoint:t},n)),o=u,c=p,JSON&&((r=C.fetch)&&!cfg.useXhr?r(c,{method:D,body:JSON.stringify(o),mode:"cors"}):XMLHttpRequest&&((s=new XMLHttpRequest).open(D,c),s.setRequestHeader("Content-type","application/json"),s.send(JSON.stringify(o))))))},a=function(e,t){g||setTimeout(function(){!t&&f.core||i()},500),d=!1},T=function(e){var n=x.createElement(I),e=(n.src=e,cfg[u]);return!e&&""!==e||"undefined"==n[u]||(n[u]=e),n.onload=a,n.onerror=i,n.onreadystatechange=function(e,t){"loaded"!==n.readyState&&"complete"!==n.readyState||a(0,t)},cfg.ld&&cfg.ld<0?x.getElementsByTagName("head")[0].appendChild(n):setTimeout(function(){x.getElementsByTagName(I)[0].parentNode.appendChild(n)},cfg.ld||0),n};T(k)}try{f.cookie=x.cookie}catch(p){}function t(e){for(;e.length;)!function(t){f[t]=function(){var e=arguments;d||f.queue.push(function(){f[t].apply(f,e)})}}(e.pop())}var r,s,n="track",o="TrackPage",c="TrackEvent",n=(t([n+"Event",n+"PageView",n+"Exception",n+"Trace",n+"DependencyData",n+"Metric",n+"PageViewPerformance","start"+o,"stop"+o,"start"+c,"stop"+c,"addTelemetryInitializer","setAuthenticatedUserContext","clearAuthenticatedUserContext","flush"]),f.SeverityLevel={Verbose:0,Information:1,Warning:2,Error:3,Critical:4},(l.extensionConfig||{}).ApplicationInsightsAnalytics||{});return!0!==l[E]&&!0!==n[E]&&(t(["_"+(r="onerror")]),s=C[r],C[r]=function(e,t,n,i,a){var o=s&&s(e,t,n,i,a);return!0!==o&&f["_"+r]({message:e,url:t,lineNumber:n,columnNumber:i,error:a,evt:C.event}),o},l.autoExceptionInstrumented=!0),f}(cfg.cfg),(C[n]=i).queue&&0===i.queue.length?(i.queue.push(e),i.trackPageView({})):e();})({
src: "https://js.monitor.azure.com/scripts/b/ai.3.gbl.min.js",
crossOrigin: "anonymous",
cfg: { // Application Insights Configuration
 connectionString: "InstrumentationKey=465feaf7-a327-475a-a48a-1afc759a1fda;IngestionEndpoint=https://eastus-8.in.applicationinsights.azure.com/;LiveEndpoint=https://eastus.livediagnostics.monitor.azure.com/"
}});
</script>


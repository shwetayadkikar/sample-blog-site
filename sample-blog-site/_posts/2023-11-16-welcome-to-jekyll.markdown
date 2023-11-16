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
      <button type="submit">Submit Comment</button>
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


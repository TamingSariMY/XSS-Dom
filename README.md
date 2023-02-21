# XSS-Dom

![image](https://user-images.githubusercontent.com/106005322/220373111-fcb5c313-ee7f-454d-a132-1bcbaf973de1.png)
#
## What is Dom-XSS?

#### DOM-based XSS is a cross-site scripting vulnerability that enables attackers to inject a malicious payload into a web page by manipulating the client’s browser environment. Since these attacks rely on the Document Object Model, they are orchestrated on the client-side after loading the page. In such attacks, the HTML source code and the response to the attack remain unchanged, so the malicious input is not included in the server response. Since the malicious payload is stored within the client’s browser environment, the attack cannot be detected using traditional traffic analysis tools.
#

![image](https://user-images.githubusercontent.com/106005322/220374014-4ea382d5-8c1a-4c10-ae67-9c960c45f54c.png)
#
## What is DOM?

#### The Document Object Model (DOM) is a programming interface that defines how to create, modify or erase elements in an HTML or XML document. DOM provides a standard API for the dynamic modification of the content, style, and structure of web page documents. A DOM model represents each element as a node within a tree-like system, enabling easier programmatic access and management of the elements.

#
#
## This is a Dom-XSS simulation that i did on DVWA(Damn Vulnerable Web Application) from low to high stages
#
#

## Low

![Screenshot (65)](https://user-images.githubusercontent.com/106005322/220376142-9cd47135-607f-4618-9933-1eb7088c99a5.png)
#### so first of all I will check the source code but it gives a notice that there is no protection

#

![Screenshot (63)](https://user-images.githubusercontent.com/106005322/220376286-821f1cc1-2134-465d-97e9-56ab1d5299cc.png)
#### on this xss dom we will play a lot on the url, so now I will choose English and when I click the submit button we will see the English value on the url

#

![Screenshot (64)](https://user-images.githubusercontent.com/106005322/220376394-40dec876-9e09-45bc-ac79-6e7f4d4cdec6.png)
#### so we can inject the payload by changing the value ```english``` to ```<script>alert('Taming')</script>```


#
#
## Medium

![Screenshot (76)](https://user-images.githubusercontent.com/106005322/220382437-bb660316-4337-495c-8085-288433f7e1ff.png)
#### if we look at the source code there is a tag ```if (stripos ($default, "<script") !== false)``` this code means we cannot inject a tag that has the word <script and the corresponding one will be false

#

![Screenshot (68)](https://user-images.githubusercontent.com/106005322/220379534-63ac62fb-4b53-49e1-a6c0-a6dda03194e7.png)
#### now I'm going to leave the select tag section, so now what I need to do is to put ```</select>``` which is the end of the select tag and also combine it with the payload in the form of html

#

![Screenshot (69)](https://user-images.githubusercontent.com/106005322/220379592-be01afab-7784-4268-add9-a2c7af7d92df.png)
#### and it will trigger xss on this page

#
#
## High

![Screenshot (72)](https://user-images.githubusercontent.com/106005322/220387259-b0011494-75f6-4663-9f17-38e98ec8aa08.png)
#### in this source code we are told that the only input that can be entered is from the option

#

![Screenshot (73)](https://user-images.githubusercontent.com/106005322/220387314-90850608-708d-413b-a7ab-feb91f4a7c6a.png)
#### so here I found that we can still inject the payload but it will not be sent to the server because we use ```#```

#

![Screenshot (74)](https://user-images.githubusercontent.com/106005322/220387641-b1be62cf-4236-4fef-b23e-cdab9009289c.png)
#### and it will trigger xss on this page

#

![Screenshot (75)](https://user-images.githubusercontent.com/106005322/220390765-4dd06cc1-0b9e-4c23-9aec-e6081e4cd63c.png)
#### but when I check on inspect it shows that the payload is only sent and seen on the client side

#

![Screenshot (77)](https://user-images.githubusercontent.com/106005322/220388992-eaf27604-9655-4ca3-b6d0-ff06d340953d.png)
#### and if we look at the request that has been made, it only sends the ```English``` value to the server and does not include the payload that was entered earlier

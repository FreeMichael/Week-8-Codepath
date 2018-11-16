# Week-8-Codepath
# Project 8 - Pentesting Live Targets

Time spent: **X** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1:

SQL Injection (SQLi): This vulnerability lies in the blue site not filtering SQL injections in the url
> blue/public/staff/salespeople/show.php?id=#
The SQL injection ' OR 1=1 --' is inserted where the id "#" is this returns these numerical values %27%20OR%201=1%20--%27 which should have been sanitized.

GIF Walkthrough:https://gfycat.com/RemorsefulTestyDragon


Vulnerability #2: 

Session Hijacking/Fixation: This vulnerability is exploited by using the session id gained from https://35.184.88.145/blue/public/staff/login.php to login to the green site without having credentials.

GIF Walkthrough:https://gfycat.com/TautBlankKarakul


## Green

Vulnerability #1:

Username Enumeration: This vulnerability is displayed when users are logging in. If the login username does not exist then the site will display "Login was Unsuccessful" in BOLD; whereas if the username does exist in the database then the text will not be bold. This allows attackers to see if usernames exist, which they can then try brute force attacks or other methods.

GIF Walkthrough:https://gfycat.com/DesertedMeekArchaeopteryx


Vulnerability #2:

Cross-Site Scripting (XSS): This XSS attack is directed at the contact page, where a non-user can input XSS by itself into the username and feedback field. This then causes the scripts to run on any user's computer who accesses the feedback page.

GIF Walkthrough:https://gfycat.com/WelllitCluelessHedgehog
``` Due to a student having a script run that redirects users to google I was unable to display my XSS```


## Red

Vulnerability #1:

Insecure Direct Object Reference (IDOR): This vulnerability lies in the URL 
> https://35.184.88.145/red/public/salesperson.php?id=1
where the user id is not sanitized, with this a user could change the "#" value after id= to access information about other sales staff that would usually be hidden such as:
``` Lazy Lazyman (FIRED FOR STEALING)
321-432-9876
lazyman@globitek.com```

GIF Walkthrough:https://gfycat.com/PoorGrimyDrake


Vulnerability #2: __________________


## Notes

On the final Red vulnerability (Cross-Site Request Forgery), I had trouble on creating a .php file. I will re-visit this.

##Concept Review

Which attacks were easiest to execute? Which were the most difficult?
>  The IDOR attack due to the URL being the first thing a user sees which the vulnerability lies.

What is a good rule of thumb which would prevent accidentally username enumeration vulnerabilities like the one created here?
>  Make sure there is no difference with error messages, such as the bold text issue found in this exploit.

Since you should be somewhat familiar with the CMS and how it was coded, can you think of another resource which could be made vulnerable to an Insecure Direct Object Reference? What code could be removed which would expose it? (Hint: It was also the answer to the first bonus objective to the Weekly Assignment for week 3.)
>  URL paths that are not encoded can be easily exploited by users trying common names for paths.

Many SQL Injections use OR as part of the injected code. (For example: ' OR 1=1 --'.) Could AND work just as well in place of OR? (For example: ' AND 1=1 --'.) Why or why not?
>  No, because if AND was used this would mean that the first value that the site gives must also being true, whereas OR allows the true statement ' OR 1=1 --' to work even if the first value does not.

A stored XSS attack requires patience because it could be stored for months before being triggered. Because of this, what important ingredient would an attacker most likely include in a stored XSS attack script?
...

Imagine that one of your classmates is an authorized admin for the site's CMS and you are not. How would you get them to visit the self-submitting, hidden form page you created in Objective #5 (CSRF)?
...

Compare session hijacking and session fixation. Which attack do you think is easier for an attacker to execute? Why? One of them is much easier to defend against than the other. Which one and why?
>  I feel session fixation would be easier because with session hijacking the attacker has to sniff traffic to see the session id which is usually hashed, this would be really hard to get the session id (especially if hash is salted). Whereas session fixation the attacker gets a session id and tricks a user into going to the site with that session id, which then allows the attacker to access the profile once the user logs in, since it is his session id.

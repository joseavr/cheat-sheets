# Application Automata
Automates the process to check for updates on internship applications. Also provides a nice way to store the information

## Possible Names
- TerpTracker
- InternTerp: terp and inter, easy to remember
- TerpVault: app secure to store all of ur internship app info, like a vault
- TerpEase: easy to manage internship applications
- TerpHub
- InternHub

## Inspiration

Are you tired of looking over the list of places/companies you've applied to and tired of searching thourugh each and every one every time you get an update? Don't you wish there was a more efficient way to store the information about all the applications you submitted and that you didn't have to log in to a different WorkDay page to check the status of each of your applications every once in a while just waiting for updates?

## What it does

I'm trying to automate the process of checking for updates on submitted internship applications. My program asks users for the basic input that it needs (such as the links for the submitted applications) and then it checks for updates for each individual application and updates the dataset entered by the user to reflect changes and updates after parsing the data from the website.

## How we built it

I used HTML/CSS/JavaScript to build the main page of the appplication where all the data is entered and stored. I used Selenium (it's a software that automates browsers) to get to the webpage/webpages entered by the user and I used BeautifulSoup to extract text from the webpage. I integrated Twilio into my code so that the user gets an SMS update each time something (i.e., the status of an application) gets updated. I connected it all to my back-end Python script that runs the Selenium and Twilio code when required.

## Challenges we ran into

There isn't any way for me to change anything on the webpages of my submitted internship applications that I could use for testing or for the demo. So I came up with a hardcoded solution. I created an HTML webpage that I can change for the purpose of the demo, but this simplifies the scraping/parsing process.

## Accomplishments that we're proud of

I'm proud that I was able to integrate different kinds of software into my project.

## What we learned

Learnt the basics of Selenium, Twilio and how to host my webpages on an Apache server.

## What's next for ApplicationTracker

I want to expand it to parse actual applications becuase this is a software that I would use. I also want to improve efficiency for large datasets since my current project does not really handle that. I want to connect it to a SQL based software to store data. In the user_input_form page that I have, I want to modify it using a different language so that users can modify what information they want to store (just like in excel or google sheets, but there would still be some required fields for the functionality of my code).

## Built With
-   [apache](https://devpost.com/software/built-with/apache)
-   [css](https://devpost.com/software/built-with/css)
-   [html](https://devpost.com/software/built-with/html)
-   [javascript](https://devpost.com/software/built-with/javascript)
-   [python](https://devpost.com/software/built-with/python)
-   [selenium](https://devpost.com/software/built-with/selenium)
-   [twilio](https://devpost.com/software/built-with/twilio)

## Try it out

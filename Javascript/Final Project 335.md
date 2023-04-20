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

We are trying to automate the process of checking for updates on submitted internship applications. The program asks users for the basic input that it needs (such as the links for the submitted applications) and then it checks for updates for each individual application and updates the dataset entered by the user to reflect changes and updates after parsing the data from the website.

## How we built it

We used HTML/CSS/JavaScript to build the main page of the appplication where all the data is entered and stored. We used Selenium (it's a software that automates browsers) to get to the webpage/webpages entered by the user and we used BeautifulSoup to extract text from the webpage. We integrated Twilio into our code so that the user gets an SMS update each time something (i.e., the status of an application) gets updated. We connected it all to the back-end Python script that runs the Selenium and Twilio code when required.

## Challenges we ran into

Optmizing the parsing process and creating the UI/UX for the website proved to be challenging.

## Accomplishments that we're proud of

We're proud that we were able to integrate different kinds of software into our project.

## What we learned

Learnt the basics of Selenium, Twilio and how to host webpages on an Apache server.

## What's next for ApplicationTracker

We want to expand it to parse actual applications becuase this is a software that we would use. We also want to improve efficiency for large datasets since the current version does not really handle that. We also want to integrate it with other websites or make it a Google Chrome extension at some point.

## Built With
-   [apache](https://devpost.com/software/built-with/apache)
-   [css](https://devpost.com/software/built-with/css)
-   [html](https://devpost.com/software/built-with/html)
-   [javascript](https://devpost.com/software/built-with/javascript)
-   [python](https://devpost.com/software/built-with/python)
-   [selenium](https://devpost.com/software/built-with/selenium)
-   [twilio](https://devpost.com/software/built-with/twilio)


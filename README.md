
# **Randomize App Developer Manual**

## Introduction
Randomize is an application dedicated to generating random music recommendations for users to expand their musical horizons. It is a web application powered by HTML, Sequelize and Javascript. It is also formatted in CSS through the Bulma library. This report is intended to inform developers on how to maintain and expand on the application framework for the Randomize app developed by our team this semester.

A working instance of our application can be found on Heroku at this link: [https://group-3-sp21.herokuapp.com/](https://group-3-sp21.herokuapp.com/)

## Overview
Our application functions by pulling information from a mySQL database containing a list of the top 50 songs from Spotify. Our program utilizes an API created in Sequelize by our team to randomly select 10 songs from this database and place them in a randomized table at the user’s request. Our application was developed for use in most modern internet desktop browsers and is compatible with Chrome, Firefox, and Edge.

## Links
* [User Manual]() 
* [Developer Manual]()

# Developer Manual
## Getting Started
To begin working with Randomize, there are a few dependencies that must be installed to get the application working in a development environment. These include Node.js, Bulma, Sequelize, and VSCode.

## Dependencies

 - Node.js, 64-bit v.14 or higher (runtime environment to host the application, locally or on a server)
 - Bulma (CSS library for beautifying your HTML)
 - Postman (for API testing)
 - Sequelize (JS library for beautifying your HTML)
 - VSCode, for text editing and easy navigation through the repository
 
 To install Node.js, go to [https://nodejs.org/en/download/](https://nodejs.org/en/download/) and download the 64-bit version of v.14 or higher.
 
 To use Bulma, simply [link it in the header of your HTML pages](https://bulma.io/documentation/overview/start/). No installation is required.
 
## Installation

To install Randomize, clone the Github repository [here](https://github.com/kthrnv/Group3-Final-INST377SP2021) to a local location on your computer.

Next, open the repository in VSCode or the text editor of your choice.

In the VSCode terminal, type `npm install` and `npm start`. This will install any necessary Node.js modules into your repository and boot up your local server. Typically, this server can be accessed on [http://localhost:3000/](http://localhost:3000/) by default. This is where you will be accessing the application.

## Running The App

To run the application as if an end user were accessing it, navigate to the URL of your Node.js server ([http://localhost:3000/](http://localhost:3000/) by default) in the internet browser of your choice. If everything is working, you should see an interface that looks like this:

[insert image here]

Follow the instructions listed on the application homepage to help you get started generating playlists.


## Application Testing
The are no prewritten tests in the source repository, but you can use Cypress to run your own written tests.
1. Open two terminals and make sure you are in the main project directory
2. In the first terminal, run ```npm start```.
3. In the second terminal run ```npm test```.

## API Testing
Testing for this application’s API can be done through the use of Postman, an application that links to your locally-hosted API endpoints and performs a variety of tests using GET, POST, PUT, and DELETE commands to ensure that your API endpoints are functioning correctly. To test your API endpoints in Postman, follow these steps:
1.  Start your Node.js server in the Randomize repository terminal, if you have not already done so.
   
2.  In Postman, navigate to the “Overview” page and create a new workspace tab.
    
3.  In the URL bar within your new tab, paste the address of the server you are hosting your Randomize repository on. This should look something like “[http://localhost:3000/](http://localhost:3000/)”.
    
4.  To test a given api route, append the url with “/api/[insert route name]”. For example, if you wanted to view the songs endpoint of the api, you would use the url “[http://localhost:3000/api/songs](http://localhost:3000/api/songs)” in Postman. Try this with a variety of different request types to make sure that your API is functioning as intended.
    
5.  Analyze the data returned by Postman to ensure your endpoint is functioning properly. The HTTP response code displayed in the upper right hand corner of the results panel can be helpful in diagnosing problems with endpoint connections.
    
6.  If everything looks good, your endpoint is working!


## API Routes and Endpoints
The API created by our team utilized the Sequelize JS library to create a series of API routes and endpoints that provide the necessary data for the Randomize application to function. Here is a broad overview of the routes that exist within the Randomize application infrastructure, the endpoints that are enabled for each API route, and the functions they serve.

```/``` - This route is the default empty route when first accessing the API.
* GET - returns response ‘Welcome to the Spotify Top Charts API!'

```/playlists``` - This route contains 3 playlists: US Top 50, Global Top 50, and Podcast Charts. These playlists possess a playlist_id value and playlist_name value.
* GET - Returns data from Playlists table.
* DELETE - Removes the selected playlist from the Playlist table. If playlist_id value is greater than 3 (default out-of-the-box playlists cannot be deleted.

```/wholeUSchart``` - This route contains a comprehensive list of the top 50 songs in the US at the time of data collection. This endpoint combines data from multiple other endpoints to include data regarding the song name, artist name, and playlist ID it originates from.
* GET - Returns data from US Top 50 table with associated metadata added for each song from Artists and Songs tables.

```/wholeGlobalChart``` - This route contains a comprehensive list of the top 50 songs on the  
    global charts at the time of data collection. This endpoint combines data from multiple other endpoints to include data regarding the song name, artist name, and playlist ID it originates from.
* GET - Returns data from Global Top 50 table with associated metadata added for each song from Artists and Songs tables.

```/global``` - This route contains a more limited list of the top 50 songs in the world at the time of data collection. This endpoint lists the song’s rank, # of streams, playlist ID, song ID, and artist ID.
* GET - Returns data from the Global Top 50 table with no additional metadata.

```/albums``` - This route contains a more limited list of the top 50 songs in the world at the time of data collection. This endpoint lists the song’s rank, # of streams, playlist ID, song ID, and artist ID.
* GET - Returns all existing data from Albums table if table length is greater than 0.
* POST - Creates a new entry in the Albums table based on currentId value.
* PUT - Updates an existing entry in the Albums table based on currentId value.

```/songs``` - This route contains a list of all the songs contained in our database. It includes each song’s song id, name, artist id, and whether a song is explicit or not.
* GET - Returns all existing data from Songs table if table length is greater than 0.
* POST - Creates a new entry in the Songs table based on currentId value.
* PUT - Updates an existing entry in the Songs table.

```/artists``` - This route contains a list of all the songs contained in our database. It includes each song’s song id, name, artist id, and whether a song is explicit or not.
* GET - Returns data from Artists table if table length is greater than 0.
* POST - Creates a new entry in Artists table based on currentId value.
 * PUT - Updates an existing entry in Artists table.
 
```/userSongs``` - API route for data of only user-added songs.
* GET - Returns data from Songs table that are greater than song_id of 66 (song_id after 66 are songs not originally included in the database).
## Known Issues & Future Development
### Bugs:
* Application does not check whether a song is already in the database if a user adds a pre-existing song
* Application does not reformat user input to the style standards that were used to create the database
* Users cannot specify the artist of a song they are adding because Artists and Songs data are on two different tables within the database. Because of this complexity, only the song name and explicit values are requested (both part of Songs data) and are displayed in the generator table and user-added table.

### Future Development: 
* Continuing with the original plan and implementing custom playlists
* Cross-checking that user-added songs are real songs available on Spotify or Apple Music  
* Consistently updating the US and Global Top 50 charts to reflect the current songs
* A playlist organization system that allows the creation and modification of multiple playlists
* Features that allow users to influence or filter the type of music that is selected to build their random playlist
* An expanded song library that allows for a greater degree of diversity in the music selected to build a random playlist

# IMDme 

IMDme is a simple webapp created to help you organize and remember all those movies you've been meaning to watch.

#To Get Started

Assuming I set this up correctly, all you should have to do after you set up the database
is run the following command in your terminal to launch the app in your browser at localhost:3000

```bash
yarn start
```

Copy and paste this code to create your database. 

```bash
CREATE DATABASE imdmedata;
USE imdmedata;
CREATE TABLE `user` (id INTEGER PRIMARY KEY AUTO_INCREMENT);
ALTER TABLE `user` ADD email VARCHAR(255) NOT NULL UNIQUE;
ALTER TABLE `user` ADD password TEXT NOT NULL;

CREATE TABLE `watchlist`(
     wl_id INTEGER PRIMARY KEY AUTO_INCREMENT,
     wl_title TEXT NOT NULL,
     user_id INTEGER NOT NULL
      );

CREATE TABLE `movie` (
     movie_id INTEGER PRIMARY KEY AUTO_INCREMENT,
     movie_title TEXT NOT NULL,
     poster_address TEXT NOT NULL,
     parent_watchlist_id INTEGER NOT NULL
     );

ALTER TABLE watchlist
     ADD FOREIGN KEY(user_id) REFERENCES user(id) ON DELETE CASCADE;
ALTER TABLE movie
     ADD FOREIGN KEY(parent_watchlist_id) REFERENCES watchlist(wl_id) ON DELETE CASCADE;
``` 


# Structure
There are a few main parts to the repo. <br/>
The src file is basically just the react app, components, styling<br/>
The src file contains: <br/>
     - App.js which is the main app set up with a react router<br/>
     - index.css which just sets the background color for all the pages<br/>
     - index.js which just tells the app to run<br/>
     - sample.env with environment variables for the TMDB API key and mySQL password<br/>
    - components file which contains:<br/>
       - Dashboard with Dashboard.js, AddMovie.js, CreateWatchlist.js components<br/>
        -Home with Homepage.js component<br/>
        -login with login.js component<br/>
        -Signup with Signup.js component<br/>
It runs on an express server located in server.js that handles GET/POST requests<br/>
package.json contains all the dependencies and scripts<br/>


# Known Bugs
1) The regex to check for valid input for Watchlist titles and Movie search queries doesn't work. I'm working on it.
2) It doesn't handle the case where the movie doesn't exist very gracefully. It doesn't break, it's just not pretty.
    Basically it refuses to add it to SQL database, so on the frontend an image not found icon comes through, if you
    refresh the page though it goes away. So at least the bad movie isn't stored in the database!
3) Visual bug if the title of a movie is too long, it gets hidden under the next row of movies.

# Project Contributors
Just me

# The Future

Right now, the app is pretty barebones in terms of functionality. In the future, I'd like to set it up to be
a little more interactive, like Spotify. You should be able to share links to watchlists with friends as well
as click on icons to redirect to watching the movie on Netflix, Hulu, Amazon Prime etc. 




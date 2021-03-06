## CS:GO Game Predictor

Download all the .py files. 

(Note: download the .csv files if you don't want to scrape data yourself. The main data set, csgo_results.csv, has data from 200 pages)

#Usage

Once you have all the required files, run the project.py file. This will import any necessary modules and python files.
These instructions are also provided when running the program. 
To use call the "predict()" function using these values

predict(# of HLTV pages to scrape data from, Team 1 name, Team 2 name, Map to be Played)
  
If pages is set to 0, data will not be scraped and any previously scraped data will be used.
This program is designed to predict from the top 20 current teams (As Ranked by HLTV)\nand the maps in the current map pool.
To see a list of the teams, call the "teamNames()" function.
To see a list of maps, call the "mapNames()" function.
Team and Map names are case sensitive.

#Documentation
##Scraper.py
The functions of scraper.py can be used to scrape map and team data from the Counter Strike: Global Offensive Rating site hltv.org. all files made by these will be saved in the working directory.
###scrape_map_stats()
This function takes no arguments and creates a file named "map_data.csv" which contains data in the following order:
  - map win percentage
  - pistol round win percentage
  - round win percentage after getting first kill
  - round win percentage after receiving first death

###extractDataIntoCondensedList(match)
Takes a match scraped from hltv.org and gets match data and puts it in a CSV format to be used in scrape(). Match data has:
- Second team name
- First team name
- Winner of the game
- Second team score
- First team score
- map

###scrape(pages)
Scrape is the main function of the program and takes an integer as an argument for how many pages of recent matches the program will scrape. Scrape uses the library beautiful soup to get data from the website.

##decision_trees.py
These functions are taken directly taken from chapter 17 Gurus on making decision trees.

##project.py
The program starts by printing user instructions on how to use the predictor. 

###isTop20(input)
Takes a team name as a string and returns true if it is in the hard coded top 20.
###isMap(input)
Takes a map name as a string and returns true if it is one of the chosen maps.
###get_rating(input)
Takes a team name as a string and returns the rating from collected data.
###get_rank(input)
Takes a team name as a string and returns its hltv rank.
###get_kd(input)
Takes a team name as a string and returns the kill to death ratio from collected data.
###readCsv(fileName)
Takes a CSV file and returns a list of lists where each item is in a list, and those lists are items in the larger list.
###returnMapStats(t, m)
Takes a team name t and map nam m as strings and returns all map stats gathered by 'scrape_map_stats()' and returns a list of stats
###filterCSV()
creates a new CSV of data that filters out all games that include teams not in the top 20 or played on maps not in our group
###getVariables()
Prints out the variables used in making the decision tree.
###getDataReady()
Turns the collected data into the format needed to make the decsision tree made from the book. This means changing numbers into booleans. We set team one having the better stat as true. Then it builds a decision tree based off the data
###userInputStats(team1, team2, m)
Takes a team one team1, team two team2 and map m as strings and creates an input vector. This fake match will be match will be used to predict the outcome
###teamNames()
Prints the team names in order of hltv ranking
###mapNames()
Prints map names.
###accuracy()
Accuracy takes the scraped data and trains the model on a user inputted percentage of the data while testing it on the remaining data. Returns a percentage of games correctly predicted.
###predict(pages, team1, team2, m)
This is the main function of file. The function takes team one team1, team two team2 and map m as strings and pages as an int. If pages is 0, previously scraped data will be used, otherwise the program will scrape the ammount of pages of most recent data for matches played.The program will also reprompt you to enter an input vector if the input vector is not possible (map or one of the teams not from the specified pool). The function will make a prediction on what team will win given the input and print it to the console.

#Notes
This program is only designed to work with the current (at the time of writing) top 20 teams, as rated by HLTV
This allows us to make sure we have enough stats for these teams.
Hard coded variables include
- Team Rank (As determined by HLTV ranking system at the time of writing.)
- Team Id-(As seen in hltv url)
- KD-(Found on individual team stats page)
- Rating (This was calculated by averaging the player ratings of the current rosters for each of the top 20 teams)
- Hltv scraping is done using BeautifulSoup 4.
- This program makes use of the decision tree algorithm code written by Joel Grus

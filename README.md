# worldcup-database
World Cup Database Project
This project is a PostgreSQL-based database that stores the results of the last three rounds (Eighth-Finals, Quarter-Finals, Semi-Finals, Third Place, and Final) from the 2014 and 2018 World Cup tournaments. It includes tables for teams and games, along with several queries that summarize the tournament data.

Project Structure
The project contains the following important files:

games.csv: This file contains data for the World Cup matches, including the year, round, teams, and goals scored.
insert_data.sh: This bash script reads the data from the games.csv file and inserts the necessary data into the PostgreSQL database.
queries.sh: This bash script contains several queries that retrieve summarized data from the World Cup database, such as the total number of goals, unique teams, and more.
expected_output.txt: This file shows the expected output for the queries executed in queries.sh.
worldcup.sql: This file is a PostgreSQL dump that can be used to recreate the database, including the schema and the inserted data.
Database Structure
The database consists of two tables: teams and games.

1. teams Table
team_id SERIAL PRIMARY KEY: Unique identifier for each team.
name VARCHAR(255) UNIQUE NOT NULL: The name of the team.
2. games Table
game_id SERIAL PRIMARY KEY: Unique identifier for each game.
year INT NOT NULL: The year the game took place.
round VARCHAR(255) NOT NULL: The round of the World Cup (e.g., Quarter-Final, Semi-Final).
winner_id INT REFERENCES teams(team_id) NOT NULL: The ID of the winning team, references the team_id in the teams table.
opponent_id INT REFERENCES teams(team_id) NOT NULL: The ID of the opponent team, references the team_id in the teams table.
winner_goals INT NOT NULL: The number of goals scored by the winning team.
opponent_goals INT NOT NULL: The number of goals scored by the opponent.
Setup and Execution Instructions
1. Requirements
PostgreSQL
Bash terminal
Basic understanding of psql (PostgreSQL CLI)
2. Create the Database
First, log in to the PostgreSQL interactive terminal:

bash
Copy code
psql -U postgres
Create the worldcup database:

sql
Copy code
CREATE DATABASE worldcup;
Connect to the worldcup database:

sql
Copy code
\c worldcup
Create the teams and games tables by running the SQL queries inside the psql terminal (or they will be created automatically when the insert_data.sh script is run).

3. Insert Data
Ensure the insert_data.sh file has the correct permissions by running:

bash
Copy code
chmod +x insert_data.sh
Run the insert_data.sh script to insert the data from games.csv into the database:

bash
Copy code
./insert_data.sh
This script reads the data from the games.csv file and populates the teams and games tables in the worldcup database. It checks for unique teams and avoids duplicates.

4. Run Queries
Ensure the queries.sh file has the correct permissions by running:

bash
Copy code
chmod +x queries.sh
Execute the queries.sh script to run the predefined queries and retrieve the required data:

bash
Copy code
./queries.sh
This script will return results such as:

Total number of goals in all games.
The winner of the 2018 World Cup.
List of teams that participated in the 2014 Eighth-Final round.
Most goals scored by a team in a single game, and more.
5. Export the Database
If you want to create a backup of the database (including its schema and data), run the following command:

bash
Copy code
pg_dump -cC --inserts -U postgres worldcup > worldcup.sql
This will create a file named worldcup.sql that contains all the commands needed to recreate the database.

6. Rebuild the Database
If you want to rebuild the database using the worldcup.sql dump file:

First, ensure you are in the directory where the worldcup.sql file is located.
Run the following command to restore the database:
bash
Copy code
psql -U postgres < worldcup.sql
This will recreate the worldcup database with all the data.

Queries Description
The queries.sh script contains the following queries:

Total number of goals in all games from winning teams: Summarizes all goals scored by winning teams across all rounds.

Total number of goals in all games from both teams combined: Sums the goals of both the winning and opponent teams across all games.

Average number of goals by winning teams: Calculates the average number of goals scored by winning teams in all games.

Average number of goals by winning teams rounded to two decimal places: Calculates and rounds the average goals of winning teams to two decimal places.

Average number of goals scored by both teams: Computes the average goals scored by both the winning and opponent teams.

Most goals scored in a single game by one team: Retrieves the highest number of goals scored by a single team in any game.

Number of games where the winning team scored more than two goals: Counts how many games had a winning team that scored more than two goals.

Winner of the 2018 tournament: Displays the team that won the 2018 World Cup.

Teams who played in the 2014 Eighth-Final round: Lists all the teams that played in the 2014 Eighth-Final round.

List of unique winning team names: Displays all the unique teams that have won a game.

Year and team name of all champions: Shows the year and team name of the champions in the Final round for each World Cup.

List of teams that start with 'Co': Lists all teams whose names start with "Co".

Expected Output
The expected output of the queries.sh script can be found in the expected_output.txt file, which shows the correct answers for each query.

License
This project is a requirement to earn freeCodeCamp certification as a backend developer. 

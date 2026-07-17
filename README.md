# World Cup 2026 Data Model Documentation

## Overview

This project uses **CSV files only** as the data source. No SQL database
is used.

## Folder Categories

-   Dimensions
-   Facts
-   Bridge Tables
-   Player Statistics
-   Team Statistics

# Dimensions

## dim_teams.csv

Purpose: One row per national team.

Columns: - team_id (PK) - fifa_code - team_name - group_name -
confederation - continent - flag_url

## dim_players.csv

Purpose: One row per player.

Columns: - player_id (PK) - team_id (FK -\> dim_teams) - team_name -
player_name - position - club_name - club_country - birth_date -
photo_url - flag_url

## dim_coaches.csv

Purpose: One row per coach.

Columns: - coach_id (PK) - team_id (FK) - team_name - coach_name -
coach_nationality - birth_date - age - photo_url - flag_url

## dim_stadiums.csv

Purpose: One row per stadium.

Columns: - stadium_id (PK) - stadium_name - city - country_code -
capacity - time_zone - coordinates

# Facts

## fact_matches.csv

Purpose: One row per match.

Columns: - match_id (PK) - round - is_knocked - match_date -
match_time - group_name - team1_id - team2_id - city - stadium_id -
home_score_ft - away_score_ft - home_score_ht - away_score_ht -
is_played

# Bridge Tables

## bridge_goals.csv

Purpose: One row per goal scored.

Columns: - goal_id (PK) - match_id - player_id - team_id -
scored_team_id - minute - minute_numeric - is_own_goal - is_penalty

# Player Statistics

Each file contains one row per player.

-   attacking.csv --- Attacking metrics (assists, shots, xG, conversion
    rate, corners)
-   defending.csv --- Defensive metrics
-   discipline.csv --- Fouls, cards, offsides
-   distribution.csv --- Passing & distribution
-   goalkeeping.csv --- Goalkeeper metrics
-   physical.csv --- Physical metrics
-   golden_boot.csv --- Goals, assists, minutes played

# Team Statistics

Each file contains one row per team.

-   team_attacking.csv
-   team_defending.csv
-   team_discipline.csv
-   team_distribution.csv
-   team_goalkeeping.csv
-   team_movement.csv
-   team_physical.csv

# Relationships

    dim_teams
    ├── dim_players
    ├── dim_coaches
    ├── fact_matches
    └── bridge_goals

    dim_stadiums
    └── fact_matches

    Player statistics -> player_id
    Team statistics -> team_id

# Notes

-   Database: None
-   Source: CSV files only
-   Relationships use IDs only.
-   CSV files are updated by the data pipeline and deployed with the
    application.

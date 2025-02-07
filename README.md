# Predict_MLB_Hits
* Predicting batted ball outcomes using Statcast's new swing data

#### Project Status: Still Tinkering


## Overview
The hope of this notebook is to build a model to predict batted ball outcomes using Statcast's new swing data as well as pitch metrics, and other situational data. This project is inspired by Nick Wan's kaggle contest (https://www.kaggle.com/competitions/nwds-batted-balls/overview). During th 2024 season, MLB was able to start tracking swing speed and length, and the contest was designed to explore the interaction between the two new swing metrics within a baseball context. The goal is to predict batted ball outcomes and to evaluate the model's success using AUC. 

## Dataset
This dataset includes only batted balls in play and home runs from the beginning of the 2024 season up to the All-Star game. From Nick Wan's contest:

*The data comes from MLB Statcast via Baseball Savant. Please reference the Baseball Savant Statcast Search CSV documentation for a data dictionary:*
https://baseballsavant.mlb.com/csv-docs

*Some columns are unique to this competition. These are:*

* uid: a unique ID for each row in the dataset
* is_lhp: whether a pitcher throws with their left hand
* is_lhb: whether a batter hits with a left-handed stance
* spray_angle: calculated via pybaseball and is described as

 > *Spray angle is the raw left-right angle of the hit - Adjusted spray angle flips the sign for left handed batters, making it a push/pull angle. Inspired by this Alan Nathan post (https://baseball.physics.illinois.edu/carry-v2.pdf). The formula to transform hit coordinates to spray angle used was obtained from this blog post (https://baseballwithr.wordpress.com/2018/01/15/chance-of-hit-as-function-of-launch-angle-exit-velocity-and-spray-angle/).*

* outcome: the result of the batted ball; can be 'out', 'single', 'double', 'triple', or 'home_run'
* outcome_code: for convenience and clarity, the outcome column is represented with integers where 0='out', 1='single', 2='double', 3='triple', and 4='home_run'.

## Process
* Data Source: Used "batted_balls.csv" which consists of 50000 events and 41 features
* Removed non-competitative swings (bunts, check swings etc.) from the dataset
* Feature engineered 51 additional metrics
* Used Optuna to tune an XGBoost model to predict hits

## Results
* Through several runs, .737 was the best AUC score obtained. This would be middle of the pack for the contest submissions. There were two excellent submissions with scores above .95 while most submissions were in the .71-.75 range. I hope to continue to improve the model's performance

# coding-hsg-group-2305
Project for the course 'Programming with Advanced Computer Languages' in FS21.

**Group ID**: 2305

**Group members**: Noel Ackermann (Username: Noicel)

**Project name**: Predicting Football Games With a Poisson Model

**Description**: Based on my bachelor thesis. The user should be able to select a league and the program should return value bets based on outcome probabilities estimated with a pre-defined model.

The project can be executed by calling one function ('league_bets') and specifying one parameter, the maximum odds of the value bets that will be presented. The code is presented using Jupyter Notebook.

Example:
```
league_bets(2.5)
```

With user inputs 'Ecuador' and 'Liga Pro', the output looks as follows:
```
Enter a country.
Ecuador
Select a league: Liga Pro.
Liga Pro
----------------------------------------------
21-05-30 20:30
Macara - Aucas
Bet: Macara over 2.3
Estimated probability: 43.47%
----------------------------------------------
21-05-31 02:00
U. Catolica - Barcelona SC
Bet: Barcelona SC over 2.02
Estimated probability: 49.5%
```

The function 'league_bets' depends on other functions. The rough structure of the approach is:
1. Let the user select a league using function 'select_url'. First, the user selects a country, then, the website [Betexplorer](https://www.betexplorer.com) is checked for leagues in this country with upcoming matches, and, if such leagues exist, it lets the user select one of those leagues. All data (results, games, betting odds used here come from Betexplorer.
2. If the user selected a valid league, it is searched for upcoming games with the function 'find_games'.
3. In a next step, the function 'get_results' searches for past results of this league.
4. After checking whether enough games have been played for the model to work, the function 'r_calc' applies a Poisson model discussed in my bachelor thesis (referred to as Dixon & Coles with tau). For members of the University of St.Gallen, the thesis should be available [here](https://universitaetstgallen.sharepoint.com/sites/EDOCDB/edocDocsPublished/16604001101.pdf). The only change made to the procedure is that for this project, only results of the current season are used to make predictions. This has the obvious disadvantage that no predictions can be made at the beginning of the season. The function 'r_calc' reuses parts of R code of the thesis that estimate model parameters.
5. After estimating the model parameters, probabilities for home and away wins can be estimated by using the function 'res_prob', which depends on the functions 'respois', 'μ', and 'λ', applying the estimated parameters.
6. Finally, value bets are printed if the estimated odds are below the user's specified maximum odds. Value bets are defined here as the odds of the bookmaker being higher than the odds corresponding to a team's estimated win probabilities.

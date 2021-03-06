# This is a package to get NBA stats from scraping yahoo.com

There are 2 main classes in this package
* DataAttribute
* Player
* Team

## DataAttribute
* this is the return value from most of the Player methods
* Attributes:
  * names: list = field(default_factory=list)
  * num_game: int = 1
  * fg_made: float = 0.0
  * fg_attempt: float = 0.0
  * three_made: float = 0.0
  * three_attempt: float = 0.0
  * ft_made: float = 0.0
  * ft_attempt: float = 0.0
  * rebound: float = 0.0
  * assist: float = 0.0
  * turnover: float = 0.0
  * steal: float = 0.0
  * block: float = 0.0
  * point: float = 0.0

## Player
* Attributes:
  * name (string):                              player's full name
  * player_id (int):                            player 4 digit id
  * game_raw_data (BeautifulSoup object):       internal data for processing
  * yearly_raw_data (BeautifulSoup object):     internal data for processing
  * team (string):                              player's team
  * number (int):                               player's number
  * avg_pt (float):                             average point for current season
  * avg_reb (float):                            average rebound for current season
  * avg_ast (float):                            average assist for current season
  * position (string):                          position
  * college (string):                           college the player attended

* Methods:
  * get_yearly_data(self, year='current')
    * return the yearly average represented by DataAttribute dataclass
	* required parameters:
	  * year (int): a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year

  * get_recent_games_data(self, game_type='all', home_only=False, away_only=False, games=5, year='current')
    * return a list of DataAttribute objects
	* required parameters:
	  * game_type (string): accepted types are all, reg, or post, default=all
      * home_only (bool):   home game only, default=False
      * away_only (bool):   away game only, default=False
      * games (int):        the number of games, default=5
      * year (int):         a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year. default=current

  * get_recent_games_avg_stats(self, game_type='all', home_only=False, away_only=False, games=5, year='current')
    * return a list of DataAttribute objects
	* required parameters:
	  * game_type (string): accepted types are all, reg, or post, default=all
      * home_only (bool):   home game only, default=False
      * away_only (bool):   away game only, default=False
      * games (int):        the number of games, default=5
      * year (int):         a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year. default=current

  * get_data_by_opponentt(self, oppo, game_type='all', year='current')
    * return a list of DataAttribute objects
	* required parameters:
	  * game_type (string): accepted types are all, reg, or post, default=all
      * home_only (bool):   home game only, default=False
      * away_only (bool):   away game only, default=False
      * games (int):        the number of games, default=5
      * year (int):         a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year. default=current

  * get_avg_stats_by_opponent(self, oppo, game_type='all', year='current')
    * return the average stats against a particular opponent represented by DataAttribute dataclass
	* required parameters:
	  * oppo (string):      the 3 charater team name, eg, "BKN"
      * game_type (string): accepted types are all, reg, or post, default=all
      * year (int):         a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year. default=current

  * clear_cache(self)
    * clear caches
	* requred parameters:
	  * None
## Team
* Attributes:
  * name (string):                      team name
  * win (int):                          number of wins for current season
  * loss (int):                         number of loss for current season
  * pt (float):                         average point
  * reb (float):                        average rebound
  * fg (float):                         average fild goal percentage
  * percent_3pt (float):                average 3 point percentage
  * standing (string):                  team standing
  * raw_data (BeautifulSoup object):    internal data for processing
  * players (list[Player]):             list of player objects

## Example
* ```
  from nba_stats import nba_stats
  player = nba_stats.Player('Stephen Curry')
  player.get_yearly_data()
  DataAttribute(names=['2020-21'], num_game='4', fg_made=8.3, fg_attempt=20.0, three_made=3.5, three_attempt=11.0, ft_made=6.5, ft_attempt=6.5, rebound=3.8, assist=7.0, turnover=4.3, steal=1.8, block=0.5, point=26.5)
  player.get_avg_stats_by_opponent('CLE', year=2019)
  DataAttribute(names=['@CLE'], num_game=1, fg_made=6.0, fg_attempt=14.0, three_made=1.0, three_attempt=3.0, ft_made=1.0, ft_attempt=2.0, rebound=6.0, assist=5.0, turnover=2.0, steal=0.0, block=0.0, point=14.0)

  team = nba_stats.Team('Golden State Warriors')
  team.pt
  111.0
  team.win
  2

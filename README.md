# This is a package to get NBA stats from scraping yahoo.com

There are 2 main classes in this package
* Player
* Team

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
	* required argument:
	  * year (int): a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year

  * get_recent_games_data(self, game_type='all', home_only=False, away_only=False, games=5, year='current')
    * return a list of DataAttribute objects
	* required parameters:
	  * game_type (string): accepted types are all, reg, or post, default=all
      * home_only (bool):   home game only, default=False
      * away_only (bool):   away game only, default=False
      * games (int):        the number of games, default=5
      * year (int):         a 4 digit formatted year, eg, 2019. If it's "current", it'll get the current year. default=current

# The 'tyrone_mings' Package

The transfermarkt website is an amazing resource, there is an abundance of information on clubs, leagues and players. However, there is no API so collating the information can involve a lot of cut and pasting.

The tyrone_mings package aims to help people access the information with relative ease to help with analysis and understanding of the world of football. It's named after England footballer Tyrone Mings as an ode to his charity work and constant willingness to speak up on issues of racism and inequality.

I will be adding new functions as and when I write them. This is a package built out of a frustration that I have lots of snippets of code dotted around and wanted a home for my existing stuff as well as new stuff I write.

### Leagues
Each league has a base page i.e. https://www.transfermarkt.com/premier-league/startseite/wettbewerb/GB1. By default the base page contains info about the current season but can be adjusted to show any previous season. The following functions help access information from these pages.

#### get_club_urls_from_league_page()
Takes a league's base page and returns a list of urls for each club's base page for that season.

```
club_urls = get_club_urls_from_league_page("https://www.transfermarkt.com/premier-league/startseite/wettbewerb/GB1")
```

#### get_player_urls_from_league_page()
Takes a league's base page and returns a list of urls for each player's base page from all clubs. To track progress add verbose = True to print the name of each club once their players are added.

```
player_urls = get_player_urls_from_league_page("https://www.transfermarkt.com/premier-league/startseite/wettbewerb/GB1", verbose = True)
```

### Clubs
Each club has a base page i.e. https://www.transfermarkt.com/aston-villa/startseite/verein/405. By default the base page contains info about the current season but can be adjusted to show any previous season. The following functions help access information from these pages.

#### get_player_urls_from_club_page()
Takes a club's base page and returns a list of urls for each player's base page.

```
player_urls = get_player_urls_from_club_page("https://www.transfermarkt.com/manchester-united/startseite/verein/985/saison_id/2019")
```

### Players
Each player has a base profile page i.e. https://www.transfermarkt.com/tyrone-mings/profil/spieler/253677. However, there are a multitude of other pages covering information such as performance data, national team data etc. The pull_tm function help access information from these pages. Getting all of this information per player can take about 7s, so the user has the option to select which information should be collected.

##### Output
The user can chose to write the returning information to csv or to a pandas dataframe via output = "csv" or output = "pandas" respectively.

##### Player Bio
Player Bio collects the player id, player name,	day of birth,	month of birth,	year of birth, place of birth, country of birth, other citizenship, playing position, height and preferred foot. This are mostly static information about the player.

```
player_page = "https://www.transfermarkt.com/tyrone-mings/profil/spieler/253677"
bio = tm_pull(player_page, player_bio = True, output = 'pandas')
print(bio)
```

##### Player Status
Player Status collects the player id, current club, country of current club, current market value,	date joined current club, contract expiry date, contract option, loaning club,	country of loaning club, loan expiry date and players' agent. This are mostly static information about the player.
```
player_page = "https://www.transfermarkt.com/tyrone-mings/profil/spieler/253677"
status = tm_pull(player_page, player_status = True, output = 'pandas')
print(status)
```

##### Transfer History
Transfer History collects the player id, club transferred from, club transferred to, market value,	transfer fee paid, transfer date, season of season, country transferred to,	country transferred from, type of	transfer,	in-club or between-clubs transfer, player age at point of transfer and all youth clubs.
```
player_page = "https://www.transfermarkt.com/tyrone-mings/profil/spieler/253677"
transfer_data = tm_pull(player_page, transfer_history = True, output = 'pandas')
print(transfer_data)
```

##### Performance History
Performance History collects, for each competition and season, the player id, season , competition, competition, code, club, in squad, appearances, ppg, goals, assists, subbed on, subbed off, yellow card, second yellow card, red card, penalties, mins_played, clean sheets, goals conceded and age at the start of the season.
```
player_page = "https://www.transfermarkt.com/tyrone-mings/profil/spieler/253677"
performance_data = tm_pull(player_page, performance_history = True, output = 'pandas')
print(performance_data)
```

##### Market Value History
Tranfermarkt calculate a market value for each player in the world which is updated 1-3 times a year. Market Value History collects the player id, club,	market value,	date of calculation and the player's age at point of calculation.
```
player_page = "https://www.transfermarkt.com/tyrone-mings/profil/spieler/253677"
market_value_data = tm_pull(player_page, market_value_history = True, output = 'pandas')
print(market_value_data)
```

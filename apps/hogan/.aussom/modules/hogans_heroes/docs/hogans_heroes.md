# file: hogans_heroes.aus

## class: hogans_heroes

[24:14] `static` **extends: object** 

Trivia archive for the CBS sitcom Hogan's Heroes (1965-1971).
Holds show metadata, cast/character data, famous quotes, cast
real-life trivia, production notes, and assorted fun facts as
private member variables. Access each set through its getter.

#### Members
- **show**

	> Top-level facts about the show itself: title, network, air dates, episode and season counts, setting, studio, and premise.

- **themeSong**

	> Credits and trivia for the show's theme music, the Hogan's Heroes March by Jerry Fielding.

- **characters**

	> Principal and recurring characters together with the actors who played them, their ranks, nationalities, and their role in the series.

- **quotes**

	> Memorable lines pulled from the series, each tagged with the speaker.

- **castRealLifeTrivia**

	> Real-life facts about the cast.

- **productionTrivia**

	> Production-side trivia: creators, network, awards, set details, and post-show history.

- **funFacts**

	> Lighter in-universe and behind-the-scenes oddities that don't fit the production-trivia bucket.


#### Methods

- **getShow** ()

	> Returns top-level facts about the show: title, network, dates, episode/season counts, setting, studio, and premise.

	- **@r** `A` map of show-level metadata.


- **getThemeSong** ()

	> Returns credits and trivia for the show's theme music.

	- **@r** `A` map describing the Hogan's Heroes March.


- **getCharacters** ()

	> Returns the principal and recurring characters together with the actors who played them.

	- **@r** `A` list of character maps.


- **getQuotes** ()

	> Returns memorable quotes from the series, each tagged with the speaker.

	- **@r** `A` list of quote maps with "speaker" and "quote" keys.


- **getCastRealLifeTrivia** ()

	> Returns real-life facts about the cast.

	- **@r** `A` list of trivia strings.


- **getProductionTrivia** ()

	> Returns production-side trivia: creators, network, awards, sets, and post-show history.

	- **@r** `A` list of trivia strings.


- **getFunFacts** ()

	> Returns lighter in-universe and behind-the-scenes oddities.

	- **@r** `A` list of trivia strings.





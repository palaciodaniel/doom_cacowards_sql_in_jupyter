[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/palaciodaniel/doom_cacowards_sql_in_jupyter/master?filepath=cacowards_sql_querying_on_jupyter.ipynb)

# Doom's Cacowards SQL - A database queried with Jupyter Notebook

_By Daniel Palacio - August 2020._

## 0. INDEX

**1. [INTRODUCTION](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#1-introduction)**</br>
1.1. [About](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#11-about)</br>
1.2. [Useful Links](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#12-useful-links)</br>

**2. [IMPORTANT INFORMATION ABOUT THE DATABASE](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#2-important-information-about-the-database)**</br>
2.1. [WADs](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#21-wads)</br>
2.2. [WAD Additional Features](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#22-wad-additional-features)</br>
2.3. [WAD Authors](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#23-wad-authors)</br>

**3. [HOW TO QUERY THE DATABASE](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#3-how-to-query-the-database)**

**4. [GLOSSARY](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#4-glossary-in-alphabetical-order)**

**5. [CREDITS](https://github.com/palaciodaniel/doom_cacowards_sql_in_jupyter/blob/master/README.md#5-credits)**

---
## 1. INTRODUCTION

### 1.1. ABOUT

The following project was started with several objectives in mind, that can be summarized like this:

* I. To gain experience in building from scratch a somewhat complex SQL database.
* II. To have a good showcase application for the "ipython-sql" package, which allows to easily query SQL databases in Jupyter Notebook.
* III. To get a comprehensive but at the same time accessible list to check all the available levels from this annual ceremony.
* IV. To eventually keep updating the database with more information.
* V. To have an opportunity to practice writing several pages of documentation in an organized and tidy way (with the added challenge that I'm not a native English speaking person).

For all these reasons, I chose as a subject the Cacoward Awards, which celebrates the best user-made creations for the -still- immensely popular FPS _Doom_ franchise. 

### 1.2. USEFUL LINKS

If you feel confused about what it is all actually about, you can check the following links before continuing to the next section; and if you still have some doubts, you will find a detailed glossary on Section 2.

**CACOWARDS PER YEAR:** [2004](https://www.doomworld.com/11years/) - [2005](https://www.doomworld.com/12years/) - [2006](https://www.doomworld.com/13years/) - [2007](https://www.doomworld.com/14years/) - [2008](https://www.doomworld.com/15years/) - [2009](https://www.doomworld.com/16years/) - [2010](https://www.doomworld.com/17years/) - [2011](https://www.doomworld.com/18years/) - [2012](https://www.doomworld.com/19years/) - [2013](https://www.doomworld.com/20years/) - [2014](https://www.doomworld.com/21years/) - [2015](https://www.doomworld.com/22years/) - [2016](https://www.doomworld.com/23years/) - [2017](https://www.doomworld.com/24years/) - [2018](https://www.doomworld.com/cacowards/2018/) - [2019](https://www.doomworld.com/cacowards/2019/)

**GETTING THE REQUIRED GAMES:**

If you want the whole _Doom_ franchise, you can check the following [link](https://store.steampowered.com/bundle/15366/DOOM_Franchise_Bundle/).
If you only want the games to specifically run the Cacoward entries, you have the following options:

- **Bundles (recommended):** 

[Doom Classic Complete](https://store.steampowered.com/sub/18397/) **AND** [Heretic + HeXen Collection](https://store.steampowered.com/sub/439/).

Note that you will still need to buy _Strife_ individually.

- **Individual titles:**

| Title | GOG (DRM-Free) | Steam |
|:-----:|:--------------:|:-----:|
| _DOOM_ | [YES](https://www.gog.com/game/the_ultimate_doom) | [YES](https://store.steampowered.com/app/2280/Ultimate_Doom/) |
| _DOOM II_ | [YES](https://www.gog.com/game/doom_ii_final_doom) | [YES](https://store.steampowered.com/app/2300/DOOM_II/) |
| _Heretic_ | NO | [YES](https://store.steampowered.com/app/2390/Heretic_Shadow_of_the_Serpent_Riders/) |
| _Hexen_ | NO | [YES](https://store.steampowered.com/app/2360/HeXen_Beyond_Heretic/) |
| _Strife_ | [YES](https://www.gog.com/game/strife_veteran_edition) | [YES](https://store.steampowered.com/app/317040/The_Original_Strife_Veteran_Edition/) |

**OTHER USEFUL LINKS:** 
- [Doom Wiki's Cacoward page](https://doomwiki.org/wiki/Cacowards) 
- [/idgames/ archive](https://www.doomworld.com/idgames/) 
- [GZDoom](https://www.zdoom.org/index) - The source port I personally use, though there are other options with the same quality, so I encourage you to research them before choosing one. The full list of available source ports can be consulted [here](https://doomwiki.org/wiki/Source_port#List_of_source_ports).

## 2. IMPORTANT INFORMATION ABOUT THE DATABASE

The following is a detailed description about how the data was organized and the reasons behind those decisions. Before querying the database it is strongly recommended to read it in its entirety to avoid potential confusions. And as expressed before, if there is a term that you don't know or don't fully understand, there is a glossary where most likely it will be explained.

* The database is all about the Cacoward Winners. Other categories, like "Runner Ups", weren't included. Also, since Cacowards were introduced on 2004, the Winners from the previous ten years weren't included either.

* Regarding ambitious WADS, the database is also about all the people that were part of those projects. Not only level designers, but also people who made new graphics or music, beta tested or gave significant feedback for the WADs were included as well. Since the [Doom Wiki](https://doomwiki.org/wiki/Entryway) already does a good job in indicating the level's authors on every WAD, the database aims to answer the simple question _"Was this person somehow involved with this project or not?"_. So, for instance, if [John Romero](https://twitter.com/romero) gave a lot of advice for a certain WAD, it will count as TRUE even if he didn't contribute a level for it.

* The database was built primarily from information present on the .txt files for every WAD's [/idgames/ archive](https://www.doomworld.com/idgames/) page. A complementary source of data was the [Doom Wiki](https://doomwiki.org/wiki/Entryway) (specially for Author's information). In some cases, the WADs have official pages where everything was already organized there. Failure to get information from these three sources are the reasons for 95% of NULL fields on this database; the remaining 5% was due to ambiguous or contradictory information (i.e.: a WAD described as Single Player on the /idgames description, but with Deathmatch support only on the .txt file).

* In order to be mentioned as part of a project, it is required that the person actively contributed to it. So, for instance, if one person wrote a song for a specific WAD, and that song is used for another one a few years later, this person won't be counted as an active contributor for this second project. Unfortunately, the majority of WADs aren't clear on this aspect, so on some ambiguous cases some people weren't mentioned to avoid confusions; it would be easier to add them later than to having to remove them from that field.

* In the event that a WAD (no matter its scale) was made by no more than two or three people, only those people will be mentioned. For instance, _"Sunlust"_ only has its two authors mentioned; other contributors weren't mentioned at all.

* There might be potential features to be further included: most importantly, the specific contribution that a person made for a project (i.e.: as a beta-tester, musician, level designer, etc), the inclusion of more real names or e-mail addresses, along with nationalities, and the mention of beta-testers or other contributors for projects made by one or two people. As of the moment of writing this document, the _Doom_ Community isn't aware of the existence of this database, and further completion will depend on their interest once they're eventually contacted. 

### 2.1. WADS

* A lot of wads (specially the most recent ones) will require a [source port]((https://doomwiki.org/wiki/Source_port#List_of_source_ports)). The database doesn't indicate which ones run with the original _Doom_ engine and which ones require one of these advanced ports. It isn't necessary to detail this requirement, since the safest option is to always use a source port.

* If a wad has Roman numbers (i.e.: _"Deus Vult II"_), for queries it is required to use normal numbers instead (i.e.: _"Deus Vult 2"_). 

* If you don't need an IWAD to run a wad, it will appear as "(STANDALONE)".

* If a new level only serves as a HUB it won't be counted. So, for example, a wad with 9 levels and 2 hub levels will appear as having 9 levels on its column.

* Regarding Multiplayer modes and Skill Levels support, if in the .txt file on the [/idgames/ archive](https://www.doomworld.com/idgames/) it only says _"Not Tested"_, _"Not effectively"_, _"Start Only"_, _"Maybe"_, or something like that, they will be considered FALSE. It is extremely unlikely that untested features are suitable for playing, so the most sensible option was to classify them as FALSE.

* If a project won a Cacoward on a certain year, but then it was later patched, the Size and URL columns will reflect these changes.

#### Special cases:
  - Even though both levels from _"Monster Hunter Ltd"_ are taken as a single Cacoward entry, for practical reasons they were divided in two entries for this database.
  - _"The Adventure of Square"_ won a Cacoward for its first episode and then a few years later it won another one for the second episode. However, since both episodes are merged, the entry 145 (corresponding to the second episode) was intentionally left empty to avoid potential duplicates, depending on the type of certain queries (i.e.: _"What's the total size in MBs for all the Cacoward's entries?"_).
  - Some WADs have different versions to download, which means that the Size on MB may slightly vary depending on your version. This applies, for instance, to _"REKKR"_ or _"Dimension of the Boomed"_.

### 2.2 WAD Additional Features

* Even if there is a single new graphic, sprite or texture (i.e.: simply a new sky, for instance), that's enough to classify as TRUE the New Graphics column of that wad. Same applies for new sounds and/or new music.

* In order to be TRUE, there has to be music from another game, or music specifically written for the wad. For instance, if a _Doom 2_ WAD uses music from "Heretic", it will be considered TRUE, while if a _Doom 2_ WAD uses music from another _Doom 2_ level or from _Doom_ it will count as FALSE.

### 2.3 WAD Authors

* If one author has had several nicks across his modding career, the database will mention only the most popular (i.e.: the one mentioned on the author's [Doom Wiki](https://doomwiki.org/wiki/Entryway)'s page title) or the most recent one.

* In some cases, there were more than one e-mail address for an author, but only one was chosen.

* Deceased authors will have their e-mail address fields marked as "(DECEASED)".

## 3. HOW TO QUERY THE DATABASE

It is very simple. Download the files _cacowards_sql_querying_on_jupyter.ipynb_ and _cacowards_sqlite.db_, making sure they are on the same directory. Then simply execute the .ipynb file by running a Jupyter Notebook.

## 4. GLOSSARY (in alphabetical order)

The following definitions were mostly extracted from Wikipedia and the [Doom Wiki](https://doomwiki.org/wiki/Entryway) (there was some minor editing involved though). If you're already familiar with _Doom_ and the Cacowards ceremony, you can skip this section.

**4.1. CACOWARDS:** The Cacowards are an annual event featured at the [Doomworld website](https://www.doomworld.com/cacowards/), targeting the anniversary of _Doom_'s release, which aims to single out the best WAD/mods released in the year prior and give them an award. Exceptionally bad, funny, or unique WAD/mods are sometimes given special irregular awards, and runners up are also mentioned. Modifications considered are subjected to a year-long nomination process through the forums, the thread for which is usually started immediately after the new year passes. 

The series started in 2004 with the so-called 11th edition, which attempted to replicate the success of similar articles in the previous year's [10 Years of Doom](https://www.doomworld.com/10years/) celebration, the [Top 100 WADs of All Time"](https://www.doomworld.com/10years/bestwads/) and the [Top 10 Infamous WADs](https://www.doomworld.com/10years/bestwads/infamous.php).

**4.2. COOPERATIVE:** Cooperative gameplay, often referred to as co-op or coop, is a multiplayer game mode in which human players cooperate against a given game's monsters.

**4.3. DEATHMATCH:** Deathmatch is a multiplayer game style pioneered by _Doom_ in which players face off against each other, their computers connected to a common server via a network.

- A point, called a frag, is granted to the players whenever they kill an opponent.
- Frags are deducted when a player commits suicide, or dies accidentally (i.e.: by falling into lava).
- Upon death, players restart at a random point in the level.
- When the level ends, the intermission screen gives each player's frag count. The one with most frags will be the winner.

In more recent times, classic deathmatch has become known as FFA (free-for-all), in order to differentiate it from other player-vs-player game modes.

**4.4. DEHACKED:** It is an editor originally created for the original _Doom_ that allows the operation of the executable to be changed. Hit points, sounds, frame sequences, text strings and several other miscellaneous values can be changed. Modifications can be distributed in the form of DeHackEd "patches" which can be applied to the executable. In order to do this, DeHackEd has the ability to generate an exact copy of the _Doom_ or _Doom_ II executable.

Even though many advanced effects can be achieved with DeHackEd, it does not offer the complete flexibility that a custom source port can provide.

**4.5. DOOM:** A series of popular action videogames that consolidated the first-person shooter genre. With a science fiction and horror style, it gives the players the role of [space] marines who find themselves in the focal point of an invasion from hell. The games [also] introduced deathmatch and cooperative play (...), and helped further the practice of allowing and encouraging fan-made modifications ("mods") of commercial video games. 

Entries releases: 

* _DOOM = December 10, 1993_
* _DOOM II: Hell on Earth = October 10, 1994_
* _Master Levels for DOOM II =  December 26, 1995_
* _Final DOOM = June 17, 1996_
* _DOOM 64 = March 31, 1997_
* _DOOM 3 = August 3, 2004_
* _DOOM [2016] = May 13, 2016_
* _DOOM Eternal = March 20, 2020_

**4.6. /idgames/ ARCHIVE:** It is the largest online archive of levels, modifications, tools and other material for _Doom_ engine games. To alleviate bandwidth usage and ensure that data will not be lost, the archive is mirrored on various alternative FTP sites around the world which are recommended for downloads.

The directory can be consulted on the following [link](https://www.doomworld.com/idgames/).

**4.7. IWAD:** The acronym IWAD is generally interpreted as "internal WAD" and refers to a WAD file which contains all of the external data for a complete game. In order to be identified as IWAD, a file must contain the "IWAD" (49 57 41 44) magic identifier as the first four bytes in its header. An IWAD file is required for execution of any of the stock _Doom_ engine games. This is in contrast to PWADs, which are "patch" WADs intended to replace or augment the content found in the IWAD.

**4.8. MOD:** A mod (short for "modification") is an alteration by players or fans of a video game that changes one or more aspects of that video game, such as how it looks or behaves. Mods may range from small changes and tweaks to complete overhauls, and can extend the replay value and interest of the game. Popular games can have tens of thousands of mods created for them.

**4.9. SINGLE PLAYER:** Single player is the baseline game mode in _Doom_. The player starts in a level and has to find the exit, while killing all the monsters that wander across the different areas. When the player dies in this game mode, the level is reset and the player has to start it again, but now only wielding a pistol.

**4.10. SKILL LEVELS:** Each game skill level provides general difficulty settings that allow a greater variety of players to enjoy the game, allowing novices to face fewer opponents even with advantages for the player, and giving those who have mastered the game a challenge against many monsters, possibly with enhanced aggressiveness.

**4.11. SOURCE PORT:** A source port is a port of the source code for the _Doom_ engine. The term usually denotes a modification made by fans, as opposed to any of the officially licensed versions produced by id Software (the software company responsible for the _Doom_ franchise). The original purpose of source ports was cross-platform compatibility, but shortly after the release of the source code, programmers were correcting old, unaddressed _Doom_ bugs and deficiencies in their own source ports, and later began adding new features to alter gameplay.

The full list of available source ports can be consulted [here](https://doomwiki.org/wiki/Source_port#List_of_source_ports). If you find it overwhelming, as a reference I use the [GZDoom](https://www.zdoom.org/index) source port, but there are other options with the same quality, so I encourage you to research them before choosing one.

**4.12. WAD:** An acronym for _"Where's All the Data?"_. It is the file format used by _Doom_ and all _Doom_-engine-based games for storing data (graphics, sounds, music, levels, and other game data).

## 5. CREDITS

The Cacoward's SQL Database, along with its documentation, were built from scratch by **Daniel Palacio**.

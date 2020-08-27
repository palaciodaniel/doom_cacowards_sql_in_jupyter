# Doom's Cacowards SQL - A database queried with Jupyter Notebook

## 0. ABOUT

The following project was started with several objectives in mind, that can be summarized like this:

* I. To gain experience in building from scratch a somewhat complex SQL database.
* II. To have a good showcase application for the "ipython-sql" package, which allows to easily query SQL databases in Jupyter Notebook.
* III. To get a comprehensive but at the same time accessible list to check all the available levels from this annual ceremony.
* IV. To eventually keep updating the database with more information.
* V. To have an opportunity to practice writing several pages of documentation in an organized and tidy way (with the added challenge that I'm not a native English speaking person).

For all these reasons, I chose as a subject the Cacoward Awards, which celebrates the best user-made creations for the -still- immensely popular FPS "Doom" franchise. Should you feel confused about what it is actually about, there is a detailed glossary on Section 2 to clear all your doubts. Otherwise, feel free to continue to the next section...

## 1. IMPORTANT INFORMATION

The following is a detailed description about how the data was organized and the reasons behind those decisions. Before querying the database it is strongly recommended to read it in its entirety to avoid potential confusions. And as expressed before, if there is a term that you don't know or don't fully understand, there is a glossary where most likely it will be explained.

* The database is all about the Cacoward Winners. Other categories, like "Runner Ups", weren't included. Also, since Cacowards were introduced on 2004, the Winners from the previous ten years weren't included either.

* Regarding ambitious WADS, the database is also about all the people that were part of those projects. Not only level designers, but also people who made new graphics or music, beta tested or gave significant feedback for the WADs were included as well. Since the Doom Wiki already does a good job in indicating the level's authors on every WAD, the database aims to answer the simple question _"Was this person somehow involved with this project or not?"_. So, for instance, if John Romero gave a lot of advice for a certain WAD, it will count as TRUE even if he didn't contribute a level for it.

* The database was built primarily from information present on the .txt files for every WAD's /idgames page. A complementary source of data was the Doom Wiki (specially for Author's information). In some cases, the WADs have official pages where everything was already organized there. Failure to get information from these three sources are the reasons for 95% of NULL fields on this database; the remaining 5% was due to ambiguous or contradictory information (i.e.: a WAD described as Single Player on the /idgames description, but with Deathmatch support only on the .txt file).

* In order to be mentioned as part of a project, it is required that the person actively contributed to it. So, for instance, if one person wrote a song for a specific WAD, and that song is used for another one a few years later, this person won't be counted as an active contributor for this second project. Unfortunately, the majority of WADs aren't clear on this aspect, so on some ambiguous cases some people weren't mentioned to avoid confusions; it would be easier to add them later than to having to remove them from that field.

* In the event that a WAD (no matter its scale) was made by no more than two or three people, only those people will be mentioned. For instance, _"Sunlust"_ only has its two authors mentioned; other contributors weren't mentioned at all.

* There might be potential features to be further included: most importantly, the specific contribution that a person made for a project (i.e.: as a beta-tester, musician, level designer, etc), the inclusion of more real names or e-mail addresses, along with nationalities, and the mention of beta-testers or other contributors for projects made by one or two people. As of the moment of writing this document, the Doom Community isn't aware of the existence of this database, and further completion will depend on their interest once they're eventually contacted. 

### 1.1. WADS

* A lot of wads (specially the most recent ones) will require a source port. The database doesn't indicate which ones run with the original Doom engine and which ones require one of these advanced ports. It isn't necessary to detail this requirement, since the safest option is to always use a source port.

* If a wad has Roman numbers (i.e.: _"Deus Vult II"_), for queries it is required to use normal numbers instead (i.e.: _"Deus Vult 2"_). 

* If you don't need an IWAD to run a wad, it will appear as "(STANDALONE)".

* If a new level only serves as a HUB it won't be counted. So, for example, a wad with 9 levels and 2 hub levels will appear as having 9 levels on its column.

* Regarding Multiplayer modes and Different Difficulties, if in the .txt file on the /idgames directory it only says _"Not Tested"_, _"Not effectively"_, _"Start Only"_, _"Maybe"_, or something like that, they will be considered FALSE. It is extremely unlikely that untested features are properly balanced, so it was the most sensible option to classify them as FALSE.

* If a project won a Cacoward on a certain year, but then it was later patched, the Size and URL columns will reflect these changes.

### Special cases:
  - Even though both levels from _"Monster Hunter Ltd"_ are taken as a single Cacoward entry, for practical reasons they were divided in two entries for this database.
  - _"The Adventure of Square"_ won a Cacoward for its first episode and then a few years later it won another one for the second episode. However, since both episodes are merged, the entry 145 (corresponding to the second episode) was intentionally left empty to avoid potential duplicates, depending on the type of certain queries (i.e.: _"What's the total size in MBs for all the Cacoward's entries?"_).
  - Some WADs have different versions to download, which means that the Size on MB may slightly vary depending on your version. This applies, for instance, to _"REKKR"_ or _"Dimension of the Boomed"_.

### 1.2 WAD additional contents

* Even if there is a single new graphic, sprite or texture (i.e.: simply a new sky, for instance), that's enough to classify as TRUE the New Graphics column of that wad. Same applies for new sounds and/or new music.

* In order to be TRUE, there has to be music from another game, or music specifically written for the wad. For instance, if a "Doom 2" WAD uses music from "Heretic", it will be considered TRUE, while if a "Doom 2" WAD uses music from another "Doom 2" level or from "Doom" it will count as FALSE.

### 1.3 WAD Authors

* If one author has had several nicks across his modding career, the database will mention only the most popular (i.e.: the one mentioned on the author's Doom Wiki's page title) or the most recent one.

* In some cases, there were more than one e-mail address for an author, but only one was chosen.

* Deceased authors will have their e-mail address fields marked as "(DECEASED)".

## 2. GLOSSARY (in alphabetical order)

The following definitions were mostly extracted from Wikipedia and the Doom Wiki (there was some minor editing involved though). If you're already familiar with Doom and the Cacowards ceremony, you can skip this section.

**2.1. CACOWARDS:** The Cacowards are an annual event featured at the Doomworld website, targeting the anniversary of Doom's release, which aims to single out the best WAD/mods released in the year prior and give them an award. Exceptionally bad, funny, or unique WAD/mods are sometimes given special irregular awards, and runners up are also mentioned. Modifications considered are subjected to a year-long nomination process through the forums, the thread for which is usually started immediately after the new year passes. 

The series started in 2004 with the so-called 11th edition, which attempted to replicate the success of similar articles in the previous year's "10 Years of Doom" celebration, the "Top 100 WADs of All Time" and the "Top 10 Infamous WADs".

**2.2. COOPERATIVE:** Cooperative gameplay, often referred to as co-op or coop, is a multiplayer game mode in which human players cooperate against a given game's monsters.

**2.3. DEATHMATCH:** Deathmatch is a multiplayer game style pioneered by Doom in which players face off against each other, their computers connected to a common server via a network.

- A point, called a frag, is granted to the players whenever they kill an opponent.
- Frags are deducted when a player commits suicide, or dies accidentally (i.e.: by falling into lava).
- Upon death, players restart at a random point in the level.
- When the level ends, the intermission screen gives each player's frag count. The one with most frags will be the winner.

In more recent times, classic deathmatch has become known as FFA (free-for-all), in order to differentiate it from other player-vs-player game modes.

**2.4. DEHACKED:** It is an editor originally created for the original Doom that allows the operation of the executable to be changed. Hit points, sounds, frame sequences, text strings and several other miscellaneous values can be changed. Modifications can be distributed in the form of DeHackEd "patches" which can be applied to the executable. In order to do this, DeHackEd has the ability to generate an exact copy of the Doom or Doom II executable.

Even though many advanced effects can be achieved with DeHackEd, it does not offer the complete flexibility that a custom source port can provide.

**2.5. DOOM:** A series of popular action videogames that consolidated the first-person shooter genre. With a science fiction and horror style, it gives the players the role of [space] marines who find themselves in the focal point of an invasion from hell. The games [also] introduced deathmatch and cooperative play (...), and helped further the practice of allowing and encouraging fan-made modifications ("mods") of commercial video games. 

Entries releases: 

* _DOOM = December 10, 1993_
* _DOOM II: Hell on Earth = October 10, 1994_
* _Final DOOM = June 17, 1996_
* _Doom 64 = March 31, 1997_
* _DOOM 3 = August 3, 2004_
* _DOOM [2016] = May 13, 2016_
* _DOOM Eternal = March 20, 2020_

**2.6. /idgames/ ARCHIVE:** It is the largest online archive of levels, modifications, tools and other material for "Doom" engine games. To alleviate bandwidth usage and ensure that data will not be lost, the archive is mirrored on various alternative FTP sites around the world which are recommended for downloads.

**2.7. IWAD:** The acronym IWAD is generally interpreted as "internal WAD" and refers to a WAD file which contains all of the external data for a complete game. In order to be identified as IWAD, a file must contain the "IWAD" (49 57 41 44) magic identifier as the first four bytes in its header. An IWAD file is required for execution of any of the stock Doom engine games. This is in contrast to PWADs, which are "patch" WADs intended to replace or augment the content found in the IWAD.

**2.8. MOD:** A mod (short for "modification") is an alteration by players or fans of a video game that changes one or more aspects of that video game, such as how it looks or behaves. Mods may range from small changes and tweaks to complete overhauls, and can extend the replay value and interest of the game. Popular games can have tens of thousands of mods created for them.

**2.9. SINGLE PLAYER:** Single player is the baseline game mode in "Doom". The player starts in a level and has to find the exit, while killing all the monsters that wander across the different areas. When the player dies in this game mode, the level is reset and the player has to start it again, but now only wielding a pistol.

**2.10. SKILL LEVELS:** Each game skill level provides general difficulty settings that allow a greater variety of players to enjoy the game, allowing novices to face fewer opponents even with advantages for the player, and giving those who have mastered the game a challenge against many monsters, possibly with enhanced aggressiveness.

**2.11. SOURCE PORT:** A source port is a port of the source code for the "Doom" engine. The term usually denotes a modification made by fans, as opposed to any of the officially licensed versions produced by id Software (the software company responsible for the "Doom" franchise). The original purpose of source ports was cross-platform compatibility, but shortly after the release of the source code, programmers were correcting old, unaddressed "Doom" bugs and deficiencies in their own source ports, and later began adding new features to alter gameplay.

**2.12. WAD:** An acronym for _"Where's All the Data?"_. It is the file format used by "Doom" and all Doom-engine-based games for storing data (graphics, sounds, music, levels, and other game data).

# beets-popularity

Beets plugin to store the popularity values from Spotify as flexible item attributes in the database

## Installation
Using pip:
  
    pip install beets-popularity

Manually:

    git clone https://github.com/abba23/beets-popularity.git
    cd beets-popularity
    python setup.py install

## Usage
    $ beet popularity happy
    popularity: Bon Jovi - The Circle - Happy Now: 20
    popularity: The Doors - Strange Days - Unhappy Girl: 40
    popularity: Kygo - Cloud Nine - Happy Birthday: 59

## Options
| Option | |Description |
| ------ | ------ | ------ |
| -a | \-\-album | match albums instead of tracks |
| -n | \-\-nowrite | print the popularity values without storing them |

## Import
All imported files will automatically have a popularity attribute and value assigned to them, if they are on Spotify and the plugin is enabled.
    
## Query
As the popularity of a song is a value between 0 and 100, you could filter your library like this in order to list all tracks that have a popularity of at least 20:

    $ beet list -f '$title - $artist ($popularity)' popularity:20..100
    Bon Jovi - Happy Now (20)
    The Doors - Unhappy Girl (40)
    Kygo - Happy Birthday (59)
    
This is especially useful in combination with the [Smart Playlist Plugin](https://beets.readthedocs.io/en/v1.4.3/plugins/smartplaylist.html). Adding this to your configuration would allow you to have continuously updated playlists of the most popular songs in your library:

    smartplaylist:
        playlist_dir: ~/Music/Playlists
        playlists:
            - name: popular.m3u
              query: 'popularity:70..100'
    
            - name: popular_rock.m3u
              query: 'popularity:60..100 genre:Rock'
GSO Music Application v5.12
===========================

New in v5.12
-------------
- M4A is now handled as a first-class audio format alongside MP3.
- File pickers, folder scans, local attachment storage, playback queues, playlist playback, All Songs Player, and audio quiz modes accept M4A files.
- Embedded MP4/M4A metadata atoms such as title, artist, album, year, genre, track, composer, comment, cover-art summary, and common freeform atoms are read into Embedded tags and used for form/library prefill.
- Library bulk selection wording now says Select without audio instead of Select without MP3, because the app supports MP3, M4A/MP4, AAC, WAV, OGG, and FLAC attachments.
- Source embedded-tag writing remains intentionally limited to MP3/ID3. M4A/MP4 tags are read and stored in the browser library but are not rewritten into the original source M4A file.

GSO Music Application v5.11
===========================

New in v5.11
-------------
- The bottom song player is hideable. Use Hide player to keep music playing without the large fixed player bar, then Show player to bring it back.
- In Add/Edit song, the Notes and Embedded tags editor zones can be shown or hidden independently.
- The Logs tab now has search plus Status and Year filters, and log rows display the song year.
- The Quiz tab now includes two audio games: listen and choose the artist from 6 choices, and listen and choose the title from 6 choices. These modes use songs with attached audio.
- The Light/Dark and Help buttons now share the same light-blue 3D styling and size.

GSO Music Application v5.10
===========================

New in v5.10
-------------
- The Add/Edit song form now exposes an Embedded tags editor. When a Library song is opened with Edit, the stored embeddedTags can be changed directly as JSON or as key: value lines.
- When editing an MP3 that was imported from an authorized folder, Save can write the edited ID3 text tags back to the original source MP3 file. This uses the browser File System Access API and requires folder write permission.
- Source MP3 writing preserves non-managed binary ID3 frames such as embedded artwork when possible, while replacing managed text tags such as title, artist, album, track, year, genre, comments, lyrics, and custom text tags.
- Source writing is intentionally limited to MP3/ID3. MP4/M4A atom writing remains read-only.

GSO Music Application v5.9
==========================

What it is
-----------
A self-contained offline browser application for managing a personal song library, playlists, local audio playback, rebuilt duplicate detection, lyrics search, music statistics, and direct deletion of files from an authorized browser folder when supported, a dedicated deletion Logs tab, and quota-safe metadata storage for large libraries.

Files
-----
- index.html   : Main application page with tabs
- styles.css   : Visual styling
- app.js       : Application logic
- help.html    : User help page
- README.txt   : This guide
- CHANGELOG.txt: Change summary
- Updates.txt  : Requested improvements implemented in this version

How to run
----------
1. Open index.html in a modern browser.
2. Use Import / Export to import CSV/JSON metadata or to attach/import MP3, MP4, M4A, AAC, WAV, OGG, or FLAC files.
3. Use Library to search, filter, play, edit, favorite, attach audio, delete only the browser entry, or delete the original file from an authorized folder.
4. Use Playlists to create playlists, select a song to add, filter by song/artist/year/genre, and show or hide each playlist's songs.
5. Use Playlist Player to play a selected playlist, or use Shuffle play all songs to start playback without selecting a playlist.
6. Use All Songs Player to play all attached songs, songs by artist, songs by genre, favorites only, or songs by year with shuffle and repeat options.
7. Use Duplicates to review same-title or similar-title candidates with its own filters, play attached audio, delete original files directly when folder write permission is available, copy Windows CMD delete commands as fallback, or export duplicate CSV.
8. Use Statistics to review library statistics, playlist statistics, and top 5/10/20/30/40/50 rankings.
9. Use Song Info from a Library song card to fetch public web metadata and display useful search links in the Song Info tab.
10. Use Lyrics from a Library song card to display web lyrics search links and any lyrics embedded in local audio tags.
11. Use Library filters plus Select filtered / Add filtered / Select without audio to select multiple songs. Use Bulk edit to open the bulk edit popup.
12. Use Logs to review every confirmed Delete file attempt from Library or Duplicates, including success, failure, year, relative path, full path, fallback CMD command, and search/status/year filtering.
13. Use Quiz to test song knowledge with mixed year/artist/title questions, typed-year questions, or audio recognition games where the user listens and chooses the artist or title from 6 choices.



Recommended way to run on a laptop
-----------------------------------
This fixed package includes a lightweight Node.js launcher. It uses only built-in Node modules, so no npm library installation is required.

Windows:
1. Install Node.js LTS if needed.
2. Double-click start-gso-music.bat.
3. The app opens at http://127.0.0.1:4173/. Keep the terminal window open while using it.

Command line:
  npm start

or:
  node server.js

You can still open index.html directly, but localhost is recommended because it avoids some browser restrictions linked to file:// pages.

Direct browser deletion and Logs in v5.4
-------------------------------
Direct deletion is now available from the Library and Duplicates views when the app can use a remembered folder handle with write permission. The workflow is:

1. Launch the app through localhost with start-gso-music.bat or npm start.
2. Go to Import / Export.
3. Use Choose / scan folder and approve the folder permission requested by the browser.
4. The app stores the relative file path for each imported audio file.
5. Use Delete file in Library or Duplicates to delete the disk file directly and remove the song from the browser library.
6. Open Logs to review the deletion result, path used, relative path, and fallback CMD command if direct deletion failed.

If the browser reports that the file cannot be found, the app now treats this as a recoverable condition: it removes the stale library entry, records a warning log, and copies the Windows CMD fallback command when a full path is available. If direct deletion is not supported or permission is denied, the app keeps the existing safe fallback: it copies a Windows CMD del command for manual review.



GSO Music Application v5.9 - requested changes
================================================

This version implements the requested changes:

1. Duplicate search has been rebuilt. Duplicate groups are now detected first from the current Library-filtered song set, then the Duplicates tab search and filters narrow the visible duplicate groups. This prevents a duplicate group from disappearing when the duplicate search text matches only one member of the group.
2. The old Select songs by and Value controls have been removed. Multi-selection now uses the Library filters only: set the Library filters, then click Select filtered or Add filtered.
3. Bulk edit is now opened through a dedicated popup. The popup supports Playlist, Genre, Year, Artist, Album, Rating, and Favorite.
4. Library now includes Select without audio, which selects songs matching the active Library filters that do not have an attached local audio file.

GSO Music Application v5.8 - Updates.txt implementation
=======================================================

This version implements the requested Updates.txt changes:

1. Library now has a rule-based multi-selection toolbar. You can select or add matching songs by current Library filters, artist, year, album, or playlist, then use the existing bulk actions.
2. Duplicates are now calculated from the current Library-filtered song set first, then narrowed by the Duplicate tab filters.
3. Every Library song card now has a Search lyrics button. It opens a dedicated Lyrics tab with web lyrics search links and displays any lyrics already embedded in the local audio tags.

GSO Music Application v5.7 - Updates.txt implementation
=======================================================

This version implements the requested Updates.txt changes:

1. Added a dedicated Quiz tab with mixed questions for year, artist, and title.
2. Added a typed-year quiz mode that asks for the year based on title and artist.
3. Added quiz answer history showing given answer vs correct answer, with configurable question count and countdown seconds.
4. Quiz candidates exclude empty or unknown years, titles, and artists.
5. Duplicate detection now uses a probability score based on title, artist, album, duration/length, file size, and year, and the Duplicates table shows the score.
6. Bulk selection now supports multiple-song metadata updates, browser-entry deletion, direct selected-file deletion when folder write permission is available, and a clear-selection button.
7. The Help page now has two tabs: User guide and Technical info.
8. The attached application picture is included as app-icon.png and displayed in the application header.


GSO Music Application v5.6 - Updates.txt implementation
=======================================================

This version implements the requested Updates.txt changes:

1. Added an All Songs Player tab to play all attached songs, songs by artist, songs by genre, favorites only, or songs by year, with Shuffle, Repeat all, and Repeat one.
2. Added a Clear filters button in the Library tab.
3. In Library cards, album names are now light blue and duration values are blue.
4. File name and path are grouped into a single File and path block, hidden by default, with a central Show file and path / Hide file and path button for all song cards.
5. Song statistics now has dedicated options to exclude Unknown Artist / Unknown Genre values from artist and genre charts.

GSO Music Application v5.5 - Updates.txt implementation
-------------------------------------------------------
This version implements the requested Updates.txt changes:

1. Library filters are combined/dependent: selecting an artist narrows the available title, year, genre, and playlist filter values, and each filter updates based on the other active filters.
2. Playlist Player starts as the default tab and includes Shuffle play all songs for playback without selecting a playlist first.
3. Statistics includes playlist statistics and the Top values selector now supports Top 30, Top 40, and Top 50.
4. Library cards visually highlight titles in yellow, artists in red, and years in green.
5. Playlist tags are shown as light-blue 3D buttons.
6. Duplicates has its own filters for search, match type, title, year, artist, and playlist; duplicate CSV export follows these filters.
7. Every Library song card has a Search web info button. It opens the Song Info tab, shows web-search links, and attempts an automatic MusicBrainz lookup for release, artist, album, year, and recording details.

Loading fix in v5.1
-------------------
The page no longer calculates duplicate groups and all secondary tabs during the initial render. The Library tab renders songs in batches of 250, and heavy panels such as Duplicates are calculated only when opened. This prevents freezing when a large music folder has already been imported.

Earlier implemented from previous Updates.txt
---------------------------------------------
1. Playlists: the song-to-add selector is combined with Artist, Year, and Genre controls.
2. Theme: dark mode is the default. The theme button shows "Light" while dark mode is active and "Dark" while light mode is active.
3. Playlists: the former combined action is split into two clear buttons: Create playlist and Add selected song.
4. Playlists: each playlist card has a Show songs / Hide songs button; song lists are hidden by default.
5. Playlist Player: shuffle, repeat all, and repeat one are available.
6. Duplicates: the tab now detects same-title and similar-title candidates and can play attached songs directly.
7. Duplicates: the tab can remove a song from the browser library and copy a Windows CMD del command for the original file path.
8. v5.2 adds direct browser file deletion when the folder was authorized with write permission.
9. help.html was updated for these changes.
10. v5.4 moves library metadata to IndexedDB, makes save operations quota-safe, trims oversized embedded tags, and handles browser "file not found" delete results without crashing.

Data storage
------------
Song metadata is now stored primarily in IndexedDB under:

  local-song-audio-v1 / settings / songLibrary

This avoids the localStorage quota error on large libraries. During first launch, the app migrates any existing metadata from the old localStorage key and then clears that large localStorage copy:

  local-song-library-v1

If IndexedDB is unavailable, the app falls back to a compact localStorage save with oversized embedded tags removed. Save errors are caught so actions such as Delete file, Remove + CMD, and duplicate removal do not crash on quota errors.

Manual playlist names are stored in localStorage under:

  local-song-playlists-v1

Confirmed Delete file command logs are stored in localStorage under:

  local-song-delete-logs-v1

Attached audio files are stored separately in IndexedDB under:

  local-song-audio-v1 / audioFiles

The app runs locally. It does not upload files to a server.

Important browser limitation
----------------------------
A browser page cannot silently read or delete files from a typed Windows path. For folder import and direct file deletion, you must authorize the folder with the browser picker. Direct deletion uses the browser folder permission; when that is not available, the app copies a Windows CMD command such as:

  del /f /q "C:\Music\Artist\Song.mp3"

Run that command yourself in Windows CMD only after checking that the path is correct. Use Delete file only after verifying the confirmation dialog because direct deletion removes the original disk file.

CSV import / export
-------------------
Supported app CSV columns include:
Title, Artist, Album, Genre, Track, Year, Length, Size, Last Modified, Path, Filename, Playlist, Audio Path, Audio Relative Path, Embedded Tags

The app also supports the enriched mp3tag-style columns already used by earlier versions.

Duplicate detection
-------------------
Duplicate candidates are grouped when titles are the same after normalization or similar enough by edit-distance/token comparison. This deliberately favors review over automatic deletion: remasters, live versions, radio edits, and alternate recordings can be false positives.

Use Export duplicate CSV to archive the duplicate review list, including group number, match type, full storage path, and Windows delete command.

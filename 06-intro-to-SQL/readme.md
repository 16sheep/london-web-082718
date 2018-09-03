# Intro to SQL

1. Install the SQLite Browser if you haven't already [here](http://sqlitebrowser.org/)
2. Open the SQLite Browser and click 'File -> Open DataBase'
3. Choose the `chinook.db` file from this repo. This database is open source and maintained by Microsoft (SQL is no fun if you don't have any data)
4. Click the tab that says 'Execute SQL'. Type SQL queries in the box above. Press the play button. See the results of that query in the box below

## sqlite3 formatting

```sql
.mode column
.headers on
```

## Joins explained

[Link](http://blog.seldomatt.com/blog/2012/10/17/about-sql-joins-the-3-ring-binder-model/)

## Query examples

1. Write the SQL to return all of the rows in the artists table?

```SQL
SELECT * FROM artists;
```

2. Write the SQL to select the artist with the name "Black Sabbath"

```SQL
SELECT * FROM artists WHERE artists.name = "Black Sabbath"
```

3. Write the SQL to create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

```sql
CREATE TABLE fans (
  id INTEGER PRIMARY KEY,
  name TEXT
);
```

4. Write the SQL to alter the fans table to have a artist_id column type integer?


```sql
ALTER TABLE fans ADD COLUMN (artist_id INTEGER);
```

5. Write the SQL to add yourself as a fan of the Black Eyed Peas? ArtistId **169**

```sql
INSERT INTO fans (name, artist_id) VALUES ("Louis", 169);
```

or

```sql
INSERT INTO fans (name, artist_id) VALUES ("Rishi", SELECT (ArtistId) FROM artists WHERE artists.name = "Black Eyed Peas");
```

8. Write the SQL to return fans that are not fans of the black eyed peas.

```sql
SELECT name FROM fans WHERE fans.artist_id != 169;
```

9. Write the SQL to display all artists's names next to their album titles

```sql
SELECT artists.Name, albums.Title from artists INNER JOIN albums ON artists.ArtistId = albums.ArtistId;
```

10. Write the SQL to display artist name, album name and number of tracks on that album

```sql
SELECT artists.Name, albums.Title, count(tracks.trackId) as Tracks from artists
INNER JOIN albums ON artists.ArtistId = albums.ArtistId
INNER JOIN tracks ON albums.AlbumId = tracks.AlbumId
GROUP BY albums.AlbumId;
```

11. Write the SQL to return the name of all of the artists in the 'Pop' Genre

```sql
SELECT artists.Name, albums.Title, COUNT(tracks.Name) from artists INNER JOIN albums ON artists.ArtistId = albums.ArtistId INNER JOIN tracks ON albums.AlbumId = tracks.AlbumId GROUP BY albums.AlbumId;
```

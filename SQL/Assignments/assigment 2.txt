/* Assignment - 2 (SQL | Aggregate Functions & JOINs) */

/* 1. How many tracks does each album have? Your solution should include Album id 
and its number of tracks sorted from highest to lowest. */
SELECT 		AlbumId, count(name) as "name count"
FROM		tracks
GROUP BY 	AlbumId
ORDER BY 	count(name) DESC;

/* 2. Find the album title of the tracks. 
Your solution should include track name and its album title. */
SELECT 		tracks.Name, albums.Title
FROM		albums
INNER JOIN	tracks
ON			albums.AlbumId = tracks.AlbumId;

/* 3. Find the minimum duration of the track in each album.
Your solution should include album id, album title 
and duration of the track sorted from highest to lowest. */
SELECT 		tracks.AlbumId, albums.Title, 
			min(tracks.Milliseconds) as min_duration
FROM		tracks
LEFT JOIN	albums
ON			albums.AlbumId = tracks.AlbumId
GROUP BY 	tracks.AlbumId
ORDER BY	min_duration DESC;

/* 4. Find the total duration of each album. 
Your solution should include album id, album title 
and its total duration sorted from highest to lowest. */
SELECT 		tracks.AlbumId, albums.Title, 
			sum(tracks.Milliseconds) as total_duration
FROM		tracks
LEFT JOIN	albums
ON			albums.AlbumId = tracks.AlbumId
GROUP BY 	tracks.AlbumId
ORDER BY	total_duration DESC;

/* 5. Based on the previous question, find the albums 
whose total duration is higher than 70 minutes. 
Your solution should include album title and total duration. 
1 minute = 60 000 milliseconds - 70 minutes = 4200000 milliseconds*/
SELECT 		tracks.AlbumId, albums.Title, 
			sum(tracks.Milliseconds) as total_duration
FROM		tracks
LEFT JOIN	albums
ON			albums.AlbumId = tracks.AlbumId
GROUP BY 	albums.Title
HAVING		total_duration > 4200000
ORDER BY	total_duration DESC;
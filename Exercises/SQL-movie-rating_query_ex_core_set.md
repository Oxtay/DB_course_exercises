# SQL Movie-Rating Query Exercises (core set)

Find the titles of all movies directed by Steven Spielberg.

```sql
SELECT title
FROM Movie
WHERE director='Steven Spielberg'
```

Find all years that have a movie that received a rating of 4 or 5, and sort them in increasing order.

```sql
SELECT distinct year
FROM Movie, Rating
WHERE Movie.mID=Rating.mID and stars > 3
order by year asc;
```

Find the titles of all movies that have no ratings.

```sql
SELECT distinct title
FROM Movie, Rating
WHERE Movie.mID not in (select Movie.mID from Movie, Rating where Movie.mID = Rating.mID)
```

Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.

```sql
select distinct name
from Reviewer, Rating
where Reviewer.rID=Rating.rID and ratingDate is null
```

Write a query to return the ratings data in a more readable format: reviewer name, movie title, stars, and ratingDate. Also, sort the data, first by reviewer name, then by movie title, and lastly by number of stars.

```sql
select distinct name, title, stars, ratingDate
from Movie, Reviewer, Rating
where Movie.mID=Rating.mID and Reviewer.rID=Rating.rID
order by name, title, stars;
```

For all cases where the same reviewer rated the same movie twice and gave it a higher rating the second time, return the reviewer's name and the title of the movie.

```sql
select name, title
from Reviewer, Movie, Rating, Rating r2
where Reviewer.rID = Rating.rID 
    and Movie.mID = Rating.mID
    and Movie.mID = r2.mID
    and Rating.rID = r2.rID
    and Rating.ratingDate < r2.ratingDate
    and Rating.stars < r2.stars
```

For each movie that has at least one rating, find the highest number of stars that movie received. Return the movie title and number of stars. Sort by movie title.

```sql
select title, max(stars)
from Movie, Rating
where Movie.mID = Rating.mID
group by Rating.mID order by title
```

List movie titles and average ratings, from highest-rated to lowest-rated. If two or more movies have the same average rating, list them in alphabetical order.

```sql
select title, avg(stars) as average
from Movie, Rating
where Movie.mID=Rating.mID
group by title
order by average desc
```

Find the names of all reviewers who have contributed three or more ratings.

```sql
select name
from Reviewer, Rating r1, Rating r2, Rating r3
where Reviewer.rID = r1.rID
    and r1.rID = r2.rID
    and r2.rID = r3.rID
    and ((r1.mID < r2.mID and r2.mID = r3.mID and r2.stars < r3.stars)
    or (r2.mID < r3.mID and r1.mID = r2.mID and r1.stars < r2.stars));
```

An alternative correct solution would be

```sql
select name 
from Reviewer 
where rID in (
select rID from (
select rID, count(mID) as cnt
from Rating
group by rID
having cnt > 2))
```
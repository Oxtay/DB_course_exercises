# SQL Movie-Rating Query Exercises (Challenge level)

Q1. For each movie, return the title and the 'rating spread', that is, the difference between highest and lowest ratings given to that movie. Sort by rating spread from highest to lowest, then by movie title. 

```sql
select title, max(stars)-min(stars) as spread
from Movie, Rating
where Movie.mID = Rating.mID
group by title
order by spread desc
```

Find the difference between the average rating of movies released before 1980 and the average rating of movies released after 1980. (Make sure to calculate the average rating for each movie, then the average of those averages for movies before 1980 and movies after. Don't just calculate the overall average rating before and after 1980.) 

```sql

```
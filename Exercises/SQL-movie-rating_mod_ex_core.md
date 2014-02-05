# SQL Movie Rating Modification Exercises (CoreEx)

Q1. Add the reviewer Roger Ebert to your database, with an rID of 209. 

```sql
insert into Reviewer values (209, 'Roger Ebert')
```

Q2. Insert 5-star ratings by James Cameron for all movies in the database. Leave the review date as NULL. 

```sql
insert into Rating
select rID, mID, 5, null
from Reviewer, Movie
where name = 'James Cameron'
```

Q3. For all movies that have an average rating of 4 stars or higher, add 25 to the release year. (Update the existing tuples; don't insert new tuples.) 

```sql
update Movie set year = year+25
where mID in (select mID 
    from (select Rating.mID, avg(stars) as average
        from Movie, Rating
        where Movie.mID=Rating.mID
        group by Rating.mID)
    where average >=4);
```

Q4. Remove all ratings where the movie's year is before 1970 or after 2000, and the rating is fewer than 4 stars. 

```sql
delete from Rating
where mID in (select mID from Movie where year < 1970 or year > 2000) and stars < 4
```
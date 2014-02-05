# SQL Social Network Query Exercises (Core set)

Q1. Find the names of all students who are friends with someone named Gabriel. 

```sql
select name
from highschooler, friend
where highschooler.ID = friend.ID1
    and friend.ID2 in (select ID from highschooler where name = 'Gabriel')
```

Q2. For every student who likes someone 2 or more grades younger than themselves, return that student's name and grade, and the name and grade of the student they like.

```sql
select name1, grade1, name2, grade2
from (select h1.name as name1, h2.name as name2, h1.grade as grade1, h2.grade as grade2, 
    h1.grade-h2.grade as gradeDiff
    from highschooler h1, highschooler h2, likes
    where h1.ID = ID1 and h2.ID = ID2)
where gradeDiff > 1;
```

Q3. For every pair of students who both like each other, return the name and grade of both students. Include each pair only once, with the two names in alphabetical order. 

```sql
select name1, grade1, name2, grade2
from (select h1.name as name1, h2.name as name2, h1.grade as grade1, h2.grade as grade2
    from highschooler h1, highschooler h2, likes l1, likes l2
    where h1.ID = l1.ID1
        and h2.ID = l1.ID2 
        and l1.ID1 = l2.ID2 
        and l1.ID2 = l2.ID1 
        and h1.name < h2.name);
```

Q4. Find names and grades of students who only have friends in the same grade. Return the result sorted by grade, then by name within each grade. 

```sql
select name, grade
from highschooler
where ID not in (select ID1
from highschooler h1, highschooler h2, friend
where h1.ID = ID1
    and h2.ID = ID2
    and h1.grade <> h2.grade)
    and ID in (select ID1
from highschooler h1, highschooler h2, friend
where h1.ID = ID1
    and h2.ID = ID2
    and h1.grade = h2.grade)
order by grade, name;
```

Q5. Find the name and grade of all students who are liked by more than one other student. 

```sql
select distinct name, grade
from Highschooler h, Likes l1, likes l2
where l1.ID2 = l2.ID2 
    and l1.ID1 <> l2.ID1
    and h.ID = l1.ID2
```
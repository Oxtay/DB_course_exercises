# SQL Social Network Modification Exercises (CoreEx)

Q1. It's time for the seniors to graduate. Remove all 12th graders from Highschooler. 

```sql
delete from Highschooler
where grade = 12
```

Q2. If two students A and B are friends, and A likes B but not vice-versa, remove the Likes tuple. 

```sql
delete from Likes
where exists (select 1 from Friend
            where Friend.ID1 = Likes.ID1 and Friend.ID2 = Likes.ID2)
  and not exists (select 1 from Likes as L2 
            where L2.ID1 = Likes.ID2 and L2.ID2=Likes.ID1)
```

Q3. For all cases where A is friends with B, and B is friends with C, add a new friendship for the pair A and C. Do not add duplicate friendships, friendships that already exist, or friendships with oneself. (This one is a bit challenging; congratulations if you get it right.) 

```sql
insert in Friend (ID1, ID2)
select distinct id1, id2 from (
    select F1.id1 as id1, F2.id2 as id2
    from Friend F1 join Friend F2 on F1.id2 = F2.id1)
```
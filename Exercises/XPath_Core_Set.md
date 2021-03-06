#XML Course-Catalog XPath and XQuery Exercises Core Set

Q1. Return all Title elements (of both departments and courses).
```xml
doc("courses.xml")//Title
```
Q2. Return last names of all department chairs. 
```
doc("courses.xml")/Course_Catalog/Department/Chair/Professor/Last_Name
```
or 
```
doc("courses.xml")//Chair//Last_Name
```
Q3. Return titles of courses with enrollment greater than 500. 
```
doc("courses.xml")//Course[@Enrollment>500]/Title
```

Q4. Return titles of departments that have some course that takes "CS106B" as a prerequisite. 
```
doc("courses.xml")//Department[Course/Prerequisites/Prereq = "CS106B"]/Title
```

Q5. Return last names of all professors or lecturers who use a middle initial. Don't worry about eliminating duplicates. 
```
doc("courses.xml")//(Professor|Lecturer)[Middle_Initial]/Last_Name
```

Q6. Return the count of courses that have a cross-listed course (i.e., that have "Cross-listed" in their description).
```
doc("courses.xml")/Course_Catalog/count(Department/Course[contains(Description,"Cross-listed")])
```

Q7. Return the average enrollment of all courses in the CS department. 
```
doc("courses.xml")/Course_Catalog/Department[@Code = "CS"]/avg(Course/@Enrollment)
```

Q8. Return last names of instructors teaching at least one course that has "system" in its description and enrollment greater than 100. 
```
doc("courses.xml")//Course[contains(Description,"system") 
and @Enrollment>100]/Instructors//Last_Name
```


#XML World-Countries XPath and XQuery Exercises Core Set

Q1.Return the area of Mongolia. 
```xquery
for $c in doc("countries.xml")/countries/country
where $c/@name="Mongolia"
return $c/data(@area)
```

```xpath
doc("countries.xml")/countries/country[@name="Mongolia"]/data(@area)
```

Q2. Return the names of all cities that have the same name as the country in which they are located. 
```xquery
for $c in doc("countries.xml")/countries/country
where $c/@name=$c/city/name 
return <name> {$c/data(@name)} </name>
```

```xpath
doc("countries.xml")/countries/country/city[name=parent::*/@name]/name
```

Q3. Return the average population of Russian-speaking countries.
```xquery
let $plist := doc("countries.xml")/countries/country[language="Russian"]
return avg($plist/data(@population))
```

```xpath
avg(doc("countries.xml")/countries/country[language="Russian"]/data(@population))
```

Q4. Return the names of all countries where over 50% of the population speaks German. (Hint: Depending on your solution, you may want to use ".", which refers to the "current element" within an XPath expression.) 
```xquery
for $c in doc("countries.xml")/countries/country
return $c//language[@percentage>50 and data(.)="German"]/parent::country/data(@name)
```

Q5. Return the name of the country with the highest population. (Hint: You may need to explicitly cast population numbers as integers with xs:int() to get the correct answer.) 
```xquery
for $clist in doc("countries.xml")/countries
return $clist/*[data(@population)=max($clist/country/data(@population))]/data(@name)

```
Introducing the principles of Tidy Data
========================================================
author: Najko Jahn
date: 
autosize: true

What is Tidy Data?
========================================================

According to [Hadley Wickham](http://r4ds.had.co.nz/tidy-data.html#introduction-6) tidy data is a standard way to organize data values within a dataset

![From R for Data Science](http://r4ds.had.co.nz/images/tidy-1.png)

- <http://r4ds.had.co.nz/tidy-data.html#non-tidy-data>

Why is it important?
========================================================

- Organizing datasets as tidy data makes data cleaning efforts easier
- Broad range of analytical tools are built upon the assumption to consume tidy data
- Sharing tidy data increases re-use

Tools to tidy data
========================================================

![](https://pbs.twimg.com/media/C922XSOXgAAyWt2.jpg)

<http://tidyverse.org/>

```r
install.packages("tidyverse")
```


Gathering with tidyr
========================================================

Problem: One variable might be spread across multiple columns.


```r
library(tidyverse)
table4b
```

```
# A tibble: 3 × 3
      country     `1999`     `2000`
*       <chr>      <int>      <int>
1 Afghanistan   19987071   20595360
2      Brazil  172006362  174504898
3       China 1272915272 1280428583
```

Gathering with tidyr
========================================================


```r
table4b %>%
  gather(`1999`, `2000`, key = "year", value = "population")
```

```
# A tibble: 6 × 3
      country  year population
        <chr> <chr>      <int>
1 Afghanistan  1999   19987071
2      Brazil  1999  172006362
3       China  1999 1272915272
4 Afghanistan  2000   20595360
5      Brazil  2000  174504898
6       China  2000 1280428583
```

Gathering with tidyr
========================================================


```r
table4b %>%
  gather(`1999`, `2000`, key = "year", value = "population") %>%
  group_by(country) %>%
  summarize(mean(population))
```

```
# A tibble: 3 × 2
      country `mean(population)`
        <chr>              <dbl>
1 Afghanistan           20291216
2      Brazil          173255630
3       China         1276671928
```

Spreading with tidyr
=========================================================

Problem: One observation might be scattered across multiple rows.


```r
head(table2)
```

```
# A tibble: 6 × 4
      country  year       type     count
        <chr> <int>      <chr>     <int>
1 Afghanistan  1999      cases       745
2 Afghanistan  1999 population  19987071
3 Afghanistan  2000      cases      2666
4 Afghanistan  2000 population  20595360
5      Brazil  1999      cases     37737
6      Brazil  1999 population 172006362
```

Spreading with tidyr
=========================================================


```r
spread(table2, key = type, value = count)
```

```
# A tibble: 6 × 4
      country  year  cases population
*       <chr> <int>  <int>      <int>
1 Afghanistan  1999    745   19987071
2 Afghanistan  2000   2666   20595360
3      Brazil  1999  37737  172006362
4      Brazil  2000  80488  174504898
5       China  1999 212258 1272915272
6       China  2000 213766 1280428583
```

Separate with tidyr
=========================================================

Problem: One column contains more than one variable


```r
table3
```

```
# A tibble: 6 × 3
      country  year              rate
*       <chr> <int>             <chr>
1 Afghanistan  1999      745/19987071
2 Afghanistan  2000     2666/20595360
3      Brazil  1999   37737/172006362
4      Brazil  2000   80488/174504898
5       China  1999 212258/1272915272
6       China  2000 213766/1280428583
```

Separate with tidyr
=========================================================

Problem: One column contains more than one variable


```r
table3 %>%
  separate(rate, into = c("cases", "population"))
```

```
# A tibble: 6 × 4
      country  year  cases population
*       <chr> <int>  <chr>      <chr>
1 Afghanistan  1999    745   19987071
2 Afghanistan  2000   2666   20595360
3      Brazil  1999  37737  172006362
4      Brazil  2000  80488  174504898
5       China  1999 212258 1272915272
6       China  2000 213766 1280428583
```


=========================================================


And now it's your turn!

Examples taken from:

<http://r4ds.had.co.nz/tidy-data.html#non-tidy-data>


# IMDB-ANALYSIS
USE IMDB DATASET TO ANALYSIS ONE MOVIES'RATING AND EARNINGS
# the movie name is Avengers: Endgame
```{r}
filter(moviename,title=="Avengers: Endgame")
```
# connect to the SQLite
```{r}
mydb <- src_sqlite("/Users/zimin/Downloads/movie.db",create = F)
mydb
```
# load data
```{r}
movierate <- tbl(mydb,"rating")
movierate
```
# ratings mean is 6.885 and Median is 7.1
```{r}
summary(movierate)
```
# select Avengers: Endgame Id to find this movies averagerating is 8.4, higher than ratings mean
```{r}
filter(movierate,tconst=="tt4154796")
```
# select Avengers: Endgame from SQLite
```{r}
tbl(mydb,sql("SELECT * FROM year WHERE tconst=='tt4154796'"))
```
# Use movie ID to find the directors Id
```{r}
moviecrew <- tbl(mydb,sql("SELECT * FROM crew WHERE tconst=='tt4154796'"))
moviecrew
```
# select directors ID
```{r}
endgamedirectors <- filter(moviedirectors,nconst%in%c('nm0751577','nm0751648'))
endgamedirectors
```
# select their movies
```{r}
russobasics <- filter(moviebasics,tconst%in%c('tt3498820','tt1843866','tt4154756','tt4154796'))
russobasics
```
# Add new colume to russorating.budget,boxoffice(domestic&international) data from BOX Office Mojo
```{r}
attach(russorating)
russorating$moviename <- c("Captain America:The Winter Soldier","Captain America: Civil War","Avengers: Infinity War","Avengers: Endgame")
russorating$movieyear <- c("2014","2016","2018","2019")
russorating$budget <- c("170000000","250000000","316000000","356000000")
russorating$domestic <- c("259766572","408084349","678815482","858373000")
russorating$international <- c("454654931","745211944","1369544272","1939427564")
russorating
```
# make a function to calculate returnmoney
# Add returnmoney to russorating
# make a function to calculate investor earnings.These four films have good earnings.
[1]  83291437 157201540 400330248 612096119
# Movies and films with a rating higher than 7.7 account for about 35% of all, according to the Russo Brothers’ movies ratings and final earnings, the next movie will also receive a good result.

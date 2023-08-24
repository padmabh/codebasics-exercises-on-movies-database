# codebasics-exercises-on-movies-database



1) Print all movie titles and release year for all Marvel Studios movies
	
   SELECT title, release_year from movies where studio="Marvel Studios"

2) Print all movies that have Avenger in their name

   SELECT * from movies where title LIKE '%Avenger%'

3) Print the year in which "The Godfather" move was released

   SELECT release_year from movies where title="The Godfather"

4) Print all distinct movie studios on Bollywood industry

   SELECT DISTINCT studio from movies where industry="Bollywood"



  
1) print all movies by the order of their release year (latest first)
   
   select * from movies order by release_year desc
   
2) all movies released this year in 2022
   
   select * from movies where release_year=2022  
   
3) ok now all the movies released after 2020

   select * from movies where release_year>2020  
   
4) all movies after year 2020 that has more than 8 rating

   select * from movies where release_year>2020 and imdb_rating>8
   
5) select all movies that are by marvel studios and hombale films

   select * from movies where studio in ("marvel studios", "hombale films")
   
6) select all thor movies by their release year

   select title, release_year from movies 
   where title like '%thor%' order by release_year asc

7) select all movies that are not from marvel studios

   select * from movies where studio!="marvel studios"



   

1) how many movies were released between 2015 and 2022

   select 
        count(*)
   from movies 
   where release_year between 2015 and 2022
   
2) print the max and min movie release year

   select 
      min(release_year) as min_year,
      max(release_year) as max_year
   from movies
   
3) print a year and how many movies were released in that year starting with latest year

   select release_year, count(*) as movies_count 
   from movies group by release_year order by release_year desc


  

1) Print profit % for all the movies 
   
   select 
        *, 
    (revenue-budget) as profit, 
    (revenue-budget)*100/budget as profit_pct 
   from financials
   



1) Show all the movies with their language names

   SELECT m.title, l.name FROM movies m 
   JOIN languages l USING (language_id)
   
2) Show all Telugu movie names (assuming you don't know language
id for Telugu)
  
   SELECT title	FROM movies m 
   LEFT JOIN languages l 
   ON m.language_id=l.language_id
   WHERE l.name="Telugu"

3) Show language and number of movies released in that language
   	SELECT 
            l.name, 
            COUNT(m.movie_id) as no_movies
	FROM languages l
	LEFT JOIN movies m USING (language_id)        
	GROUP BY language_id
	ORDER BY no_movies DESC;
   




1) Generate a report of all Hindi movies sorted by their revenue amount in millions. 
Print movie name, revenue, currency, and unit

	SELECT 
		title, revenue, currency, unit, 
			CASE 
					WHEN unit="Thousands" THEN ROUND(revenue/1000,2)
			WHEN unit="Billions" THEN ROUND(revenue*1000,2)
					ELSE revenue 
			END as revenue_mln
	FROM movies m
	JOIN financials f
			ON m.movie_id=f.movie_id
	JOIN languages l
			ON m.language_id=l.language_id
	WHERE l.name="Hindi"
	ORDER BY revenue_mln DESC

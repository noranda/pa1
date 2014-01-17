#Assignment: PA 1
#####Written by: Noranda Brown
#####Version: 2014.1.17

###Data
The data set, ml-100k, consists of 100,000 ratings of 1682 movies from 943 users downloaded from http://www.grouplens.org. The main data set u.data consists of 100,000 rows where each row has 4 tab-separated items: user_id, movie_id, rating, and timestamp.

###Program
**Class: MovieData**

`initialize` - Initializes instance variable: `@movies`

`load_data` - Reads in data from the original ml-100k files and stores movie objects in a hash.

`popularity(movie_id)` - Returns a number (0 - 100) that indicates the popularity (higher numbers are more popular). Note: Popularity is calculated by summing the ratings for the movie and normalizing the result. This takes into account not only the average rating, but also the number of times a movie has been reviewed. i.e. sum_ratings / num_ratings (to get the average rating) * num_ratings (to account for multiple reviews) = sum_ratings -> normalize

`popularity_list` - Generates a list of all movie_id’s ordered by decreasing popularity.

`similarity(user1, user2)` - Generates a number (0 - 100) which indicates the similarity in movie preference between user1 and user2 (higher numbers indicate greater similarity).

`most_similar(u, number_of_users = 5)` - Returns a list of the top number_of_users (default = 5) whose tastes are most similar to the tastes of user u.

`other_users(u)` - Private method that lists of all users except u.

**Class: Movie**

`initialize(movie_id)` - Initializes instance variables: `@movie_id`, `@user_ratings`, and `@sum_ratings`.

`add_rating(user_id, rating, timestamp)` - Adds a user_id, rating and timestamp to a movie.

`sum_ratings` - Returns the sum of all ratings for a movie.

`user_rated?(user_id)` - Returns true if user_id has rated a movie and false otherwise.

`user_rating(user_id)` - Returns the user rating from user_id for a movie.

`user_list` - Returns a list of users that have reviewed a movie.

**Class: UserRating**

`initialize(user_id, rating, timestamp)` - Initializes instance variables: `@user_id`, `@rating`, and `@timestamp`.

###Questions

1. Describe an algorithm to predict the ranking that a user U would give to a movie M assuming the user hasn’t already ranked the movie in the dataset.
```
predict_rating(user_id)
        sum = most_similar(user_id, 20).inject(0) { |sum, user| sum + user_rating(user) }
        count = most_similar(user_id, 20).inject(0) { |count, user| count + 1 if user_rated?(user) }
        (sum / count).to_i
```
This algorithm calculates the average rating of the top 20 most similar users.

2. Does your algorithms scale? What factors determine the execution time of your “most_similar” and “popularity_list” algorithms.

    While this algorithm would work, it would not scale very well, primarily due to the `most_similar` method which requires calculating the similarity between the user and *all other users*. Thus, the more users, the less efficient the algorithm.
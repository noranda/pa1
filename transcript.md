# Transcript

    2.1.0p0 :084 > require "./movie_data"
     => true
    2.1.0p0 :085 > m = MovieData.new
     => #<MovieData:0x00000102ad0590 @movies={}>
    2.1.0p0 :086 > m.load_data
     => #<File:ml-100k/u.data (closed)>
    2.1.0p0 :087 > m.popularity_list.take(10)
     => [50, 100, 181, 258, 174, 127, 286, 1, 98, 288]
    2.1.0p0 :088 > m.popularity_list.reverse.take(10)
     => [1561, 1570, 599, 1486, 1621, 1579, 1565, 1659, 1343, 1626]
    2.1.0p0 :089 > m.most_similar(1,20)
     => [155, 418, 812, 876, 105, 351, 273, 309, 895, 767, 516, 433, 662, 111, 691, 702, 237, 800, 803, 53]
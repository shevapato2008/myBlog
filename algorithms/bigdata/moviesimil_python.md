---
layout: algorithm
comments: true
mathjax: true
---

# Movie Similarities

<br>

## Data
---
Download `ml-100k` file from [here](https://github.com/shevapato2008/HadoopMapReduce_Python/tree/master/11.%20Movie%20Similarities/ml-100k "ml-100k") and `ml-1m` from [here](https://github.com/shevapato2008/HadoopMapReduce_Python/tree/master/11.%20Movie%20Similarities/ml-1m "ml-1m"). Then put them in the same folder as python code.

<br>

## Code & Analysis
---
The ordinary version: `MovieSimilarities.py`
```python
from mrjob.job import MRJob
from mrjob.step import MRStep
from math import sqrt

from itertools import combinations

class MovieSimilarities(MRJob):

    def configure_options(self):
        super(MovieSimilarities, self).configure_options()
        self.add_file_option('--items', help='Path to u.item')

    def load_movie_names(self):
        # Load database of movie names.
        self.movieNames = {}

        with open("u.item") as f:
            for line in f:
                fields = line.split('|')
                self.movieNames[int(fields[0])] = fields[1].decode('utf-8', 'ignore')

    def steps(self):
        return [
            MRStep(mapper=self.mapper_parse_input,
                    reducer=self.reducer_ratings_by_user),
            MRStep(mapper=self.mapper_create_item_pairs,
                    reducer=self.reducer_compute_similarity),
            MRStep(mapper=self.mapper_sort_similarities,
                    mapper_init=self.load_movie_names,
                    reducer=self.reducer_output_similarities)]

    def mapper_parse_input(self, key, line):
        # Outputs userID => (movieID, rating)
        (userID, movieID, rating, timestamp) = line.split('\t')
        yield userID, (movieID, float(rating))

    def reducer_ratings_by_user(self, user_id, itemRatings):
        # Group (item, rating) pairs by userID
        ratings = []
        for movieID, rating in itemRatings:
            ratings.append((movieID, rating))
        yield user_id, ratings

    def mapper_create_item_pairs(self, user_id, itemRatings):
        # Find every pair of movies each user has seen, and emit
        # each pair with its associated ratings

        # "combinations" finds every possible pair from the list of movies
        # this user viewed.
        for itemRating1, itemRating2 in combinations(itemRatings, 2):
            movieID1 = itemRating1[0]
            rating1 = itemRating1[1]
            movieID2 = itemRating2[0]
            rating2 = itemRating2[1]

            # Produce both orders so sims are bi-directional
            yield (movieID1, movieID2), (rating1, rating2)
            yield (movieID2, movieID1), (rating2, rating1)


    def cosine_similarity(self, ratingPairs):
        # Computes the cosine similarity metric between two
        # rating vectors.
        numPairs = 0
        sum_xx = sum_yy = sum_xy = 0
        for ratingX, ratingY in ratingPairs:
            sum_xx += ratingX * ratingX
            sum_yy += ratingY * ratingY
            sum_xy += ratingX * ratingY
            numPairs += 1

        numerator = sum_xy
        denominator = sqrt(sum_xx) * sqrt(sum_yy)

        score = 0
        if (denominator):
            score = (numerator / (float(denominator)))

        return (score, numPairs)

    def reducer_compute_similarity(self, moviePair, ratingPairs):
        # Compute the similarity score between the ratings vectors
        # for each movie pair viewed by multiple people

        # Output movie pair => score, number of co-ratings

        score, numPairs = self.cosine_similarity(ratingPairs)

        # Enforce a minimum score and minimum number of co-ratings
        # to ensure quality
        if (numPairs > 10 and score > 0.95):
            yield moviePair, (score, numPairs)

    def mapper_sort_similarities(self, moviePair, scores):
        # Shuffle things around so the key is (movie1, score)
        # so we have meaningfully sorted results.
        score, n = scores
        movie1, movie2 = moviePair

        yield (self.movieNames[int(movie1)], score), \
            (self.movieNames[int(movie2)], n)

    def reducer_output_similarities(self, movieScore, similarN):
        # Output the results.
        # Movie => Similar Movie, score, number of co-ratings
        movie1, score = movieScore
        for movie2, n in similarN:
            yield movie1, (movie2, score, n)


if __name__ == '__main__':
    MovieSimilarities.run()
```
The improved version for large dataset: `MovieSimilaritiesLarge.py`
```python
from mrjob.job import MRJob
from mrjob.step import MRStep
from math import sqrt

from itertools import combinations

class MovieSimilarities(MRJob):

    def configure_options(self):
        super(MovieSimilarities, self).configure_options()
        self.add_file_option('--items', help='Path to movies.dat')

    def load_movie_names(self):
        # Load database of movie names.
        self.movieNames = {}

        with open("movies.dat") as f:
            for line in f:
                fields = line.split('::')
                if (fields[0] != 'movieId'): # Skip first line
                    self.movieNames[int(fields[0])] = fields[1].decode('utf-8', 'ignore')

    def steps(self):
        return [
            MRStep(mapper=self.mapper_parse_input,
                    reducer=self.reducer_ratings_by_user),
            MRStep(mapper=self.mapper_create_item_pairs,
                    reducer=self.reducer_compute_similarity),
            MRStep(mapper=self.mapper_sort_similarities,
                    mapper_init=self.load_movie_names,
                    reducer=self.reducer_output_similarities)]

    def mapper_parse_input(self, key, line):
        # Outputs userID => (movieID, rating)
        (userID, movieID, rating, timestamp) = line.split('::')
        if (userID != 'userId'):  # Skip first line
            yield  userID, (movieID, float(rating))

    def reducer_ratings_by_user(self, user_id, itemRatings):
        #Group (item, rating) pairs by userID

        ratings = []
        for movieID, rating in itemRatings:
            ratings.append((movieID, rating))

        yield user_id, ratings

    def mapper_create_item_pairs(self, user_id, itemRatings):
        # Find every pair of movies each user has seen, and emit
        # each pair with its associated ratings

        # "combinations" finds every possible pair from the list of movies
        # this user viewed.
        for itemRating1, itemRating2 in combinations(itemRatings, 2):
            movieID1 = itemRating1[0]
            rating1 = itemRating1[1]
            movieID2 = itemRating2[0]
            rating2 = itemRating2[1]

            # Produce both orders so sims are bi-directional
            yield (movieID1, movieID2), (rating1, rating2)
            yield (movieID2, movieID1), (rating2, rating1)


    def cosine_similarity(self, ratingPairs):
        # Computes the cosine similarity metric between two
        # rating vectors.
        numPairs = 0
        sum_xx = sum_yy = sum_xy = 0
        for ratingX, ratingY in ratingPairs:
            sum_xx += ratingX * ratingX
            sum_yy += ratingY * ratingY
            sum_xy += ratingX * ratingY
            numPairs += 1

        numerator = sum_xy
        denominator = sqrt(sum_xx) * sqrt(sum_yy)

        score = 0
        if (denominator):
            score = (numerator / (float(denominator)))

        return (score, numPairs)

    def reducer_compute_similarity(self, moviePair, ratingPairs):
        # Compute the similarity score between the ratings vectors
        # for each movie pair viewed by multiple people

        # Output movie pair => score, number of co-ratings

        score, numPairs = self.cosine_similarity(ratingPairs)

        # Enforce a minimum score and minimum number of co-ratings
        # to ensure quality
        if (numPairs > 10 and score > 0.95):
            yield moviePair, (score, numPairs)

    def mapper_sort_similarities(self, moviePair, scores):
        # Shuffle things around so the key is (movie1, score)
        # so we have meaningfully sorted results.
        score, n = scores
        movie1, movie2 = moviePair

        yield (self.movieNames[int(movie1)], score), \
            (self.movieNames[int(movie2)], n)

    def reducer_output_similarities(self, movieScore, similarN):
        # Output the results.
        # Movie => Similar Movie, score, number of co-ratings
        movie1, score = movieScore
        for movie2, n in similarN:
            yield movie1, (movie2, score, n)


if __name__ == '__main__':
    MovieSimilarities.run()
```

<br>

## Run the Code
---
The ordinary version:

Execute the following command in the Python Console.
```shell
# To run locally:
!python MovieSimilarities.py --items=ml-100k/u.item ml-100k/u.data > sims.txt

# To run on a single EMR node:
!python MovieSimilarities.py -r emr --items=ml-100k/u.item ml-100k/u.data

# To run on 4 EMR nodes:
!python MovieSimilarities.py -r emr --num-ec2-instances=4 --items=ml-100k/u.item ml-100k/u.data

# Troubleshooting EMR jobs (subsitute your job ID):
!python -m mrjob.tools.emr.fetch_logs --find-failure j-1NXMMBNEQHAFT
```
The result `sims.txt` looks like the following.
```
"101 Dalmatians (1996)"	["City Hall (1996)", 0.9500888801011946, 22]
"101 Dalmatians (1996)"	["Hunt for Red October, The (1990)", 0.950775494380866, 53]
"101 Dalmatians (1996)"	["Shadowlands (1993)", 0.9508168774138372, 13]
"101 Dalmatians (1996)"	["Being There (1979)", 0.9508790426232138, 21]
"101 Dalmatians (1996)"	["Angels in the Outfield (1994)", 0.9510664125512855, 16]
"101 Dalmatians (1996)"	["Homeward Bound: The Incredible Journey (1993)", 0.9511741749756156, 26]
"101 Dalmatians (1996)"	["Cool Hand Luke (1967)", 0.9511903665799749, 24]
"101 Dalmatians (1996)"	["Mortal Kombat (1995)", 0.9515236577553171, 12]
"101 Dalmatians (1996)"	["Michael (1996)", 0.9520552525053347, 38]
"101 Dalmatians (1996)"	["Raging Bull (1980)", 0.9522904718924488, 11]
"101 Dalmatians (1996)"	["Peacemaker, The (1997)", 0.9523038333920102, 12]
"101 Dalmatians (1996)"	["Fan, The (1996)", 0.9523665767109106, 19]
"101 Dalmatians (1996)"	["She's the One (1996)", 0.9531718551058114, 15]
"101 Dalmatians (1996)"	["Bullets Over Broadway (1994)", 0.953742320097803, 14]
... ...
```
The result `sims-4-machines.txt` looks like below:
```
"101 Dalmatians (1996)"	["City Hall (1996)", 0.9500888801011946, 22]
"101 Dalmatians (1996)"	["Hunt for Red October, The (1990)", 0.950775494380866, 53]
"101 Dalmatians (1996)"	["Shadowlands (1993)", 0.9508168774138372, 13]
"101 Dalmatians (1996)"	["Mortal Kombat (1995)", 0.9515236577553171, 12]
"101 Dalmatians (1996)"	["Raging Bull (1980)", 0.9522904718924488, 11]
"101 Dalmatians (1996)"	["Fan, The (1996)", 0.9523665767109106, 19]
"101 Dalmatians (1996)"	["Paper, The (1994)", 0.9538151752617265, 12]
"101 Dalmatians (1996)"	["Apartment, The (1960)", 0.9563830905993714, 13]
"101 Dalmatians (1996)"	["Eye for an Eye (1996)", 0.9585225256084312, 11]
"101 Dalmatians (1996)"	["Parent Trap, The (1961)", 0.9629801022299663, 27]
"101 Dalmatians (1996)"	["Pete's Dragon (1977)", 0.965198954908464, 17]
"101 Dalmatians (1996)"	["Miller's Crossing (1990)", 0.9719273929377941, 11]
"101 Dalmatians (1996)"	["Black Beauty (1994)", 0.9763455284972368, 11]
"12 Angry Men (1957)"	["Powder (1995)", 0.9500183596757119, 16]
"12 Angry Men (1957)"	["Young Guns (1988)", 0.9507782369774163, 33]
"12 Angry Men (1957)"	["While You Were Sleeping (1995)", 0.9522780584047686, 45]
"12 Angry Men (1957)"	["Mallrats (1995)", 0.9522921669672343, 14]
"12 Angry Men (1957)"	["Star Trek: Generations (1994)", 0.9523061952537475, 35]
... ...
```

The improved version for dealing with large data:

Execute the following command in the Python Console.
```shell
# To run on 20 EMR nodes:
!python MovieSimilaritiesLarge.py -r emr --num-ec2-instances=20 --items=ml-1m/movies.dat ml-1m/ratings.dat

# Troubleshooting EMR jobs (substitute your job ID):
!python -m mrjob.tools.emr.fetch_logs --find-failure j-1NXMMBNEQHAFT
```

<br><br>

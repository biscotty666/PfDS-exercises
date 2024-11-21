# MovieLens 1M Dataset 

[PfDA](http://127.0.0.1:8888/lab?token=fd8d3c0aad33d45f9ac222181dcb56a36c8190ba76598570)

## Loading data


```python
import pandas as pd 

unames = ["user_id", "gender", "age", "occupation", "zip"]
users = pd.read_table("data/users.dat", sep="::", 
                     header=None, names=unames, engine="python")
```


```python
rnames = ["user_id", "movie_id", "rating", "timestamp"]
ratings = pd.read_table("data/ratings.dat", sep="::", 
                     header=None, names=rnames, engine="python")

mnames = ["movie_id", "title", "genres"]
movies = pd.read_table("data/movies.dat", sep="::", 
                     header=None, names=mnames, engine="python")
```


```python
users.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>gender</th>
      <th>age</th>
      <th>occupation</th>
      <th>zip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>F</td>
      <td>1</td>
      <td>10</td>
      <td>48067</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>M</td>
      <td>56</td>
      <td>16</td>
      <td>70072</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>M</td>
      <td>25</td>
      <td>15</td>
      <td>55117</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>M</td>
      <td>45</td>
      <td>7</td>
      <td>02460</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>M</td>
      <td>25</td>
      <td>20</td>
      <td>55455</td>
    </tr>
  </tbody>
</table>
</div>




```python
ratings.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1193</td>
      <td>5</td>
      <td>978300760</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>661</td>
      <td>3</td>
      <td>978302109</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>914</td>
      <td>3</td>
      <td>978301968</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>3408</td>
      <td>4</td>
      <td>978300275</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2355</td>
      <td>5</td>
      <td>978824291</td>
    </tr>
  </tbody>
</table>
</div>




```python
movies.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie_id</th>
      <th>title</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Animation|Children's|Comedy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Jumanji (1995)</td>
      <td>Adventure|Children's|Fantasy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Grumpier Old Men (1995)</td>
      <td>Comedy|Romance</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Waiting to Exhale (1995)</td>
      <td>Comedy|Drama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Father of the Bride Part II (1995)</td>
      <td>Comedy</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Since column names match, pandas will know how to relate them 
data = pd.merge(pd.merge(ratings, users), movies)
data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>movie_id</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>gender</th>
      <th>age</th>
      <th>occupation</th>
      <th>zip</th>
      <th>title</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1193</td>
      <td>5</td>
      <td>978300760</td>
      <td>F</td>
      <td>1</td>
      <td>10</td>
      <td>48067</td>
      <td>One Flew Over the Cuckoo's Nest (1975)</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>661</td>
      <td>3</td>
      <td>978302109</td>
      <td>F</td>
      <td>1</td>
      <td>10</td>
      <td>48067</td>
      <td>James and the Giant Peach (1996)</td>
      <td>Animation|Children's|Musical</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>914</td>
      <td>3</td>
      <td>978301968</td>
      <td>F</td>
      <td>1</td>
      <td>10</td>
      <td>48067</td>
      <td>My Fair Lady (1964)</td>
      <td>Musical|Romance</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>3408</td>
      <td>4</td>
      <td>978300275</td>
      <td>F</td>
      <td>1</td>
      <td>10</td>
      <td>48067</td>
      <td>Erin Brockovich (2000)</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2355</td>
      <td>5</td>
      <td>978824291</td>
      <td>F</td>
      <td>1</td>
      <td>10</td>
      <td>48067</td>
      <td>Bug's Life, A (1998)</td>
      <td>Animation|Children's|Comedy</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1000204</th>
      <td>6040</td>
      <td>1091</td>
      <td>1</td>
      <td>956716541</td>
      <td>M</td>
      <td>25</td>
      <td>6</td>
      <td>11106</td>
      <td>Weekend at Bernie's (1989)</td>
      <td>Comedy</td>
    </tr>
    <tr>
      <th>1000205</th>
      <td>6040</td>
      <td>1094</td>
      <td>5</td>
      <td>956704887</td>
      <td>M</td>
      <td>25</td>
      <td>6</td>
      <td>11106</td>
      <td>Crying Game, The (1992)</td>
      <td>Drama|Romance|War</td>
    </tr>
    <tr>
      <th>1000206</th>
      <td>6040</td>
      <td>562</td>
      <td>5</td>
      <td>956704746</td>
      <td>M</td>
      <td>25</td>
      <td>6</td>
      <td>11106</td>
      <td>Welcome to the Dollhouse (1995)</td>
      <td>Comedy|Drama</td>
    </tr>
    <tr>
      <th>1000207</th>
      <td>6040</td>
      <td>1096</td>
      <td>4</td>
      <td>956715648</td>
      <td>M</td>
      <td>25</td>
      <td>6</td>
      <td>11106</td>
      <td>Sophie's Choice (1982)</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>1000208</th>
      <td>6040</td>
      <td>1097</td>
      <td>4</td>
      <td>956715569</td>
      <td>M</td>
      <td>25</td>
      <td>6</td>
      <td>11106</td>
      <td>E.T. the Extra-Terrestrial (1982)</td>
      <td>Children's|Drama|Fantasy|Sci-Fi</td>
    </tr>
  </tbody>
</table>
<p>1000209 rows × 10 columns</p>
</div>




```python
data.iloc[0]
```




    user_id                                            1
    movie_id                                        1193
    rating                                             5
    timestamp                                  978300760
    gender                                             F
    age                                                1
    occupation                                        10
    zip                                            48067
    title         One Flew Over the Cuckoo's Nest (1975)
    genres                                         Drama
    Name: 0, dtype: object



## Statistics

__Mean rating by gender__


```python
mean_ratings = data.pivot_table("rating", index="title", 
                               columns="gender", aggfunc="mean")
mean_ratings.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>gender</th>
      <th>F</th>
      <th>M</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>$1,000,000 Duck (1971)</th>
      <td>3.375000</td>
      <td>2.761905</td>
    </tr>
    <tr>
      <th>'Night Mother (1986)</th>
      <td>3.388889</td>
      <td>3.352941</td>
    </tr>
    <tr>
      <th>'Til There Was You (1997)</th>
      <td>2.675676</td>
      <td>2.733333</td>
    </tr>
    <tr>
      <th>'burbs, The (1989)</th>
      <td>2.793478</td>
      <td>2.962085</td>
    </tr>
    <tr>
      <th>...And Justice for All (1979)</th>
      <td>3.828571</td>
      <td>3.689024</td>
    </tr>
  </tbody>
</table>
</div>



Filter down to movies that recived at least 250 ratings (arbitrary). First use grouping by title and size to find out how many ratings for each movie.


```python
ratings_by_title = data.groupby("title").size()
ratings_by_title.head()
```




    title
    $1,000,000 Duck (1971)            37
    'Night Mother (1986)              70
    'Til There Was You (1997)         52
    'burbs, The (1989)               303
    ...And Justice for All (1979)    199
    dtype: int64




```python
active_titles = ratings_by_title.index[ratings_by_title >= 250]
```


```python
active_titles
```




    Index([''burbs, The (1989)', '10 Things I Hate About You (1999)',
           '101 Dalmatians (1961)', '101 Dalmatians (1996)', '12 Angry Men (1957)',
           '13th Warrior, The (1999)', '2 Days in the Valley (1996)',
           '20,000 Leagues Under the Sea (1954)', '2001: A Space Odyssey (1968)',
           '2010 (1984)',
           ...
           'X-Men (2000)', 'Year of Living Dangerously (1982)',
           'Yellow Submarine (1968)', 'You've Got Mail (1998)',
           'Young Frankenstein (1974)', 'Young Guns (1988)',
           'Young Guns II (1990)', 'Young Sherlock Holmes (1985)',
           'Zero Effect (1998)', 'eXistenZ (1999)'],
          dtype='object', name='title', length=1216)



The index can be used to pull out those movies only.


```python
mean_ratings = mean_ratings.loc[active_titles]
mean_ratings
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>gender</th>
      <th>F</th>
      <th>M</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>'burbs, The (1989)</th>
      <td>2.793478</td>
      <td>2.962085</td>
    </tr>
    <tr>
      <th>10 Things I Hate About You (1999)</th>
      <td>3.646552</td>
      <td>3.311966</td>
    </tr>
    <tr>
      <th>101 Dalmatians (1961)</th>
      <td>3.791444</td>
      <td>3.500000</td>
    </tr>
    <tr>
      <th>101 Dalmatians (1996)</th>
      <td>3.240000</td>
      <td>2.911215</td>
    </tr>
    <tr>
      <th>12 Angry Men (1957)</th>
      <td>4.184397</td>
      <td>4.328421</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Young Guns (1988)</th>
      <td>3.371795</td>
      <td>3.425620</td>
    </tr>
    <tr>
      <th>Young Guns II (1990)</th>
      <td>2.934783</td>
      <td>2.904025</td>
    </tr>
    <tr>
      <th>Young Sherlock Holmes (1985)</th>
      <td>3.514706</td>
      <td>3.363344</td>
    </tr>
    <tr>
      <th>Zero Effect (1998)</th>
      <td>3.864407</td>
      <td>3.723140</td>
    </tr>
    <tr>
      <th>eXistenZ (1999)</th>
      <td>3.098592</td>
      <td>3.289086</td>
    </tr>
  </tbody>
</table>
<p>1216 rows × 2 columns</p>
</div>




```python
top_female_ratings = mean_ratings.sort_values("F", ascending=False)
top_female_ratings.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>gender</th>
      <th>F</th>
      <th>M</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Close Shave, A (1995)</th>
      <td>4.644444</td>
      <td>4.473795</td>
    </tr>
    <tr>
      <th>Wrong Trousers, The (1993)</th>
      <td>4.588235</td>
      <td>4.478261</td>
    </tr>
    <tr>
      <th>Sunset Blvd. (a.k.a. Sunset Boulevard) (1950)</th>
      <td>4.572650</td>
      <td>4.464589</td>
    </tr>
    <tr>
      <th>Wallace &amp; Gromit: The Best of Aardman Animation (1996)</th>
      <td>4.563107</td>
      <td>4.385075</td>
    </tr>
    <tr>
      <th>Schindler's List (1993)</th>
      <td>4.562602</td>
      <td>4.491415</td>
    </tr>
  </tbody>
</table>
</div>



## Measuring disagreement


```python
mean_ratings["diff"] = mean_ratings["M"] - mean_ratings["F"]
sorted_by_diff = mean_ratings.sort_values("diff")
sorted_by_diff.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>gender</th>
      <th>F</th>
      <th>M</th>
      <th>diff</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Dirty Dancing (1987)</th>
      <td>3.790378</td>
      <td>2.959596</td>
      <td>-0.830782</td>
    </tr>
    <tr>
      <th>Jumpin' Jack Flash (1986)</th>
      <td>3.254717</td>
      <td>2.578358</td>
      <td>-0.676359</td>
    </tr>
    <tr>
      <th>Grease (1978)</th>
      <td>3.975265</td>
      <td>3.367041</td>
      <td>-0.608224</td>
    </tr>
    <tr>
      <th>Little Women (1994)</th>
      <td>3.870588</td>
      <td>3.321739</td>
      <td>-0.548849</td>
    </tr>
    <tr>
      <th>Steel Magnolias (1989)</th>
      <td>3.901734</td>
      <td>3.365957</td>
      <td>-0.535777</td>
    </tr>
  </tbody>
</table>
</div>




```python
sorted_by_diff[::-1].head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>gender</th>
      <th>F</th>
      <th>M</th>
      <th>diff</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Good, The Bad and The Ugly, The (1966)</th>
      <td>3.494949</td>
      <td>4.221300</td>
      <td>0.726351</td>
    </tr>
    <tr>
      <th>Kentucky Fried Movie, The (1977)</th>
      <td>2.878788</td>
      <td>3.555147</td>
      <td>0.676359</td>
    </tr>
    <tr>
      <th>Dumb &amp; Dumber (1994)</th>
      <td>2.697987</td>
      <td>3.336595</td>
      <td>0.638608</td>
    </tr>
    <tr>
      <th>Longest Day, The (1962)</th>
      <td>3.411765</td>
      <td>4.031447</td>
      <td>0.619682</td>
    </tr>
    <tr>
      <th>Cable Guy, The (1996)</th>
      <td>2.250000</td>
      <td>2.863787</td>
      <td>0.613787</td>
    </tr>
  </tbody>
</table>
</div>



## Statistical measurement of disagreement


```python
rating_std_by_title = data.groupby("title")["rating"].std()
```


```python
rating_std_by_title = rating_std_by_title.loc[active_titles]
rating_std_by_title.head()
```




    title
    'burbs, The (1989)                   1.107760
    10 Things I Hate About You (1999)    0.989815
    101 Dalmatians (1961)                0.982103
    101 Dalmatians (1996)                1.098717
    12 Angry Men (1957)                  0.812731
    Name: rating, dtype: float64




```python
rating_std_by_title.sort_values(ascending=False)[:10]
```




    title
    Dumb & Dumber (1994)                     1.321333
    Blair Witch Project, The (1999)          1.316368
    Natural Born Killers (1994)              1.307198
    Tank Girl (1995)                         1.277695
    Rocky Horror Picture Show, The (1975)    1.260177
    Eyes Wide Shut (1999)                    1.259624
    Evita (1996)                             1.253631
    Billy Madison (1995)                     1.249970
    Fear and Loathing in Las Vegas (1998)    1.246408
    Bicentennial Man (1999)                  1.245533
    Name: rating, dtype: float64



Movie genres are one field with multiple values separated by `|`


```python
movies["genres"].head()
```




    0     Animation|Children's|Comedy
    1    Adventure|Children's|Fantasy
    2                  Comedy|Romance
    3                    Comedy|Drama
    4                          Comedy
    Name: genres, dtype: object




```python
movies["genres"].head().str.split("|")
```




    0     [Animation, Children's, Comedy]
    1    [Adventure, Children's, Fantasy]
    2                   [Comedy, Romance]
    3                     [Comedy, Drama]
    4                            [Comedy]
    Name: genres, dtype: object



## Create a list in a dataframe column


```python
movies["genres"] = movies.pop("genres").str.split("|")
movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie_id</th>
      <th>title</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>[Animation, Children's, Comedy]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Jumanji (1995)</td>
      <td>[Adventure, Children's, Fantasy]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Grumpier Old Men (1995)</td>
      <td>[Comedy, Romance]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Waiting to Exhale (1995)</td>
      <td>[Comedy, Drama]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Father of the Bride Part II (1995)</td>
      <td>[Comedy]</td>
    </tr>
  </tbody>
</table>
</div>




```python
movies["genres"][1]
```




    ['Adventure', "Children's", 'Fantasy']




```python
movies_exploded = movies.explode("genres")
movies_exploded[:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie_id</th>
      <th>title</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Animation</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Children's</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Comedy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Jumanji (1995)</td>
      <td>Adventure</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Jumanji (1995)</td>
      <td>Children's</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Jumanji (1995)</td>
      <td>Fantasy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Grumpier Old Men (1995)</td>
      <td>Comedy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Grumpier Old Men (1995)</td>
      <td>Romance</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Waiting to Exhale (1995)</td>
      <td>Comedy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Waiting to Exhale (1995)</td>
      <td>Drama</td>
    </tr>
  </tbody>
</table>
</div>




```python
ratings_with_genre = pd.merge(pd.merge(movies_exploded, ratings), 
                                       users)
```


```python
ratings_with_genre.iloc[0]
```




    movie_id                     1
    title         Toy Story (1995)
    genres               Animation
    user_id                      1
    rating                       5
    timestamp            978824268
    gender                       F
    age                          1
    occupation                  10
    zip                      48067
    Name: 0, dtype: object




```python
genres_ratings = (ratings_with_genre.groupby(["genres", "age"])
                             ["rating"].mean()
                             .unstack("age"))
genres_ratings[:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>age</th>
      <th>1</th>
      <th>18</th>
      <th>25</th>
      <th>35</th>
      <th>45</th>
      <th>50</th>
      <th>56</th>
    </tr>
    <tr>
      <th>genres</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Action</th>
      <td>3.506385</td>
      <td>3.447097</td>
      <td>3.453358</td>
      <td>3.538107</td>
      <td>3.528543</td>
      <td>3.611333</td>
      <td>3.610709</td>
    </tr>
    <tr>
      <th>Adventure</th>
      <td>3.449975</td>
      <td>3.408525</td>
      <td>3.443163</td>
      <td>3.515291</td>
      <td>3.528963</td>
      <td>3.628163</td>
      <td>3.649064</td>
    </tr>
    <tr>
      <th>Animation</th>
      <td>3.476113</td>
      <td>3.624014</td>
      <td>3.701228</td>
      <td>3.740545</td>
      <td>3.734856</td>
      <td>3.780020</td>
      <td>3.756233</td>
    </tr>
    <tr>
      <th>Children's</th>
      <td>3.241642</td>
      <td>3.294257</td>
      <td>3.426873</td>
      <td>3.518423</td>
      <td>3.527593</td>
      <td>3.556555</td>
      <td>3.621822</td>
    </tr>
    <tr>
      <th>Comedy</th>
      <td>3.497491</td>
      <td>3.460417</td>
      <td>3.490385</td>
      <td>3.561984</td>
      <td>3.591789</td>
      <td>3.646868</td>
      <td>3.650949</td>
    </tr>
    <tr>
      <th>Crime</th>
      <td>3.710170</td>
      <td>3.668054</td>
      <td>3.680321</td>
      <td>3.733736</td>
      <td>3.750661</td>
      <td>3.810688</td>
      <td>3.832549</td>
    </tr>
    <tr>
      <th>Documentary</th>
      <td>3.730769</td>
      <td>3.865865</td>
      <td>3.946690</td>
      <td>3.953747</td>
      <td>3.966521</td>
      <td>3.908108</td>
      <td>3.961538</td>
    </tr>
    <tr>
      <th>Drama</th>
      <td>3.794735</td>
      <td>3.721930</td>
      <td>3.726428</td>
      <td>3.782512</td>
      <td>3.784356</td>
      <td>3.878415</td>
      <td>3.933465</td>
    </tr>
    <tr>
      <th>Fantasy</th>
      <td>3.317647</td>
      <td>3.353778</td>
      <td>3.452484</td>
      <td>3.482301</td>
      <td>3.532468</td>
      <td>3.581570</td>
      <td>3.532700</td>
    </tr>
    <tr>
      <th>Film-Noir</th>
      <td>4.145455</td>
      <td>3.997368</td>
      <td>4.058725</td>
      <td>4.064910</td>
      <td>4.105376</td>
      <td>4.175401</td>
      <td>4.125932</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

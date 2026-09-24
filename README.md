# Content-Based-Music-Recommendation-System
A content-based recommendation system that recommends songs based on their **audio characteristics and artist genres**. The system combines numerical audio features with text-based genre information and uses **cosine similarity** to identify similar songs.

## Project Workflow
Dataset → EDA → Data Cleaning → Feature Engineering → TF-IDF → Feature Combination → Cosine Similarity → Recommendation

## Dataset
The dataset contains 19 columns, including:
* Track URI
* Track Name
* Artist Name(s)
* Album Name
* Album Release Date
* Popularity
* Artist Genres
* Danceability
* Energy
* Key
* Loudness
* Mode
* Speechiness
* Acousticness
* Instrumentalness
* Liveness
* Valence
* Tempo
* Time Signature

After data cleaning, the dataset contained 4,991 songs, with no columns dropped.

## Features Used in the Model
Only a subset of columns was used to build the recommendation system:
* 9 numerical audio features: Danceability, Energy, Loudness, Speechiness, Acousticness, Instrumentalness, Liveness, Valence, Tempo
* Artist Genres (text-based, transformed via TF-IDF)

## Exploratory Data Analysis
EDA was performed to examine:
* Dataset structure
* Duplicate records
* Missing values
* Numerical feature distributions
* Correlations between audio features
* Consistency of categorical values

A total of **9 duplicate records** were identified and removed. Missing values in numerical columns were handled using the **median**, while missing categorical values were filled using the **mode**. The analysis also examined correlations between audio features. Most features showed low to moderate correlations, allowing multiple characteristics to be used in the recommendation system.

## Feature Engineering
The recommendation system combines two types of information:

### Audio Features
Nine numerical audio features were selected:
```text
Danceability
Energy
Loudness
Speechiness
Acousticness
Instrumentalness
Liveness
Valence
Tempo
```

These features were standardized using **StandardScaler**.

### Artist Genres
The `Artist Genres` column contains text-based genre information. The genre text was transformed into numerical representations using **TF-IDF (Term Frequency-Inverse Document Frequency)** with English stop words removed.

## Feature Combination
The standardized audio features and TF-IDF genre representations were combined into a single feature matrix.
```text
Audio Features
       +
Genre Features
       ↓
Combined Feature Matrix
```

This allows the system to consider both the musical characteristics and genre information of each song.

## Similarity Calculation
**Cosine similarity** was used to measure the similarity between songs based on their combined feature representations. For a selected song, the system:
1. Finds the song in the dataset.
2. Retrieves its similarity scores against other songs.
3. Sorts songs based on similarity.
4. Excludes the selected song itself.
5. Returns the top 5 most similar songs.

## Recommendation Function
The main recommendation function is:
```python
recommend_songs(song_title, n=5)
```

The function accepts a song title and returns recommended songs with:
* Track Name
* Artist Name(s)
* Album Name
* Artist Genres

If the selected song is not available in the dataset, the function returns a `"Song not found in the dataset"` message.

## Example
Example inputs were tested using multiple songs from the dataset to verify that the recommendation function could generate similar songs based on the combined feature representation.

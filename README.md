# Content-Based Movie Recommendation System

## Project Goal

The objective of this project is to build a content-based movie recommendation system. Given a movie title, the system recommends five other movies that are most similar in content.

## Approach

This project utilizes a content-based filtering approach, which means it recommends movies based on their inherent properties rather than user ratings. The entire process was developed using Python, Pandas for data manipulation, and Scikit-learn for feature extraction.

**1. Data Loading and Merging**
* The project uses the **TMDB 5000 Movie Dataset**, which is split into two CSV files: `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv`.
* These two datasets were merged into a single dataframe based on the movie title, creating a comprehensive source of information for each film.

**2. Feature Selection and Preprocessing**
To determine movie similarity, a specific set of content-based features was selected:
* `genres`
* `keywords`
* `overview`
* `cast` (top 3 actors)
* `crew` (specifically the director)

These features were then meticulously cleaned and transformed:
* **JSON Parsing:** The `genres`, `keywords`, `cast`, and `crew` columns were originally in a JSON format. Helper functions were created to parse these strings and extract the relevant information (e.g., actor names, director's name, genre labels).
* **Consolidation:** To prevent the model from treating multi-word names (like "Sam Worthington" and "Sam Mendes") as separate entities, all spaces were removed (e.g., "SamWorthington").
* **Tag Creation:** All the selected, cleaned features for each movie were combined into a single text block, or "tag." This tag serves as a comprehensive content summary for each film.

**3. Feature Extraction (Vectorization)**
* To convert the text-based tags into a numerical format that a machine learning model can understand, the **`CountVectorizer`** from Scikit-learn was used.
* Each movie's tag was converted into a vector of 5000 dimensions, where each dimension corresponds to the frequency of a particular word (after removing common English stop words).
* This process resulted in a large matrix where each row represents a movie and each column represents a word in the vocabulary.

**4. Similarity Calculation**
* With all movies represented as numerical vectors, the **cosine similarity** was calculated between every pair of movies.
* Cosine similarity measures the cosine of the angle between two vectors, providing a metric of how similar they are in "content space." A value closer to 1 indicates high similarity, while a value closer to 0 indicates low similarity.

**5. Recommendation Function**
A function was created that takes a movie title as input, finds its corresponding vector, and calculates its similarity score against all other movies. It then sorts these scores and returns the titles of the five most similar movies.

---

## Key Findings and Results

The system is fully functional and provides logical recommendations. The content-based approach ensures that the suggestions are based on shared genres, plot keywords, actors, and directors.

**Example Recommendation:**
When the system is asked to recommend movies similar to **'Spectre'**, it produces the following list:

1.  Quantum of Solace
2.  Never Say Never Again
3.  Skyfall
4.  From Russia with Love
5.  Thunderball

**Interpretation:**
This is an excellent set of recommendations. All the suggested movies are part of the **James Bond franchise**, just like 'Spectre'. This confirms that the system successfully identified the most important tags, such as keywords like 'spy' and 'secretagent', the lead actor 'DanielCraig', and the shared genre of 'Action'.

---

## Conclusion

This project successfully demonstrates the implementation of a content-based movie recommendation system. By converting movie attributes into a high-dimensional vector space and using cosine similarity, the model is able to generate relevant and contextually appropriate movie suggestions. The methodology is robust and can be easily extended with additional features or applied to different types of media.

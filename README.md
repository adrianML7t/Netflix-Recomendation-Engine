# 🎬 Netflix Content Recommendation Engine

[cite_start]This project implements a content-based recommendation system using the Netflix titles dataset. [cite_start]It leverages **Natural Language Processing (NLP)** and **Cosine Similarity** to suggest movies and TV shows based on their thematic metadata[cite: 55, 56, 59].

## 📊 Project Overview
[cite_start]The engine analyzes over 8,800 titles to provide relevant suggestions by transforming text descriptions and categories into mathematical vectors[cite: 16, 18, 64]. [cite_start]By measuring the distance between these vectors, the system identifies titles with the highest thematic overlap[cite: 56, 58, 66].

## 🛠️ Tech Stack
* [cite_start]**Data Manipulation**: Pandas, NumPy.
* [cite_start]**Machine Learning**: Scikit-Learn (`TfidfVectorizer`, `cosine_similarity`)[cite: 15, 56].
* [cite_start]**Visualization**: Seaborn, Matplotlib[cite: 14, 20].

## ⚙️ Technical Workflow

### 1. Data Cleaning and Feature Selection
* [cite_start]The original dataset is loaded from `netflix_titles.csv`.
* [cite_start]Null values are dropped to ensure data integrity.
* [cite_start]The model focuses on the `description` and `listed_in` (genre) columns to capture the essence of the content[cite: 1, 2].

### 2. Feature Engineering: The "Soup"
* [cite_start]A custom function, `create_soup`, concatenates the selected text features into a single string for each entry[cite: 1, 3].
* [cite_start]All text is normalized to lowercase to ensure the vectorizer treats words like "Drama" and "drama" as identical[cite: 4].



### 3. TF-IDF Vectorization
* [cite_start]The system uses `TfidfVectorizer` with English stop words to convert text into a numerical matrix[cite: 15, 16].
* [cite_start]**Matrix Shape**: The resulting matrix contains 8,807 rows and 18,477 unique word columns[cite: 18].
* [cite_start]Weights are assigned to words based on their frequency within a document versus the entire dataset[cite: 13, 14].

### 4. Visual Analysis (Heatmap)
[cite_start]A heatmap was generated to visualize the most unique words (tokens) across a sample of titles, such as "orleans", "mysteries", and "reality"[cite: 31, 32, 34].



---

## 🚀 Recommendation Logic
[cite_start]The core of the engine is the `search_engine()` function[cite: 64]. [cite_start]It calculates the **Cosine Similarity** between titles, creating a 1:1 similarity map[cite: 56, 58].

### Usage Example
When a user inputs a title, the system:
1.  [cite_start]Retrieves the index of the requested movie[cite: 65].
2.  [cite_start]Extracts the similarity scores for that specific index[cite: 66].
3.  [cite_start]Sorts all titles from most to least similar[cite: 66].
4.  [cite_start]Returns the top 5 matches, excluding the original title[cite: 66].

### Implementation Details
[cite_start]The results are presented in a stylized DataFrame using a Red color gradient to highlight match strength[cite: 73, 74].

```python
# Example of the final engine logic
def search_engine():
    movie = input("Choose a movie and get similar ones: ")
    idx = df_indexes[movie]
    sim_scores = sorted(list(enumerate(cos_res[idx])), key=lambda x: x[1], reverse=True)
    top_matches = sim_scores[1:6]
    # ... formatting and returning styled results

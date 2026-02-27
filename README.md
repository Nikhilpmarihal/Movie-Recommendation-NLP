# 🎬 Neural Cinema

## Scalable Movie Recommendations with FastAPI & NLP

Neural Cinema is a **production-grade, content-based movie recommendation system** engineered for scalability, responsiveness, and clean modular design.

Built with **TF-IDF powered NLP**, served through **FastAPI**, and delivered via an intuitive **Streamlit interface**, the platform provides real-time, intelligent movie discovery with dynamic content integration from TMDB.

---

## 🚀 Executive Summary

Neural Cinema transforms raw movie metadata into meaningful recommendations using advanced text processing and similarity modeling.

The system is designed with:

* ⚡ **Low-latency API performance**
* 🧠 **Robust NLP processing pipeline**
* 🧩 **Modular architecture for long-term maintainability**
* 🌍 **Cloud deployment readiness**
* 🎥 **Real-time poster & metadata integration via TMDB API**

This architecture ensures high reliability, scalability, and seamless user experience.

---

## ✨ Core Features

### 🎯 Content-Based Filtering

* Recommends movies based on similarity in:

  * Overviews
  * Genres
  * Taglines
* Powered by TF-IDF vectorization and cosine similarity.

### 🧠 Advanced NLP Pipeline

* Lowercasing and punctuation removal
* Tokenization
* Stopword removal
* Lemmatization using WordNet
* Regex-based cleaning

### ⚡ High-Performance Backend

* Built with FastAPI for asynchronous processing
* Pydantic for strict data validation
* Pre-loaded Pickle models for ultra-fast inference

### 🖥️ Interactive Frontend

* Streamlit UI for:

  * Search functionality
  * Trending content display
  * Recommendation visualization
  * Dynamic poster rendering

### 🎥 TMDB API Integration

* Real-time fetching of:

  * Movie posters
  * Backdrops
  * Ratings
  * Popular/trending movies

---

## 🛠️ Tech Stack

| Layer                | Technologies                                |
| -------------------- | ------------------------------------------- |
| **Language**         | Python 3.11.9                               |
| **Data Processing**  | Pandas, NumPy                               |
| **Machine Learning** | Scikit-Learn (TF-IDF, Cosine Similarity)    |
| **NLP**              | NLTK (Stopwords, WordNet Lemmatizer), Regex |
| **Backend**          | FastAPI, Uvicorn, Pydantic                  |
| **Frontend**         | Streamlit                                   |
| **Deployment**       | Render (API), Streamlit Community Cloud     |
| **External API**     | TMDB API                                    |

---

## 🧠 System Architecture

```
User (Streamlit UI)
        ↓
FastAPI Backend
        ↓
Preloaded TF-IDF Model
        ↓
Cosine Similarity Engine
        ↓
Top-N Ranked Recommendations
        ↓
TMDB API (Posters & Metadata)
        ↓
Rendered Results in UI
```

---

## 🔬 How It Works

### 1️⃣ Data Preprocessing

* Dataset: TMDB Movies dataset (~45,000 movies)
* Removed duplicates and null values
* Combined:

  * `overview`
  * `genres`
  * `tagline`
* Created a unified feature: **tags**

---

### 2️⃣ NLP Processing Pipeline

The `tags` column undergoes:

* Lowercasing
* Special character removal
* Stopword filtering
* Lemmatization

This ensures semantic consistency and dimensional efficiency.

---

### 3️⃣ TF-IDF Vectorization

* Converts text into numerical representation
* Vocabulary size limited to **50,000 features**
* Captures importance of terms using:

  * Term Frequency (TF)
  * Inverse Document Frequency (IDF)

---

### 4️⃣ Cosine Similarity Scoring

When a movie is selected:

* Its TF-IDF vector is compared against all others
* Cosine similarity measures angular proximity
* Top-N highest scoring movies are returned

---

### 5️⃣ Serving & Deployment

* Models are precomputed and stored as Pickle files:

  * `tfidf_matrix.pkl`
  * `tfidf.pkl`
  * `indices.pkl`
  * `df.pkl`
* Loaded at API startup for instant inference
* Backend deployed on Render
* Frontend deployed on Streamlit Cloud

---

## 📂 Project Structure

```
neural-cinema/
│
├── main.py                 # FastAPI backend server & routing
├── app.py                  # Streamlit frontend
├── requirements.txt        # Dependencies
├── .env                    # Environment variables
│
├── tfidf_matrix.pkl        # TF-IDF matrix
├── tfidf.pkl               # TF-IDF Vectorizer
├── indices.pkl             # Index mapping
├── df.pkl                  # Cleaned dataframe
│
└── README.md
```

---

## 💻 Installation & Setup

### 1️⃣ Clone Repository

```bash
git clone https://github.com/yourusername/neural-cinema.git
cd neural-cinema
```

---

### 2️⃣ Create Virtual Environment

```bash
python -m venv venv
```

Activate:

**Mac/Linux**

```bash
source venv/bin/activate
```

**Windows**

```bash
venv\Scripts\activate
```

---

### 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

> Ensure Python version **3.11.9** for compatibility with scikit-learn model serialization.

---

### 4️⃣ Configure Environment Variables

Create `.env` file:

```
TMDB_API_KEY=your_tmdb_api_key_here
```

---

## ▶️ Running the Application

### 🚀 Start Backend

```bash
uvicorn main:app --reload
```

API available at:

```
http://localhost:8000
```

Interactive API Docs:

```
http://localhost:8000/docs
```

---

### 🖥️ Start Frontend

Open new terminal:

```bash
streamlit run app.py
```

The web application will open automatically.

---

## 🌐 API Endpoints

| Endpoint           | Method | Description                               |
| ------------------ | ------ | ----------------------------------------- |
| `/health`          | GET    | Health check                              |
| `/home-feed`       | GET    | Fetch trending, popular, top-rated movies |
| `/search`          | GET    | Search movies via keyword                 |
| `/movie-details`   | GET    | Retrieve detailed movie info              |
| `/recommendations` | GET    | Return similar movies                     |

---

## 📊 Performance Optimization Strategy

* Precomputed similarity matrix
* Pickled model loading
* Asynchronous FastAPI execution
* Clean modular separation of layers
* Reduced runtime computation overhead

# ⚡ Advanced Distributed Data Processing with PySpark

This project demonstrates scalable batch and streaming analytics using Apache Spark. It combines document indexing (TF-IDF), real-time server log analysis, and search ranking functionality — simulating real-world big data engineering tasks using PySpark, Spark SQL, and Spark Structured Streaming.

---

## 📌 Project Highlights

- ✅ Compute TF-IDF scores for large-scale text corpora stored in S3
- ✅ Rank documents based on keyword relevance
- ✅ Ingest and process real-time logs using Spark Structured Streaming
- ✅ Generate both in-memory reports and persistent outputs to S3

---

## 📁 Modules

### 🔍 1. TF-IDF Computation & Relevance Ranking
- Cleaned and tokenized documents from S3 (e.g., Shakespeare, Austen).
- Computed **TF-IDF** scores for each `(term, doc_id)` using PySpark RDDs and DataFrames.
- Implemented a **relevance scoring function** to rank documents based on user search queries.
- Results included top/bottom TF-IDF values and real-time document relevance output.

> 🔹 Output: `[(doc_id, term, tfidf_score)]`  
> 🔍 Functionality: `relevance(query, tfidf_index) → top 5 ranked docs`

---

### 📊 2. Real-Time Log Processing with Structured Streaming
- Ingested logs from simulated S3 buckets.
- Each log entry: `serverID, severity (0–2), timestamp`
- Generated two key reports:
  - **SEV2 Volume Report**: In-memory SparkSQL table with real-time update on service call volume.
  - **SEV0 Error Log**: Persistent CSV log of critical errors streamed to S3.

> 📦 Streaming Sink:  
> - SEV2 → In-memory (Spark SQL)  
> - SEV0 → CSV in S3 bucket (`Lab9Output/sev0_Report`)

---

### 🧠 3. Unified TF-IDF + Query Notebook
- Integrated the entire indexing + relevance flow into a **modular PySpark notebook**
- Clean code blocks for:
  - Indexing S3-based corpora
  - Querying with user input
  - Previewing results with `.show()` or `.collect()`

---

## 🛠 Tools & Technologies

- **Apache Spark (PySpark, SQL, Streaming)**
- **S3 Buckets** (Simulated document corpus and log streams)
- **Python 3.9**, **Spark 3.x**, **Livy Notebooks**
- **Math**: log10-based IDF, normalized term frequency

---

## 🚀 How to Run

### 📁 Document Indexing (TF-IDF)
```python
# Build TF-IDF index
myindex = indexDocuments('s3://your-bucket/textcorpora/')
myindex.persist()

# Run search
relevance("your search phrase", myindex).show()

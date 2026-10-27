
# 🚀 AI/ML Log Classification & Automated Failure Triage System

An intelligent, multi-tier hybrid log classification and auto-triage pipeline built in Python. Designed to parse, cluster, and categorize large volumes of system and wireless execution logs into actionable functional root-cause categories, significantly reducing manual debugging time.

---

## 🏗️ System Architecture & Hybrid Approach

To optimize performance, speed, and cost, the system utilizes a **3-tier cascading architecture**:

1. **Tier 1: Regular Expressions (Regex)**
   - Instantly filters and classifies high-frequency, predictable log patterns (e.g., standard user sign-ins, routine system notifications) with zero latency.
2. **Tier 2: BERT Embeddings & Supervised Machine Learning**
   - Converts raw log text into **384-dimensional dense semantic vectors** using `SentenceTransformers` (`all-MiniLM-L6-v2`).
   - Applies trained classifiers (`LogisticRegression` / `RandomForest`) with probability thresholding (`>0.50`) to categorize complex errors (`Critical Error`, `Security Alert`, `HTTP Status`, `Resource Usage`) with **94%+ precision**.
3. **Tier 3: LLM Zero/Few-Shot Fallback (Groq API / Llama 3.3)**
   - Dynamically routes rare or ambiguous edge-case failure logs (e.g., `Workflow Error`, `Deprecation Warning`) to an LLM prompt for zero-shot root-cause identification.

---

## 📂 Project Structure

```text
AI-ML-Log-Classification-Automated-Failure-Triage-System/
│
├── training/
│   └── log_classification_training.ipynb  # Jupyter Notebook for EDA, DBSCAN clustering, and ML training
│
├── models/
│   └── log_classifier.joblib              # Serialized scikit-learn model artifacts
│
├── resources/
│   ├── test.csv                           # Sample raw input log files (source, log_message)
│   └── output.csv                         # Automatically generated classified triage report
│
├── processor_regex.py                     # Rule-based Regex extraction engine
├── processor_bert.py                      # SentenceTransformer embedding & ML classification module
├── processor_llm.py                       # LLM fallback integration via Groq API
├── server.py                              # FastAPI backend exposing the /classify REST endpoint
├── requirements.txt                       # Project dependencies
└── README.md                              # Project documentation

```

---

## ⚙️ Tech Stack

* **Programming Language:** Python
* **Machine Learning & NLP:** `scikit-learn`, `SentenceTransformers`, `NLTK`, `Regex`, `DBSCAN`
* **Data Processing:** `Pandas`, `NumPy`, `Joblib`
* **Backend & API:** `FastAPI`, `Uvicorn`
* **Generative AI:** `Groq API` (`Llama-3.3-70b-versatile`)

---

## 🛠️ Installation & Setup

1. **Clone the repository:**
```bash
git clone [https://github.com/HARDIKKUMAR21/AI-ML-Log-Classification-Automated-Failure-Triage-System.git](https://github.com/HARDIKKUMAR21/AI-ML-Log-Classification-Automated-Failure-Triage-System.git)
cd AI-ML-Log-Classification-Automated-Failure-Triage-System

```


2. **Install dependencies:**
```bash
pip install -r requirements.txt

```


3. **Set up Environment Variables:**
Create a `.env` file in the root directory and add your Groq API key for LLM fallbacks:
```env
GROQ_API_KEY=your_groq_api_key_here

```



---

## 🚀 Usage

### 1. Running the FastAPI Backend Server

Start the local server using Uvicorn:

```bash
uvicorn server:app --reload

```

### 2. Testing via API Endpoint

* **Main Endpoint:** `http://127.0.0.1:8000/classify` (POST request with a CSV file containing `source` and `log_message` columns)
* **Interactive Docs:** Visit `http://127.0.0.1:8000/docs` to test file uploads directly through the Swagger UI.

---

## 📊 Performance & Results

* **Data Scale:** Benchmarked and trained across **2,410+ multi-source system logs**.
* **Automation Efficiency:** Automatically resolved **20.7%** of routine logs instantly via zero-latency Regex rules.
* **Classification Accuracy:** Achieved **94.2% precision** and a **0.93 F1-score** on complex system error logs using BERT embeddings combined with supervised classification models.

---



```

```

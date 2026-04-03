# Railway Public Address System

## Overview
    The Railway Public Address System is a Python-based project that generates text and voice announcements for train schedules, delays, and passenger feedback. It processes train data, analyzes sentiment from feedback, and produces audio announcements using text-to-speech (TTS).

    This system provides clear, automated announcements for both delayed and on-time trains, offering a seamless experience for railway operations.
---

## Features
- **Data Processing:** Combines train schedules, delay logs, and passenger feedback into a unified dataset.
- **Sentiment Analysis:** Uses NLTK's VADER sentiment analyzer to evaluate passenger feedback.
- **Announcements:** Generates text and voice announcements for trains.
- **Audio Playback:** Creates and plays `.mp3` files on macOS using Google Text-to-Speech (gTTS).

---

## Prerequisites
- **Python:** Version 3.11 recommended.
- **Operating System:** Tested on macOS (compatible with Linux/Windows with minor adjustments).
- **Dependencies:** Listed in `requirements.txt`.
---

## Installation

### 1. Clone the Repository
```bash
    git clone https://github.com/harsh-kumar274/Public-Railway-Address-System.git
```

### 2. Set Up Virtual Environment
```bash
    python3 -m venv venv
    source venv/bin/activate  # On macOS/Linux
# For Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
    pip install -r requirements.txt
```

### 4. Install SpaCy Model and NLTK Data
```bash
    python -m spacy download en_core_web_sm
    python -c "import nltk; nltk.download('vader_lexicon')"
```

### 5. Prepare Data Files
Place the following files in the `data/raw/` directory:
- `train_schedule.csv`: Contains train numbers, times, platforms, and destinations.
- `delay_logs.json`: Records train delays and reasons.
- `passenger_feedback.txt`: Includes passenger feedback.

---

## Usage

### 1. Activate the Virtual Environment
```bash
    source venv/bin/activate  # macOS/Linux
    # For Windows: venv\Scripts\activate
```

### 2. Run the System

```bash
    streamlit run main.py
 ```

### 3. Interact with the System
- Enter a train number (e.g., 108, 109) to generate an announcement.
- Type `exit` to quit.

**Example Output:**
```
    Announcement for Train 108: Train 108 to New York is delayed by 45 minutes due to weather. We apologize for the inconvenience.
```

---

## Deactivating the Virtual Environment
After running the system, deactivate the virtual environment using:
```bash
    deactivate
```
This will return you to your normal terminal session.

---

## Project Structure
```bash
    Railwaymlproject/
    ├── main.py              # Entry point for the system
    ├── src/                 # Source code
    │   ├── __init__.py
    │   ├── announcement/    # Announcement generation
    │   │   ├── __init__.py
    │   │   └── announcement.py
    │   ├── preprocessing/   # Data preprocessing
    │   │   ├── __init__.py
    │   │   └── preprocess.py
    │   └── utils/           # Utility functions
    │       ├── __init__.py
    │       └── utils.py
    ├── data/                # Data files
    │   ├── raw/             # Raw input data
    │   │   ├── train_schedule.csv
    │   │   ├── delay_logs.json
    │   │   └── passenger_feedback.txt
    │   └── processed/       # Processed output data
    │       └── processed_data.csv
    ├── venv/                # Virtual environment
    ├── requirements.txt     # Python dependencies
    └── README.md            # This file
```

---



## 📚 Libraries Used

- **pandas (1.5.0)** – For reading and merging data from CSV and JSON.
- **numpy (1.26.4)** – For numerical operations like filling missing values.
- **scikit-learn (1.2.0)** – Reserved for future ML features.
- **spacy (3.7.2)** – For NLP using the `en_core_web_sm` model.
- **nltk (3.8.1)** – For sentiment analysis using VADER.
- **gtts (2.3.0)** – Converts text into speech using Google’s TTS API.

**Note**: Other dependencies (like `certifi`, `requests`) are installed via `requirements.txt`.

---

## ⚙️ Algorithms Used

### 🔗 Merging Data
- Combines schedule and delay data using `pandas.merge()` (left join on `train_no`).
- Keeps all scheduled data and adds delay info if available.
- Time complexity: `O(n log n)`.

### 😊 Sentiment Analysis
- Uses VADER from `nltk` to analyze user feedback.
- Returns a sentiment score from -1 (negative) to +1 (positive).
  
```python
    from nltk.sentiment.vader import SentimentIntensityAnalyzer
    sid = SentimentIntensityAnalyzer()
    sentiment = sid.polarity_scores(text)["compound"]
```

### 🔊 Text-to-Speech
- Uses Google Text-to-Speech (`gtts`) to create MP3 audio announcements.

```python
    from gtts import gTTS
    tts = gTTS(text, lang="en")
    tts.save("announcement.mp3")
```

---

## 🔄 How It Works

- `main.py` – Runs the main system.
- `preprocess.py` – Loads and merges data, saves to `processed_data.csv`.
- `announcement.py` – Creates announcements based on delay info.
- `utils.py` – Helper functions like loading CSVs and analyzing sentiment.

---

## 🚨 Error Handling

- Invalid train numbers are handled with `try/except`.
- File handling errors (like missing files) should be added for more robustness.

---

## ✨ Custom Messages

- **On-time trains** – Simple, friendly message.
- **Delayed trains** – Message includes delay duration and reason with an apology.

---

## Troubleshooting

### 1. **ModuleNotFoundError**
- Ensure the virtual environment  is activated using `source venv/bin/activate`.
- Confirm dependencies are installed using `pip install -r requirements.txt`.

### 2. **FileNotFoundError**
- Verify data files are present in the `data/raw/` directory.

### 3. **OSError (Spacy)**
- Ensure the SpaCy model is installed using:
  ```bash
     python -m spacy download en_core_web_sm
  ```

### 4. **SSL Errors (NLTK)**
- Install `certifi` to resolve SSL issues:
  ```bash
    pip install certifi
    export SSL_CERT_FILE=$(python -c "import certifi; print(certifi.where())")
  ```

---


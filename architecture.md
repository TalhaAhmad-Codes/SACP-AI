
# AI Services Architecture

---

# Smart Academic Communication Platform (SACP) - AI Layer

## Overview

The AI layer of SACP is responsible for providing intelligent services that support the communication platform. Instead of directly communicating with users, this layer receives requests from the backend and returns predictions, classifications, or recommendations.

Examples:

* Email classification
* Spam detection
* Message prioritization
* Recommendation generation

This repository is completely independent and focuses only on Artificial Intelligence and Machine Learning functionalities.

---

# High-Level Architecture

```text
Backend (.NET)
      │
      │ HTTP Request
      ▼
FastAPI
      │
      ├── Email Classification
      ├── Spam Detection
      ├── Prioritization
      └── Recommendations
      │
      ▼
Machine Learning Models
      │
      ▼
Prediction Response
```

---

# Folder Structure

```text
SACP-AI/
│
├── app/
│   │
│   ├── shared/
│   │   ├── config/
│   │   ├── utils/
│   │   ├── models/
│   │   └── preprocessing/
│   │
│   ├── features/
│   │   ├── email-classification/
│   │   ├── spam-detection/
│   │   ├── prioritization/
│   │   └── recommendations/
│   │
│   ├── api/
│   │   ├── routes/
│   │   └── schemas/
│   │
│   └── main.py
│
├── notebooks/
├── datasets/
├── trained-models/
└── requirements.txt
```

---

# app/

The `app` folder contains the actual source code of the AI services.

Everything required to run the application is placed inside this folder.

---

# shared/

This folder contains common components shared among multiple features.

These components should not contain business-specific logic.

```text
shared/
├── config/
├── utils/
├── models/
└── preprocessing/
```

---

## config/

Purpose:

Centralized application configuration.

Examples:

* Environment variables
* API settings
* Model paths
* Constants

Example files:

```text
config/
├── settings.py
├── constants.py
└── environment.py
```

Examples of stored values:

```python
MODEL_DIRECTORY
DATASET_DIRECTORY
API_VERSION
DEFAULT_THRESHOLD
```

---

## utils/

Purpose:

Contains helper functions used throughout the project.

Examples:

* Logging
* Date utilities
* File handling
* Text cleaning helpers

Example:

```text
utils/
├── logger.py
├── file_utils.py
└── text_utils.py
```

These functions reduce code duplication.

---

## models/

Purpose:

Responsible for loading trained machine learning models.

This folder does not train models.

It only loads already-trained models from:

```text
trained-models/
```

Example:

```text
models/
├── email_classifier.py
├── spam_detector.py
├── prioritizer.py
└── recommender.py
```

Responsibilities:

* Load model files
* Cache models
* Provide prediction methods

---

## preprocessing/

Purpose:

Prepare raw text before sending it to machine learning models.

Examples:

* Lowercase conversion
* Removing punctuation
* Tokenization
* Stopword removal
* Lemmatization

Example:

```text
preprocessing/
├── cleaner.py
├── tokenizer.py
└── vectorizer.py
```

Flow:

```text
Raw Input
    ↓
Preprocessing
    ↓
Model
    ↓
Prediction
```

---

# features/

This folder contains all AI functionalities.

Each feature is isolated from others.

```text
features/
├── email-classification/
├── spam-detection/
├── prioritization/
└── recommendations/
```

This structure follows a feature-based approach which keeps the project organized and easier to maintain.

---

## email-classification/

Purpose:

Classify emails into categories.

Examples:

* Academic
* Administrative
* Events
* General

Example:

```text
email-classification/
├── service.py
├── predictor.py
└── labels.py
```

Used by:

* Notification System
* Analytics
* Dashboard

---

## spam-detection/

Purpose:

Detect unwanted or irrelevant messages.

Examples:

* Spam
* Promotional content
* Unnecessary announcements

Example:

```text
spam-detection/
├── service.py
├── predictor.py
└── labels.py
```

Used by:

* Message filtering
* Notification management

---

## prioritization/

Purpose:

Determine importance of messages.

Examples:

High Priority:

* Examination schedules
* Attendance warnings
* Deadline reminders

Low Priority:

* Event announcements
* General notices

Example:

```text
prioritization/
├── service.py
├── predictor.py
└── labels.py
```

Used by:

* Dashboard
* Notifications
* Message ordering

---

## recommendations/

Purpose:

Provide personalized recommendations.

Examples:

Students:

* Scholarship opportunities
* Department events

Faculty:

* Important unread messages
* Frequently used templates

Example:

```text
recommendations/
├── service.py
├── predictor.py
└── labels.py
```

This module is optional and can be extended in future versions.

---

# api/

This folder exposes AI functionalities through REST APIs.

The backend communicates with these APIs instead of directly interacting with models.

```text
api/
├── routes/
└── schemas/
```

---

## routes/

Purpose:

Contains API endpoints.

Example:

```text
routes/
├── email_routes.py
├── spam_routes.py
├── priority_routes.py
└── recommendation_routes.py
```

Example endpoints:

```text
POST /classify-email

POST /detect-spam

POST /prioritize-message

POST /recommend
```

---

## schemas/

Purpose:

Define request and response structures.

These schemas validate data before processing.

Example:

```text
schemas/
├── email_schema.py
├── spam_schema.py
└── priority_schema.py
```

Benefits:

* Data validation
* Cleaner APIs
* Better documentation

---

# main.py

Purpose:

Entry point of the FastAPI application.

Responsibilities:

* Create FastAPI instance
* Register routes
* Configure middleware
* Start the application

Example:

```python
app = FastAPI()
```

Everything begins here.

---

# notebooks/

Purpose:

Experiment and research area.

Used for:

* Dataset exploration
* Training experiments
* Feature engineering
* Performance analysis

Examples:

```text
notebooks/
├── email_classification.ipynb
├── spam_detection.ipynb
└── recommendation_engine.ipynb
```

Notebook files are mainly used during development and are not part of production code.

---

# datasets/

Purpose:

Store raw and processed datasets.

Examples:

```text
datasets/
├── raw/
├── processed/
└── external/
```

Possible datasets:

* Email datasets
* Message datasets
* Spam datasets

This folder is mainly used during training.

---

# trained-models/

Purpose:

Store trained machine learning models.

Examples:

```text
trained-models/
├── email_classifier.pkl
├── spam_detector.pkl
├── priority_model.pkl
└── recommendation_model.pkl
```

These models are loaded during runtime.

No retraining happens here.

---

# requirements.txt

Purpose:

List all Python dependencies required by the project.

Examples:

```text
fastapi
uvicorn
scikit-learn
pandas
numpy
nltk
spacy
joblib
```

Installing dependencies:

```bash
pip install -r requirements.txt
```

---

# Design Principles

The architecture follows:

* KISS (Keep It Simple)
* DRY (Don't Repeat Yourself)
* Feature-Based Organization / VSA
* Separation of Concerns
* Beginner-Friendly Structure

> The goal is to keep the AI layer simple, modular, and easy to extend without introducing unnecessary complexity.

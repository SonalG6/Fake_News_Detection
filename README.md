# Fake News Detection Using XLM-RoBERTa and Microsoft Autogen with Dynamic Weighted Agents

## Overview

This project implements a **fake news detection system** that combines a fine-tuned **XLM-RoBERTa model** with a suite of **Microsoft Autogen-based agents** to enhance its ability to identify fake news. The system incorporates **dynamic weights**, advanced **text analysis features**, and **exponential decay mechanisms** to ensure high accuracy and flexibility under various scenarios.

The modular architecture allows for easy customization of datasets, agents, and hyperparameters, making it a highly adaptable solution for different domains and user requirements.

---

## Key Features

### 1. **Integration with Microsoft Autogen**

Microsoft Autogen is a framework designed for building multi-agent systems that automate complex workflows through advanced AI and NLP models. In this system, five agents (Agent1, Agent2, Agent3, Agent4, and Agent7) utilize **Microsoft Autogen** for specialized tasks like analyzing text patterns, detecting clickbait, and handling APIs.

#### Advantages of Microsoft Autogen:
- Simplifies the development of multi-agent workflows.
- Allows seamless communication between agents.
- Provides flexibility to scale up or down based on computational resources.
- Enables efficient API handling and real-time adjustments to failures or rate limits.

#### Usage in Agents:
- **Agent1 (Special Symbols Checker):** Parses the input text and computes the proportion of special characters.
- **Agent2 (Sentiment Analyzer):** Uses pre-built Autogen sentiment analysis pipelines to extract emotion scores (positive, negative, neutral).
- **Agent3 (Hashtags Analyzer):** Extracts hashtags and computes their percentage using Autogen text-processing APIs.
- **Agent4 (Clickbait Detector):** Leverages Autogen's capabilities for semantic similarity checks between the headline and content.
- **Agent7 (Tweet Existence Checker):** Handles API integration with Twitter to verify tweet existence and engagement using Autogen's robust API-call handling mechanism.

By leveraging **Microsoft Autogen**, these agents work efficiently in tandem, enhancing overall system performance and reliability.

---

### 2. **Dynamic Weights Allocation**

The system implements **dynamic weight allocation** to adapt to different scenarios:
- Each agent’s contribution to the final score is dynamically adjusted based on its reliability and the availability of data.
- For example:
  - When Agent7 encounters API rate limits, its weight is reduced, and other agents’ weights are recalibrated accordingly.
- This ensures that the system maintains high accuracy even under suboptimal conditions.

---

### 3. **Agents and Their Responsibilities**

The system integrates six agents, each contributing specific insights about the input text:

#### **Agent1: Special Symbols Checker**
- **Objective:** Analyzes the percentage of special symbols (e.g., `!`, `@`, `#`) in the input text.
- **Why It’s Useful:** Excessive use of special symbols is often associated with spam or clickbait content.
- **Technology:** Microsoft Autogen parses the text to calculate the symbol percentage.

#### **Agent2: Sentiment Analyzer**
- **Objective:** Examines the sentiment (positive, negative, or neutral) of the input text.
- **Why It’s Useful:** Fake news articles often use emotionally charged language to manipulate readers.
- **Technology:** Microsoft Autogen’s sentiment analysis pipelines extract sentiment scores efficiently.

#### **Agent3: Hashtags Percentage Analyzer**
- **Objective:** Counts and computes the percentage of hashtags in the text.
- **Why It’s Useful:** High hashtag density is a potential indicator of low-quality or spam-like content.
- **Technology:** Microsoft Autogen processes the input to extract and analyze hashtags.

#### **Agent4: Clickbait Detector**
- **Objective:** Detects clickbait by comparing the similarity between the headline and the body of the content.
- **Why It’s Useful:** Clickbait headlines often repeat or exaggerate the first few sentences of the article.
- **Technology:** Autogen's semantic similarity tools are used for the analysis.

#### **Agent5: XLM-RoBERTa Fake News Classifier**
- **Objective:** Uses a fine-tuned **XLM-RoBERTa model** to classify the input text as real or fake.
- **Why It’s Useful:** XLM-RoBERTa excels at detecting linguistic patterns associated with fake news.
- **Technology:** Trained on the [Kaggle Fake News Dataset](https://www.kaggle.com/datasets/jainpooja/fake-news-detection).

#### **Agent7: Tweet Existence Checker**
- **Objective:** Verifies whether the input text exists as a tweet on Twitter and checks for engagement metrics (likes, retweets).
- **Why It’s Useful:** Content with significant engagement on Twitter is often more credible.
- **Technology:** Autogen handles API integration and ensures smooth execution, even under rate-limiting conditions.

---

### 4. **Exponential Decay Mechanism**

To avoid the pitfalls of linear decay (where one failing agent disproportionately impacts the final result), the system uses an **exponential decay mechanism**:
- This ensures that the influence of an agent diminishes more gradually, preventing drastic accuracy drops.
- For example, when an agent’s confidence score decreases, the exponential decay function adjusts its contribution to the final score, maintaining overall system reliability.

---

### 5. **XLM-RoBERTa Model Details**

#### Model Architecture
- **Core Classifier:** A fine-tuned **XLM-RoBERTa model** trained on a multilingual dataset of fake and real news.
- **Strength:** Handles multiple languages, making the system suitable for global applications.

#### Dataset
- The model is trained on the [Kaggle Fake News Dataset](https://www.kaggle.com/datasets/jainpooja/fake-news-detection).
- **Customizability:** The dataset can be replaced to train the model on specific domains (e.g., politics, health, entertainment).

#### Fine-Tuning
- The system allows easy fine-tuning by modifying hyperparameters such as learning rate, batch size, or epochs.
- Custom agent configurations can also be updated for domain-specific use cases.

---

## Accuracy Metrics

The system measures accuracy by aggregating agent scores dynamically:

### Formulas
1. **Fake News Accuracy (F_accuracy):**
   \[
   F\_accuracy = \frac{\sum (100 - \text{Fake Scores})}{m}
   \]

2. **True News Accuracy (T_accuracy):**
   \[
   T\_accuracy = \frac{\sum (\text{True Scores})}{p}
   \]

3. **Overall Accuracy (A_model):**
   \[
   A\_model = \frac{F\_accuracy + T\_accuracy}{2}
   \]

### Example Results
For a set of 10 test inputs (5 true and 5 fake):
- **Accuracy on Fake Inputs (F_accuracy):** 85.31%
- **Accuracy on True Inputs (T_accuracy):** 94.82%
- **Overall Accuracy (A_model):** 90.06%

---

## Modularity and Customization

The system’s modular design allows for:
- Adding or removing agents based on requirements.
- Modifying agent weights to adapt to different datasets or use cases.
- Easy fine-tuning of the **XLM-RoBERTa model** and individual agent configurations.

---

## How to Run

1. Clone the repository.
2. Install the required Python packages:
   ```bash
   pip install -r requirements.txt

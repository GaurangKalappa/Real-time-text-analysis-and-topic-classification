# Real-Time Text Classification & Analytics

This is a real-time text analytics project that combines **Apache Kafka, Machine Learning, and Python** to classify incoming social media text into predefined categories and monitor category-wise trends as messages are processed.

The system uses a Kafka producer to stream text messages, a machine learning classifier to predict their categories through a Kafka consumer, and a Tkinter-based dashboard to display continuously updated category counts.

## Key Features

- **Real-Time Data Streaming:** Uses Apache Kafka to publish and consume text messages through a dedicated topic.
- **Text Classification:** Classifies incoming messages into five categories: Politics, Technology, Sports, Entertainment, and Business.
- **Machine Learning:** Uses a pre-trained Logistic Regression model and a fitted text vectorizer for message classification.
- **Trend Monitoring:** Maintains category-wise message counts and exports updated statistics to CSV.
- **Live Dashboard:** Provides a Tkinter GUI with separate tabs for each category to monitor classification counts.

## Tech Stack

The project is developed using Python and incorporates Apache Kafka for distributed streaming, Scikit-learn with Logistic Regression for machine learning, Apache Spark (PySpark) for big data processing, TF-IDF, tokenization, and stop-word removal for text processing, Pandas for data handling, Pickle for model persistence, and Tkinter for the graphical user interface (GUI).

## Machine Learning Pipeline

The project includes a PySpark-based text classification workflow:

1. **Data Preprocessing:** Converts text to lowercase, removes punctuation and special characters, tokenizes text, and filters invalid or short records.
2. **Feature Engineering:** Uses tokenization, stop-word removal, HashingTF, and IDF to transform text into numerical feature vectors.
3. **Model Training:** Implements a Random Forest classifier using a PySpark ML pipeline.
4. **Hyperparameter Tuning:** Uses cross-validation and a parameter grid to explore different tree counts and maximum depths.
5. **Evaluation:** Evaluates classification performance using accuracy.

## Kafka Streaming Workflow

**Producer:** Reads text records from a CSV dataset and publishes messages to the Kafka topic `test`.

**Consumer:** Subscribes to the topic, receives incoming messages, transforms them using the saved vectorizer, and predicts their categories using the trained Logistic Regression model.

**Analytics:** Updates category-wise counts and writes the results to a CSV file for dashboard consumption.

## Dashboard

The Tkinter dashboard provides separate tabs for each topic category namely technology, politics, sports, entertainment and business.

It periodically reads category statistics from a CSV file and refreshes the displayed counts.

## Setup and Execution

### Prerequisites

- Python 3.x
- Apache Kafka and a running Kafka broker
- Java (required by Apache Spark)
- Python packages listed below

### Install Dependencies

```bash
pip install pandas scikit-learn pyspark kafka-python
```

Tkinter is generally included with standard Python installations.

### 1. Start Kafka

Start your Kafka server locally and ensure that the broker is accessible at:

```text
localhost:9092
```

### 2. Train the Machine Learning Model

Run `model.ipynb` in Jupyter Notebook after configuring the training dataset path and completing the train/test data preparation.

The streaming consumer requires a trained classifier and its corresponding fitted vectorizer saved as:

```text
logistic_regression_model.pkl
vectorizer.pkl
```

### 3. Start the Kafka Consumer

Run `consumer.ipynb` to subscribe to the `test` topic and classify incoming messages.

### 4. Start the Kafka Producer

Configure the CSV input path in `producer.ipynb` and run it to publish text records to Kafka.

### 5. Launch the Dashboard

Run `gui.ipynb` to view category-wise message counts.

## Dataset

The project uses CSV-based text data containing a `text` column for incoming messages and a `category` column for supervised model training.

The datasets are also included in this repository. Kindly refer to them or use your own dataset.

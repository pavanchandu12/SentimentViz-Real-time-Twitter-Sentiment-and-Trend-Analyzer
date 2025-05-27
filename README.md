Kafka + Spark Streaming Tweet Analytics

This project simulates a real-time tweet and hashtag analytics pipeline using MySQL, Kafka, and Apache Spark Streaming.

We continuously extract tweets and hashtags from a MySQL database, publish them into Kafka topics, and then consume and process the data using Spark to perform real-time and batch analytics.

Features

1)_Kafka producer that:

Pulls random tweets and hashtags from MySQL

Publishes data to Kafka topics (tweets, hashtags, top_tweets, top_hashtags)

2) Spark streaming consumer that:

Subscribes to a chosen Kafka topic

Processes streaming data with time windows

Outputs results to the console and a CSV file

3)Batch consumer that:

Counts tweets by language over a 5-minute window

4)Streaming consumer that:

Aggregates tweet counts by hashtags in 15-minute windows

Outputs sorted counts and saves them to CSV

📦 Project Structure

/kafka-producer.py         # Publishes data from MySQL to Kafka topics

/spark-batch-consumer.py   # Spark job for batch-like tweet language counts

/spark-streaming-consumer.py  # Spark job for hashtag-based streaming analytics

🛠️ Setup Instructions

1️⃣ Prerequisites

✅ Install:

Python 3.x

MySQL server

Apache Kafka

Apache Spark

Required Python packages:


pip install kafka-python mysql-connector-python pyspark pandas

✅ Start Kafka and Zookeeper:



# Zookeeper

bin/zookeeper-server-start.sh config/zookeeper.properties

# Kafka broker

bin/kafka-server-start.sh config/server.properties

✅ Make sure you have Kafka topics created:


bin/kafka-topics.sh --create --topic tweets --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

bin/kafka-topics.sh --create --topic hashtags --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

bin/kafka-topics.sh --create --topic top_tweets --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

bin/kafka-topics.sh --create --topic top_hashtags --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

✅ Prepare your MySQL database:

Create a tweet_hashtags_db database.

Add tweets, hashtags, and tweet_hashtags tables.

Insert sample data for testing.

🚀 How to Run

🔹 Kafka Producer

Start the Kafka producer to stream data from MySQL:

python kafka-producer.py

🔹 Spark Batch Consumer

Start the Spark batch consumer:


python spark-batch-consumer.py

This will:

Subscribe to the tweets topic.

Count tweets per language over 5-minute windows.

Print results to the console.

🔹 Spark Streaming Consumer

Start the Spark streaming consumer:

python spark-streaming-consumer.py

This will:

Subscribe to the chosen topic (top_tweets, top_hashtags, tweets, or hashtags).

Aggregate hashtag counts over 15-minute windows.

Print results to the console and save to output.csv.

📈 Sample Output

Console output example:

+------------------------------------------+----------+-----------+

|window                                    |hashtags  |tweet_count|

+------------------------------------------+----------+-----------+

|{2025-05-27 10:00:00, 2025-05-27 10:15:00}|#AI       |25         |

|{2025-05-27 10:00:00, 2025-05-27 10:15:00}|#BigData  |30         |

+------------------------------------------+----------+-----------+


CSV output (output.csv):

window,hashtags,tweet_count

2025-05-27 10:00:00,#AI,25

2025-05-27 10:00:00,#BigData,30

Configuration Notes

Update your MySQL connection details (host, user, password, database) in the producer script.

Kafka broker defaults to localhost:9092 — change if using a remote setup.

Adjust Spark window durations or topics as needed.

💡 Future Improvements
✅ Add more detailed analytics (e.g., sentiment analysis)

✅ Integrate dashboard (e.g., using Grafana or Streamlit)

✅ Add unit tests and error handling

✅ Use Docker Compose to orchestrate Kafka + Spark + MySQL setup


Feel free to ⭐️ this repo or submit pull requests!


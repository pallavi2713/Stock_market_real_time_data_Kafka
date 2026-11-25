# Architecture
![Stock-mtk-project-architecture](https://github.com/user-attachments/assets/5c8b6c70-74bb-446e-adc4-ca424b799c71)

# Real-Time Stock Market Data Pipeline | Apache Kafka & AWS

A Python-based data engineering project that demonstrates event-driven data ingestion and processing using Apache Kafka and AWS. The pipeline publishes stock market records through Kafka, consumes streaming messages using a Python consumer, and persists the processed records in Amazon S3 for downstream data processing and analytics.

## Architecture

```text
             Stock Market Dataset
                      |
                      v
              Python Producer
             (kafka-python)
                      |
                      v
                Apache Kafka
                 EC2 Broker
                      |
                 Kafka Topic
                demo_testing2
                      |
                      v
              Python Consumer
             (kafka-python)
                      |
                      v
                 Amazon S3
              JSON Data Storage
                      |
                      v
              AWS Glue Crawler
                      |
                      v
              Glue Data Catalog
                      |
                      v
                Amazon Athena
              SQL-based Analytics
```

*Note: The Kafka producer-consumer and S3 integration are implemented in the project. AWS Glue and Athena represent the documented downstream analytics architecture.*

## Key Features

- **Event Streaming:** Implemented a Kafka producer to publish stock market records to a Kafka topic using Python.
- **Message Serialization:** Used JSON serialization and deserialization to exchange structured records between producers and consumers.
- **Stream Consumption:** Developed a Python Kafka consumer to continuously retrieve messages from the configured topic.
- **Cloud Storage Integration:** Integrated Amazon S3 to persist consumed records as JSON data.
- **Distributed Infrastructure:** Configured Apache Kafka on an AWS EC2 instance and worked with broker and ZooKeeper startup operations.
- **Analytics Architecture:** Incorporated AWS Glue Crawler, Glue Data Catalog, and Amazon Athena in the downstream data analytics design.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming | Python |
| Stream Processing | Apache Kafka |
| Kafka Client | kafka-python |
| Message Format | JSON |
| Cloud Infrastructure | AWS EC2 |
| Cloud Storage | Amazon S3 |
| Data Catalog | AWS Glue |
| Query Engine | Amazon Athena |
| Data Processing | Pandas, SQL |

## Project Structure

```text
Stock_market_real_time_data_Kafka/
│
├── KafkaProducer.ipynb
│   └── Python Kafka producer implementation
│
├── kafkaconsumer.ipynb
│   └── Python Kafka consumer and S3 integration
│
├── Kafka_Commands.txt
│   └── Kafka installation and broker commands
│
├── indexProcessed.csv
│   └── Stock market dataset
│
└── README.md
```

## Implementation Workflow

### 1. Kafka Infrastructure Setup

- Provisioned an AWS EC2 instance.
- Installed Java and Apache Kafka.
- Configured Kafka broker and ZooKeeper services.
- Created a Kafka topic named `demo_testing2`.

### 2. Producer Implementation

- Loaded stock market records using Python and Pandas.
- Configured a Kafka producer using `kafka-python`.
- Serialized records into JSON messages.
- Published messages to the configured Kafka topic.

### 3. Consumer Implementation

- Configured a Python Kafka consumer.
- Subscribed to the `demo_testing2` topic.
- Deserialized incoming JSON messages.
- Processed consumed records for cloud storage.

### 4. AWS S3 Integration

- Integrated the consumer with Amazon S3.
- Persisted consumed records as JSON files.
- Established S3 as the storage layer for downstream data processing.

### 5. Downstream Analytics Architecture

The project documents an AWS analytics layer using:

- **AWS Glue Crawler:** Discovering data schemas.
- **AWS Glue Data Catalog:** Maintaining metadata for analytical datasets.
- **Amazon Athena:** Enabling SQL-based queries over data stored in S3.

## Getting Started

### Prerequisites

- Python 3.x
- Java runtime
- Apache Kafka
- AWS account
- AWS EC2 instance
- Amazon S3 bucket
- AWS credentials configured securely

### Install Python Dependencies

```bash
pip install kafka-python pandas s3fs
```

### Start Kafka Services

After installing and extracting Apache Kafka, start the required services using the configuration appropriate to your Kafka installation.

```bash
# Start ZooKeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Start Kafka broker
bin/kafka-server-start.sh config/server.properties
```

### Create a Kafka Topic

```bash
bin/kafka-topics.sh \
  --create \
  --topic demo_testing2 \
  --bootstrap-server localhost:9092 \
  --partitions 1 \
  --replication-factor 1
```

### Execute the Pipeline

1. Configure the Kafka bootstrap server in the producer and consumer notebooks.
2. Configure AWS credentials and the destination S3 bucket.
3. Start the Kafka broker and create the topic.
4. Execute `KafkaProducer.ipynb` to publish stock market records.
5. Execute `kafkaconsumer.ipynb` to consume messages and persist records to S3.

Refer to `Kafka_Commands.txt` for the original infrastructure setup commands.

## Engineering Concepts Demonstrated

- Event-driven architecture
- Producer-consumer communication
- Distributed messaging systems
- Topic-based message streaming
- JSON serialization and deserialization
- Cloud-based data ingestion
- AWS storage integration
- Data pipeline architecture

## Future Improvements

- Replace the historical dataset with a live stock market data API.
- Introduce multiple Kafka partitions and consumer groups for parallel processing.
- Implement retry mechanisms and dead-letter queues for failed messages.
- Add structured logging and monitoring for pipeline observability.
- Improve fault tolerance and message-processing reliability.
- Automate deployment and infrastructure configuration.

## Repository

[GitHub – Stock Market Real-Time Data Pipeline](https://github.com/pallavi2713/Stock_market_real_time_data_Kafka)

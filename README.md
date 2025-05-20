# ML Streaming Project

This project implements a distributed machine learning system with two main components:
1. A data sender server that streams data over TCP
2. A receiver server that processes the data stream using Apache Spark and trains ML models

## Features

- Streaming data processing with Apache Spark
- Support for Iris and California Housing datasets
- Classification models: SVM and Logistic Regression
- Real-time model training and evaluation metrics
- Configurable batch size and streaming intervals

## Project Structure

```
ml_streaming_project/
├── data/                  # Dataset files
│   ├── iris.csv           # Iris dataset
│   └── california_housing.csv # California Housing dataset
├── sender/                # Data sender server
│   ├── __init__.py
│   ├── dataset.py         # Dataset handling
│   └── stream.py          # TCP streaming implementation
├── receiver/              # Data receiver server
│   ├── __init__.py
│   ├── config.py          # Spark configuration
│   ├── dataloader.py      # Data loading from stream
│   ├── trainer.py         # Model training logic
│   └── models/            # ML models
│       ├── __init__.py
│       ├── svm.py         # SVM implementation
│       └── logistic.py    # Logistic Regression implementation
└── main.py                # Main application entry point
```

## Requirements

- Python 3.6+
- Apache Spark
- scikit-learn
- pandas
- numpy
- tqdm

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/ml-streaming-project.git
cd ml-streaming-project
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Start the Receiver (Spark Streaming Server)

```bash
python main.py --model svm --host localhost --port 6100 --batch-interval 2
```

Options:
- `--model` or `-m`: Model type (svm or logistic), default: svm
- `--host`: Streaming host, default: localhost
- `--port` or `-p`: Streaming port, default: 6100
- `--batch-interval` or `-b`: Batch interval in seconds, default: 2
- `--app-name` or `-a`: Spark application name, default: ML_Streaming

### Start the Sender (Data Streaming Server)

```bash
cd sender
python stream.py --dataset iris --batch-size 10 --sleep 1
```

Options:
- `--dataset` or `-d`: Dataset type (iris or california), default: iris
- `--batch-size` or `-b`: Batch size, default: 10
- `--endless` or `-e`: Enable endless stream, default: False
- `--sleep` or `-s`: Streaming interval in seconds, default: 1
- `--host`: TCP host, default: localhost
- `--port` or `-p`: TCP port, default: 6100

## How It Works

1. The sender reads data from the specified dataset (Iris or California Housing)
2. Data is batched and streamed over TCP socket
3. The receiver uses Spark Streaming to process incoming data
4. The specified ML model (SVM or Logistic Regression) is trained on each batch
5. Training metrics are calculated and displayed in real-time

## License

This project is licensed under the MIT License - see the LICENSE file for details.

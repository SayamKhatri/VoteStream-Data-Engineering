# VoteStream-kafka-Data-Engineering

The VoteStream Data Engineering Pipeline is a real-time election voting system designed to capture, process, and visualize voting data instantaneously. By integrating technologies such as Apache Kafka, Apache Spark Streaming, PostgreSQL, and Streamlit, the system ensures efficient data flow from vote casting to real-time analytics, providing stakeholders with up-to-date election insights.

## System Architecture

![image](https://github.com/user-attachments/assets/4233696f-02f6-4f8d-a6ec-07fda6475060)

## Technologies Used

- **Apache Kafka**: Manages real-time data ingestion by handling vote event streams.
- **Apache Spark Streaming**: Processes streaming data for real-time analytics and transformations.
- **PostgreSQL**: Serves as the relational database for storing structured voting data.
- **Streamlit**: Provides a user-friendly interface for real-time data visualization and interaction.
- **Docker**: Containerizes services to ensure consistent deployment and scalability.

## Project Structure

The repository is organized as follows:

- **`.gitignore`**: Specifies files and directories to be ignored by Git to maintain a clean version control history.
- **`LICENSE`**: Contains the MIT license under which the project is distributed.
- **`README.md`**: Provides an overview and documentation of the project.
- **`app.py`**: Implements the Streamlit application for real-time data visualization.
- **`docker-compose.yml`**: Defines and orchestrates the Docker services for Kafka, Zookeeper, PostgreSQL, and other components.
- **`main.py`**: Initializes the PostgreSQL database, creates necessary tables (`candidates`, `voters`, `votes`), and sets up Kafka topics.
- **`postgresql-42.7.5.jar`**: JDBC driver for PostgreSQL to facilitate database connectivity.
- **`requirements.txt`**: Lists the Python dependencies required for the project.
- **`spark-streaming.py`**: Contains the Spark Streaming logic to consume, process, and enrich vote data from Kafka topics.
- **`voting.py`**: Simulates the voting process by generating and producing vote data to Kafka topics.

## Setup Instructions

To deploy and run the VoteStream Data Engineering Pipeline, follow these steps:

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/SayamKhatri/VoteStream-Data-Engineering.git
   cd VoteStream-Data-Engineering
   ```

2. **Install Dependencies**:

   Ensure that Python 3.9 or above and Docker are installed on your system. Install the required Python packages:

   ```bash
   pip install -r requirements.txt
   ```

3. **Start Docker Services**:

   Use Docker Compose to start the necessary services:

   ```bash
   docker-compose up -d
   ```

   This command will start Zookeeper, Kafka, and PostgreSQL containers in detached mode.

4. **Initialize the Database and Kafka Topics**:

   Run the `main.py` script to set up the PostgreSQL tables and Kafka topics:

   ```bash
   python main.py
   ```

5. **Simulate Voting Data**:

   Execute the `voting.py` script to generate and produce vote data to the Kafka topics:

   ```bash
   python voting.py
   ```

6. **Process Streaming Data with Spark**:

   Run the `spark-streaming.py` script to consume, process, and enrich vote data from Kafka topics:

   ```bash
   python spark-streaming.py
   ```

7. **Launch the Streamlit Dashboard**:

   Start the Streamlit application to visualize real-time voting data:

   ```bash
   streamlit run app.py
   ```

   Access the dashboard at `http://localhost:8501` in your web browser.

## Data Flow

1. **Data Ingestion**: Votes are generated and sent to specific Kafka topics.
2. **Data Processing**: Spark Streaming consumes vote data from Kafka, enriches it using PostgreSQL data, and produces processed data back to Kafka topics.
3. **Data Storage**: Processed vote data is stored in PostgreSQL tables for persistence and further analysis.
4. **Data Visualization**: The Streamlit application consumes data from PostgreSQL and Kafka to display real-time voting results and analytics.

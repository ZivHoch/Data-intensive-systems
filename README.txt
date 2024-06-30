# Data Intensive Systems Assingment, PSZ: Team 2

## Project Structure

This repository consists of four main folders:

1. **Data**
2. **Presentation**
3. **Report**
4. **Src**

### Data Folder
In the Data folder, you can find our generated datasets and their outputs. Here are the key files:
- `input.txt`: Input for our stress test containing 30,000 processes (test 3 in our report).
- `part1Output.txt`
- `part1Observations.txt`
- `part2Observations.txt`

Additionally, there are folders for other tests, each named according to the test in the report. More details about the results and experiments for each test can be found in the report in the Report folder.

### Presentation Folder
Contains the presentation materials for the project.

### Report Folder
Includes the detailed report of the project, documenting our methods, results, and analysis.

### Src Folder
The source code for the project is located in the Src folder, which contains the following files:
- `log_generator.ipynb`: Script for generating new synthetic datasets.
- `Part1.ipynb`: Implementation of Part 1 of our solution.
- `Part2.ipynb`: Implementation of Part 2 of our solution.

## Project Flow

### Setting up Spark Cluster

Before running the project, you need to set up a Spark cluster. Follow these steps:

#### Start Master Node
1. Open Command Prompt as administrator.
2. Navigate to Spark installation directory: cd %SPARK_HOME%
3. Start the Spark Master: bin\spark-class2.cmd org.apache.spark.deploy.master.Master

#### Start Worker Node(s)
For each worker node:
1. Open Command Prompt as administrator.
2. Navigate to Spark installation directory:
cd %SPARK_HOME%
3. Start the Spark Worker specifying number of cores (`-c`) and amount of RAM (`-m`). Example:
bin\spark-class2.cmd org.apache.spark.deploy.worker.Worker -c 2 -m 8G spark://192.168.1.81:7077

- `-c`: Number of cores for the worker.
- `-m`: Amount of RAM allocated to the worker.
- `spark://192.168.1.81:7077`: Spark Master URL. Obtain this link from the Spark Master web UI.

Ensure each worker node runs on a separate Command Prompt terminal.

### Generating Synthetic Datasets

If you already have the dataset in the format `<FromServer, ToServer, time, action, processId>`, you can skip this step.

1. Open Anaconda Prompt as administrator.
2. Navigate to the directory containing `log_generator.ipynb`:cd path_to_src_folder
3. Open Jupyter Notebook and run `log_generator.ipynb`.
4. Follow these steps within `log_generator.ipynb`:

#### Generate Tree Structure of Network
- Call the function `create_tree` with the desired number of servers and network depth.
  ```python
  node_list, layers = create_tree(num_servers, network_depth)
  ```

#### Generate Log
- Call the function `generate_log` with the generated `node_list`, desired number of processes, and threshold for requests.
  ```python
  logs = generate_log(node_list, num_processes, threshold)
  ```

#### Export Logs to TXT
- Use the function `export_logs_to_txt` to export the generated logs to a TXT file.
  ```python
  export_logs_to_txt(logs, 'output_file.txt')
  ```

### Part 1: Using k-Shingles and MinHashLSH

After generating the desired dataset, proceed with Part 1:

1. Open `Part1.ipynb`.
2. Convert the TXT file into CSV format if necessary.
3. Implement the following steps:
- Initialize the spark session according to you hardware resources.
- Load the CSV file into a dataframe with your spark session.
- Use k-Shingles on the concatenated string of `FromServer` and `ToServer` while keeping only the request logs.
- Generate a sparse vector representing the shingles with the CountVectorizer.
- Apply `MinHashLSH` to find similar candidate pairs and verify using Jaccard Similarity.
- Export groups and combined data according to project requirements.
- Set thresholds: 0.5 for candidates and 0.9 for verifying real pairs.

### Part 2: Using the names of the servers instead of Shingles and MinHashLSH

After completing Part 1 and obtaining `part1Output.txt` and `part1Observations.txt`, proceed with Part 2:

- Open `Part2.ipynb`, and open Spark session.
- Use as an input file the `part1Output.txt` that you got from Part 1 and convert it into CSV.
- Load the CSV file into a dataframe with your spark session.
- Use `CountVectorizer` on server names.
- Create a sparse vector and apply `MinHashLSH` to find similar candidate pairs.
- Verify pairs using Jaccard Similarity.
- Export results in the desired format.
- Set thresholds: 0.5 for candidates and 0.7 for verifying pairs.

### Location of Each File

- **Data Folder**: Contains datasets and outputs.
- **Presentation Folder**: Contains presentation materials.
- **Report Folder**: Contains the project report.
- **Src Folder**: Contains the source code (`log_generator.ipynb`, `Part1.ipynb`, `Part2.ipynb`).

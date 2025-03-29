# RL Trading Project

A project for algorithmic trading using Reinforcement Learning. The project is configured to run in a Docker container, providing an isolated execution environment with all necessary dependencies.

## Project Structure

- `RL_Trading.ipynb` - Jupyter notebook with the main code
- `fourX_.keras` - pre-trained Keras model
- `Dockerfile` - Docker image configuration
- `docker-compose.yaml` - Docker Compose configuration
- `requirements.txt` - Python dependencies

## Installation and Launch

### Prerequisites

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Steps to Launch

1. **Clone the repository**
   ```bash
   git clone <your-repository-URL>
   cd <repository-directory>
   ```

2. **Build the Docker image**
   ```bash
   docker-compose build
   ```

3. **Start the container**
   ```bash
   docker-compose up -d
   ```

4. **Get the URL for accessing Jupyter Notebook**
   ```bash
   docker-compose logs | grep token
   ```
   Copy the URL, which will look something like: `http://127.0.0.1:8888/?token=xxxxxxxxxxxxxxxx`

5. **Open the URL in your browser**
   This will open the Jupyter Notebook interface with your project files.

6. **Open RL_Trading.ipynb**
   Click on the `RL_Trading.ipynb` file to start working with the project.

7. **When finished, stop the container**
   ```bash
   docker-compose down
   ```

## Usage

### Loading Data

The notebook is already set up to load historical AMZN data using the `yfinance` library. You can change the time period or stock symbol if needed.

### Training the Model

The notebook contains a complete pipeline for training a reinforcement learning trading algorithm:
- Data preprocessing
- Creating a trading environment
- Setting up and training the RL agent
- Testing the strategy
- Visualizing results

### Using the Pre-trained Model

The project includes a `fourX_.keras` file with a pre-trained model that can be used for trading or further training on new data.

## Troubleshooting

### Dependency Issues

If you encounter errors due to missing libraries, edit the `requirements.txt` file and rebuild the image:
```bash
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

### GPU Issues

To use GPU, you need to:
1. Install [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
2. Uncomment the relevant lines in `docker-compose.yaml`:
```yaml
deploy:
  resources:
    reservations:
      devices:
        - driver: nvidia
          count: 1
          capabilities: [gpu]
```

## Additional Information

### How to Save Models and Results

All files created inside the `/app` directory in the container will be saved to your project directory on your computer thanks to the volumes configuration in docker-compose.yaml.

### How to Update Model Parameters

To experiment with different algorithm parameters, modify the corresponding cells in the notebook, for example:
- Changing the time horizon
- Adjusting RL algorithm hyperparameters
- Modifying the agent's reward strategy

## License

[Specify your license]

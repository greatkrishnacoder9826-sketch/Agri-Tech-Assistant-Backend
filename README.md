Agri-Tech Assistant BackendThis repository contains a collection of Python scripts and Jupyter Notebooks designed to power an agricultural assistant application. The project integrates machine learning models and external APIs to provide farmers with crop disease diagnostics, real-time weather updates, market prices, and voice transcription capabilities.🚀 Features🌱 Crop Disease Prediction: Uses a pre-trained TensorFlow model to identify plant diseases (such as Early Blight in Potatoes and Tomatoes, or Common Rust in Corn) from uploaded images.  ⛅ Real-Time Weather Updates: Fetches current weather conditions (temperature, humidity, etc.) for any given city using the OpenWeather API.  📈 Market Price Fetching: Connects to the Indian government's open data platform (data.gov.in) to retrieve agricultural market prices.  🎙️ Audio Transcription: Utilizes OpenAI's Whisper model (small) to transcribe audio files, specifically configured to transcribe Hindi audio into text.  🛠️ PrerequisitesTo run these scripts, you will need Python 3.11 or higher. You will also need to install the following core libraries:  Machine Learning & Image Processing: tensorflow, numpy  Audio Processing: whisper (OpenAI)  API Interactions: requests, python-dotenv  ⚙️ Setup and Installation1. Clone the repositoryBashgit clone https://github.com/yourusername/agri-tech-backend.git
cd agri-tech-backend
2. Create and activate a virtual environmentBashpython -m venv myenv
source myenv/bin/activate  # On Windows use: myenv\Scripts\activate
3. Set up Environment VariablesCreate a .env file in the root directory and add your API keys:Code snippetOPENWEATHER_API_KEY=your_openweather_api_key_here
DATA_GOV_API_KEY=your_data_gov_api_key_here
4. Add the Model
Ensure that your trained MobileNetV2 model named crop_disease_model.keras is placed in the root directory of the project.  💻 Usage Examples1. Crop Disease DetectionThe prediction script uses a MobileNetV2 architecture to classify crop leaves.  Pythonimport tensorflow as tf
from predict import predict_disease

# Supported classes: Corn (Common rust, healthy), Potato (Early blight, healthy), Tomato (Early blight, healthy)
result = predict_disease("path/to/leaf_image.jpg")
print(result) 
# Example Output: {'disease': 'Potato___Early_blight', 'confidence': 99.91}
2. Weather InformationPass a location string to get current temperature and humidity data.  Pythonfrom weather import get_temperature

weather_data = get_temperature("Sector 63, Noida")
print(weather_data)
# Example Output: {'location': 'Sector 63', 'temperature': 27.81, 'humidity': 76}
3. Audio Transcription (Whisper)The transcription module uses the Whisper small model to process audio files. Note: CPU execution will automatically default to FP32.  Pythonfrom transcribe import transcribe_audio

# Transcribe a Hindi audio file
text = transcribe_audio("path/to/audio.mp3")
print(text)
⚠️ Known IssuesMarket Price API: The data.gov.in API integration may occasionally return a 502 Bad Gateway error due to server-side instability on the government's portal. Ensure you implement retry logic or exception handling in production.  

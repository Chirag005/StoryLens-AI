*******************************************************************************
*******************************************************************************

Project Report: StoryLens-AI

*******************************************************************************
*******************************************************************************

📌 1. Project Overview

*******************************************************************************

The StoryLens-AI is an AI-powered application that transforms an uploaded image into a short, creative story and then converts that story into spoken audio.

The system combines computer vision, natural language processing (NLP), and text-to-speech (TTS) technologies to create a smooth pipeline:

Upload Image → Generate Text Description → Create Story → Convert to Speech → Play Audio Output

This project demonstrates how multiple state-of-the-art AI models can work together to create an interactive, multimodal AI experience.


*******************************************************************************

🧠 2. Key Features

*******************************************************************************

📷 Image Captioning using BLIP model (Vision + Language model)

✍️ Story Generation using a GPT-based LLM

🗣️ Speech Synthesis using a HuggingFace TTS model

🖥️ Interactive Web UI built with Streamlit

🔐 Secure integration of API keys using environment variables


*******************************************************************************

3. System Architecture
🧩 Step-by-Step Flow

*******************************************************************************

Image Upload (User Interaction)

The user uploads an image through the Streamlit web interface.

The app processes the file and displays the uploaded image.

Image-to-Text Generation (Visual Understanding)

The BLIP (Bootstrapped Language-Image Pretraining) model from Hugging Face analyzes the image.

It generates a caption or descriptive sentence summarizing the image content.

Text-to-Story Generation (Language Generation)

The caption is sent to OpenAI’s GPT model (via LangChain’s ChatOpenAI interface).

GPT uses a storytelling prompt to expand the image description into a creative short story (≤50 words).

Text-to-Speech Generation (Audio Conversion)

The story text is then passed to the ESPnet (kan-bayashi_ljspeech_vits) TTS model hosted on Hugging Face.

The model synthesizes human-like speech from the story text.

The resulting audio is saved as a .flac file and played back through the Streamlit interface.

Display & Interaction

The generated scenario, story, and speech are displayed to the user.

Users can listen to the generated audio directly on the interface.

*******************************************************************************

🧰 3. Technologies Used

*******************************************************************************

| Technology                         | Purpose                   | Details                                                                          |
| ---------------------------------- | ------------------------- | -------------------------------------------------------------------------------- |
| 🐍 **Python**                      | Core Programming Language | Handles the backend logic and model integration                                  |
| 🧭 **Streamlit**                   | Frontend / UI             | Used to build an interactive web application with file upload and audio playback |
| 🔐 **python-dotenv**               | Environment Management    | Loads API keys securely from `.env` file                                         |
| 🧠 **transformers**                | Vision Model              | Provides the BLIP model for image captioning                                     |
| 🤖 **LangChain**                   | LLM Orchestration         | Enables easy integration with GPT-based models                                   |
| 🌐 **OpenAI API**                  | LLM Backend               | Generates creative short stories from image captions                             |
| 🗣️ **Hugging Face Inference API** | TTS Model                 | Converts generated stories to speech                                             |
| 🧾 **Salesforce BLIP**             | Vision Model              | Used for image-to-text captioning                                                |
| 🔊 **ESPnet TTS**                  | Speech Synthesis          | Model used for audio output                                                      |

*******************************************************************************

🧪 4. How the Technologies Work Together

*******************************************************************************

Step 1: Image Upload (Frontend)

User uploads a .jpg image via the Streamlit interface.

The image is saved locally for processing.

Step 2: Image Captioning (BLIP Model)

The app uses the pipeline("image-to-text") from the transformers library.

Model: Salesforce/blip-image-captioning-base

Output: A textual description of what’s in the image (e.g., “A dog sitting on the grass with a ball”).

Step 3: Story Generation (OpenAI + LangChain)

The image caption is passed as context into a custom GPT prompt.

LangChain’s LLMChain structure is used to organize prompt engineering.

Backend Model: gpt-3.5-turbo from OpenAI.

Output: A short story (max 50 words) creatively generated based on the image description.

Step 4: Text-to-Speech Conversion (HuggingFace TTS)

The story text is sent to the Hugging Face inference API.

Model: ESPnet/kan-bayashi_ljspeech_vits

Output: Audio file (.flac format) generated and saved locally.

Step 5: Playback (Frontend)

The audio file is played directly in the browser using Streamlit’s st.audio() component.

User can also read the generated text and story under expandable sections.

*******************************************************************************

🧰 5. Project Structure

*******************************************************************************

Image-to-Speech-GenAI-Tool-Using-LLM/
│
├── app.py                        # Main application logic
├── token.env                     # Environment variables (API keys)
├── utils/
│   └── custom.py                 # Custom CSS / UI styling
├── img/
│   └── gkj.jpg                   # Sample image for sidebar
├── generated_audio.flac          # Generated audio file
├── requirements.txt              # Python dependencies
└── README.md                     # Project documentation


*******************************************************************************

🔐 6. Security & Environment Management

*******************************************************************************

API keys are stored in token.env:

OPENAI_API_KEY=your_openai_key
HUGGINGFACE_API_TOKEN=your_hf_token


Loaded via:

from dotenv import load_dotenv
load_dotenv("token.env")


.env or token.env should be excluded from version control using .gitignore.


*******************************************************************************

🏆 7. Advantages of This Approach

*******************************************************************************


| Feature               | Advantage                                    |
| --------------------- | -------------------------------------------- |
| Modular AI pipeline   | Easy to replace/upgrade models independently |
| Real-time processing  | Story & audio generated within seconds       |
| Open-source ecosystem | Uses widely adopted tools & models           |
| Minimal backend       | Streamlit makes deployment lightweight       |
| Creative storytelling | Demonstrates LLM + vision synergy            |
| Voice output          | Adds accessibility and interactivity         |

*******************************************************************************

🧠 8. Possible Use Cases

*******************************************************************************

🧒 Education: Turning images into short stories to teach children vocabulary and comprehension.

📸 Content Creation: Auto-generating stories and captions for social media posts.

🎧 Accessibility: Helping visually impaired users “hear” descriptions of images.

📚 Language Learning: Listening to stories to improve comprehension and pronunciation.

🧪 AI Demos / Research: Showcasing multimodal AI capabilities in classrooms or workshops.

*******************************************************************************

🚀 9. Future Improvements

*******************************************************************************

✨ Add support for multiple languages (e.g., translation before TTS).

🧭 Provide story length options (short, medium, long).

🎤 Offer voice style selection (different speakers or tones).

🖼️ Allow drag-and-drop or webcam capture input.

☁️ Deploy on a cloud platform like Streamlit Community Cloud or Hugging Face Spaces.

📁 Save generated stories + audio for sharing.

*******************************************************************************

📦 10. Installation & Running

*******************************************************************************

Prerequisites:

Python 3.10+

API keys for OpenAI and Hugging Face

Install dependencies:
pip install -r requirements.txt

Add your keys in token.env:
OPENAI_API_KEY=your_openai_key
HUGGINGFACE_API_TOKEN=your_hf_token

Run the app:
streamlit run app.py

Access in browser:
http://localhost:8501

*******************************************************************************

📜 11. Dependencies

*******************************************************************************

requirements.txt example:

streamlit
python-dotenv
transformers
torch
langchain
langchain-openai
openai
requests

*******************************************************************************

🚀 12. Results & Performance

*******************************************************************************

| Component         | Model       | Average Response Time | Output Quality           |
| ----------------- | ----------- | --------------------- | ------------------------ |
| Image Captioning  | BLIP        | ~3s                   | High                     |
| Story Generation  | GPT-3.5     | ~2–4s                 | Very High                |
| Speech Generation | ESPnet VITS | ~5–6s                 | Good                     |
| Overall Latency   | -           | ~10–15s total         | Smooth, Real-time Usable |


*******************************************************************************
*******************************************************************************

🧭 Conclusion

*******************************************************************************
*******************************************************************************


The Image-to-Speech GenAI Tool exemplifies how modern AI components can be orchestrated to form intelligent, multimodal systems that bridge vision, language, and sound.

This project demonstrates:

The power of integrating vision + language + speech models

Practical use of LangChain for chaining AI tasks

Secure API key handling via dotenv

Usable deployment through Streamlit

It represents a robust, scalable prototype for future AI storytelling, assistive technologies, and creative content generation platforms.

*******************************************************************************
*******************************************************************************



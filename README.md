# AI-Powered Interactive Learning Assistant for Classrooms

Welcome to the AI-Powered Interactive Learning Assistant! 🚀

This is an open-source, free, and low-hardware-intensive project designed especially for students and educators! Our goal is to bring the power of AI right into your classroom, making learning more interactive, engaging, and accessible for everyone.

Think of this project as your personal **AI-Powered Multi-Modal Learning Hub**. It's a smart web application that runs entirely on your own computer, allowing you to interact using text, your voice, or even images to get intelligent answers from local AI models. The best part? Because it runs locally, your data always stays private and you can use it even without an internet connection!

---

## ✨ What Can It Do? (Features)

We've packed this learning assistant with features to make your study sessions smarter and more fun:

-   **Talk, Type, or Show! (Multi-Modal Interaction)**: Got a question? Just type it out, speak into your microphone, or upload a picture (like a diagram or a math problem!). Our assistant understands them all.
-   **Smart AI, Right on Your Device (Powerful Local AI)**:
    -   For Text: We use **TinyLlama-1.1B** to understand your questions and give helpful, clear answers.
    -   For Images: The **BLIP-base** model helps the assistant "see" and understand what's in your pictures, so you can ask questions about what you're looking at.
-   **Easy to Use (Web-Based Interface)**: We built a clean and simple interface using HTML, CSS, and JavaScript, all powered by a Flask backend. It's super easy to navigate!
-   **Hands-Free Learning (Voice-to-Text)**: Speak your questions naturally! Our integration with your browser's Web Speech API makes asking questions effortless.
-   **Never Forget a Lesson (Query History)**: All your questions and the AI's answers are saved automatically, so you can review them anytime.
-   **Gets Smarter Over Time (Feedback Loop)**: You can tell us if an answer was "Good"! When you do, the system remembers that perfect answer for similar questions in the future, making it faster and even more accurate.
-   **Your Data Stays Yours (Privacy-Focused)**: Since everything runs on your computer, none of your information ever leaves your device. Your learning is your business!

---

## 🏗️ How It Works (System Architecture)

Our learning assistant is a smart web server that brings together different local AI models to understand your questions, no matter how you ask them.

+-----------------------------------------------------------------+
|               Web UI (index.html, style.css, script.js)         |
| [Text Input]      [Image Upload]      [Voice Input (Mic)]     |
+-----------------------------------------------------------------+
|                           |                           |
| (text)                    | (image + optional text)   | (transcribed text)
|                           |                           |
V                           V                           V
+-----------------------------------------------------------------+
|              Flask Backend (app.py)                           |
|-----------------------------------------------------------------|
|                               |                                 |
|     +------------------------+                                 |
|     | If Image is present:   |                                 |
|     |   1. Save Image        |                                 |
|     |   2. Analyze w/ BLIP -> [Image Description]               |
|     +------------------------+                                 |
|                               |                                 |
|  [User Query] + [Image Description (if any)] -> [Final Prompt] |
|                               |                                 |
|                               V                                 |
|             +------------------+                                |
|             |  LLM (Llama GGUF)  | -> [Generated Answer]         |
|             +------------------+                                |
|                               |                                 |
|                               V                                 |
| +-------------------------------------------------------------+ |
| |   Response sent back to Web UI for display                  | |
| +-------------------------------------------------------------+ |
|                                                                 |
|--- Data Storage (Local JSON files) ---------------------------|
|   - saved_results.json (Query History)                        |
|   - feedback_data.json (User Feedback)                        |
+-----------------------------------------------------------------+


---

## 🛠️ Get Started! (Setup and Installation)

Ready to bring your AI learning assistant to life? Just follow these simple steps!

### 1. What You Need (Prerequisites)

Make sure you have:

-   Python 3.8+
-   Git

### 2. Get the Code (Clone the Repository)

Open your terminal or command prompt and run:

```bash
git clone [https://github.com/NarayanTheRocker/AI-Interactive-Learning-Assistant.git](https://github.com/NarayanTheRocker/AI-Interactive-Learning-Assistant.git)
cd AI-Interactive-Learning-Assistant
3. Set Up Your Workspace (Create a Virtual Environment)
This keeps your project's files organized and separate from other Python projects.

For Windows:

Bash

python -m venv venv
venv\Scripts\activate
For macOS/Linux:

Bash

python3 -m venv venv
source venv/bin/activate
4. Install What's Needed (Install Python Dependencies)
Now, install all the necessary libraries:

Bash

pip install -r requirements.txt
5. Download the Brains! (Download AI Models)
This is important! You need two models: one for images (BLIP) and one for text (TinyLlama).

A) Get the BLIP Model (Automated Script)

We have a script to do this for you! Run:

Bash

python download_models.py
This will create a folder like AI_Models/blip-base in your home directory and download the BLIP model there. It will also print the exact path to this folder – keep this path handy!

B) Get the TinyLlama GGUF Model (Manual)

Click this link to download: tinyllama-1.1b-chat-v0.4.Q4_K_M.gguf

Create a folder on your computer to store this model, for example: C:\AI_Models\LLM (Windows) or /home/user/AI_Models/LLM (macOS/Linux). Save the downloaded .gguf file into that folder.

6. Tell the App Where to Find Them (Configure Model Paths in app.py)
You need to tell the application where you saved these models.

Open the app.py file in a text editor and find these lines near the top:

Python

# !!! IMPORTANT: Make sure this path to your GGUF model file is correct !!!
LLAMA_MODEL_PATH = r"C:\Users\91910\TinyLlama-1.1B-Chat-v0.4-GGUF\TinyLlama-1.1B-Chat-v0.4-Q4_K_M.gguf"

# !!! IMPORTANT: Paste the absolute path from Step 5A here !!!
BLIP_MODEL_PATH = r"C:/AI_Models/blip-base" # <-- CHANGE THIS
Update LLAMA_MODEL_PATH: Replace the example path with the full path to your downloaded .gguf file.

Update BLIP_MODEL_PATH: Replace the example path with the full path that was printed by the download_models.py script.

Example for Windows:

Python

LLAMA_MODEL_PATH = r"C:\AI_Models\LLM\tinyllama-1.1b-chat-v0.4.Q4_K_M.gguf"
BLIP_MODEL_PATH = r"C:\Users\YourUser\AI_Models\blip-base"
Example for macOS/Linux:

Python

LLAMA_MODEL_PATH = "/home/user/AI_Models/LLM/tinyllama-1.1b-chat-v0.4.Q4_K_M.gguf"
BLIP_MODEL_PATH = "/home/user/AI_Models/blip-base"
🚀 Let's Run It! (Running the Application)
You're almost there! Once everything is set up:

Make sure your virtual environment is activated.

Run the Flask server:

Bash

python app.py
Your terminal will show that the models are loading. Once they're ready, it will give you a URL, usually http://127.0.0.1:5000.

Open this URL in your web browser, and you're ready to start learning with your new AI assistant!

⚡️ Optional: Optimize the Image Model for Faster Performance
For even better performance on CPU, you can convert the BLIP image model into the OpenVINO™ Intermediate Representation (IR) format (.xml and .bin). This can significantly speed up image analysis.

How to Convert the Model
We've included a script, optimized_model.py, to handle this conversion for you.

Install additional libraries for the conversion:

Bash

pip install optimum[openvino]
Run the optimization script:

Bash

python optimized_model.py
This script will:

Find the downloaded blip-base model.

Convert it first to the ONNX format.

Then, convert the ONNX model to the OpenVINO IR format (.xml and .bin files).

Save the optimized model to a new directory, AI_Models/blip-base-ov/.

It will print the path to this new directory.

Using the Optimized Model
After the conversion is successful, you just need to update the BLIP_MODEL_PATH in app.py to point to the new OpenVINO model directory.

Example:

Change this:
BLIP_MODEL_PATH = r"C:\Users\YourUser\AI_Models\blip-base"

To this:
BLIP_MODEL_PATH = r"C:\Users\YourUser\AI_Models\blip-base-ov"

Now, when you run app.py, it will use the faster, optimized model!

📂 Project Files (Project Structure)
Here's how our project is organized:

.
├── uploads/                # Where your uploaded images are temporarily saved
├── app.py                  # The heart of the application, handling all the logic
├── download_models.py      # A handy script to download the BLIP model easily
├── optimized_model.py      # Script to convert the BLIP model to OpenVINO for better performance
├── index.html              # The web page you'll see (built with HTML, CSS, and JS)
├── saved_results.json      # (Auto-generated) Stores all your questions and the AI's answers
├── feedback_data.json      # (Auto-generated) Stores the feedback you give on AI responses
├── requirements.txt        # Lists all the Python libraries this project needs
└── README.md               # You're reading it!
🤝 Want to Help? (Contributing)
This is an open-source project, and we welcome contributions from everyone! If you have ideas for new features, ways to improve things, or spot a bug, please feel free to open an issue or submit a pull request. Your help makes this project better for all students!

📜 Legal Stuff (License)
This project is freely available under the MIT License. This means you can use, modify, and distribute it for free!

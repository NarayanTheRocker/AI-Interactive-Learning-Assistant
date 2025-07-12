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

## 🧠 AI-Powered Learning Assistant

Our learning assistant is a smart web server that brings together different local AI models to understand your questions, whether you submit text, images, or voice input. Here’s how it works:

---

### 1. Web UI

The frontend is built with **HTML**, **CSS**, and **JavaScript**, providing users with:

- **Text input** for typing questions.
- **Image upload** to send pictures along with optional text.
- **Voice input** via microphone, which is transcribed to text automatically.

All inputs are collected in the browser and sent to the backend for processing.

---

### 2. Flask Backend (`app.py`)

The backend is a **Flask** application that orchestrates the AI workflow:

#### 🔹 Image Handling (BLIP Model)
- If an image is provided, it is saved locally.
- The **BLIP (Bootstrapping Language-Image Pretraining)** model generates a description of the image.

#### 🔹 Prompt Construction
- The user’s question and the generated image description (if any) are combined into a **final prompt**.
- This ensures that both visual and textual context are considered.

#### 🔹 Language Model (LLM)
- The final prompt is sent to a local **LLaMA (GGUF)** model.
- It generates an answer, which can be factual, descriptive, or conversational.

#### 🔹 Response Delivery
- The generated answer is sent back to the **web UI** for display.

---

### 3. Data Storage

For persistence and long-term improvements, the system saves data locally in JSON format:

- `saved_results.json`: Stores a history of user queries and AI responses.
- `feedback_data.json`: Stores user feedback for future performance enhancement.

---

### ✅ Modular & Extensible

This modular design allows you to:

- Extend support for more AI models (e.g., OCR, speech synthesis).
- Customize how prompts are built and responses are displayed.
- Build a **fully offline-capable**, private learning assistant.

---



**⚙️ Getting Started**
Follow these steps to set up and run the AI-Powered Interactive Learning Assistant on your local machine.

**🚚 1. Get the Code (Clone the Repository)**
Open your terminal or command prompt and run:

git clone https://github.com/NarayanTheRocker/AI-Interactive-Learning-Assistant.git
cd AI-Interactive-Learning-Assistant

**🧱 2. Set Up Your Workspace (Create a Virtual Environment)**
Creating a virtual environment keeps your dependencies isolated from other Python projects.

For Windows:
python -m venv venv
venv\Scripts\activate
For macOS/Linux:
python3 -m venv venv
source venv/bin/activate

**📦 3. Install What's Needed (Install Python Dependencies)**
Install all the required libraries:
pip install -r requirements.txt

**🧠 4. Download the Brains! (Download AI Models)**
#You will need two models:
One for image captioning (BLIP)
One for text generation (TinyLlama)

**🟢 A) Download the BLIP Model (Automated)**
We provide a script to do this automatically:
python download_models.py
This will:
Create a directory like AI_Models/blip-base in your home folder.
Download the BLIP model into it.
Print the exact path – keep this path handy for later!

**🟢 B) Download the TinyLlama GGUF Model (Manual)**
Click here to download the TinyLlama GGUF model
Create a folder on your computer to store it. For example:

Windows:
C:\AI_Models\LLM

macOS/Linux:
/home/user/AI_Models/LLM

Save the .gguf file inside this folder.

**🛠️ 5. Configure Model Paths in app.py**
You need to tell the application where you saved these models.
Open the app.py file in your text editor and locate the following lines near the top:

!!! IMPORTANT: Make sure this path to your GGUF model file is correct !!!
LLAMA_MODEL_PATH = r"C:\Users\91910\TinyLlama-1.1B-Chat-v0.4-GGUF\TinyLlama-1.1B-Chat-v0.4-Q4_K_M.gguf"

# !!! IMPORTANT: Paste the absolute path from Step 4A here !!!
BLIP_MODEL_PATH = r"C:/AI_Models/blip-base"  # <-- CHANGE THIS
Update these paths to match your environment.

Example for Windows:
LLAMA_MODEL_PATH = r"C:\AI_Models\LLM\tinyllama-1.1b-chat-v0.4.Q4_K_M.gguf"
BLIP_MODEL_PATH = r"C:\Users\YourUser\AI_Models\blip-base"

Example for macOS/Linux:
LLAMA_MODEL_PATH = "/home/user/AI_Models/LLM/tinyllama-1.1b-chat-v0.4.Q4_K_M.gguf"
BLIP_MODEL_PATH = "/home/user/AI_Models/blip-base"
Make sure these are the exact full paths to the files and folders you created.

**🚀 6. Run the Application**
You're almost ready to go!
Make sure your virtual environment is activated.

Start the Flask server:
python app.py
After a few moments, your terminal will show logs indicating that the models are loading. When you see something like:
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
open that URL in your web browser. You are now ready to start learning with your AI-powered assistant!







**⚡️ Optional: Optimize the Image Model for Faster Performance**
For even better performance on CPU, you can convert the BLIP image model into the OpenVINO™ Intermediate Representation (IR) format (.xml and .bin). This can significantly speed up image analysis.

How to Convert the Model
We've included a script, optimized_model.py, to handle this conversion for you.

Install additional libraries for the conversion:
pip install optimum[openvino]
Run the optimization script:
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


And here is the code for `optimized_model.py` ready to be saved in its own file:

```python
import os
from pathlib import Path
from optimum.exporters.onnx import main_export
from openvino import convert_model, save_model
import shutil

def optimize_blip_model():
    """
    Finds the downloaded blip-base model, converts it to ONNX,
    and then converts it to OpenVINO IR format (.xml and .bin).
    """
    try:
        # Define the original model name and the paths
        model_id = "Salesforce/blip-image-captioning-base"
        home_dir = Path.home()
        original_model_path = home_dir / "AI_Models" / "blip-base"
        onnx_path = home_dir / "AI_Models" / "blip-base-onnx"
        openvino_path = home_dir / "AI_Models" / "blip-base-ov"

        # --- Verification Step ---
        print(f"🔍 Verifying the original model exists at: {original_model_path}")
        if not original_model_path.exists():
            print("\n❌ Error: The original BLIP model was not found.")
            print("Please run 'python download_models.py' first to download the required models.")
            return

        print("✅ Original model found.")

        # --- Step 1: Export to ONNX ---
        print("\n⏳ Step 1/2: Converting the model to ONNX format...")
        
        # Ensure the ONNX output directory exists
        onnx_path.mkdir(parents=True, exist_ok=True)
        
        # Use optimum.exporters.onnx.main_export to convert the model
        main_export(
            model_name_or_path=str(original_model_path),
            output=onnx_path,
            task="image-to-text",  # Specify the task for the BLIP model
            opset=13, # Using a stable opset version
            no_post_process=False,
        )

        print(f"✅ Successfully exported to ONNX format at: {onnx_path}")

        # --- Step 2: Convert ONNX to OpenVINO IR ---
        print("\n⏳ Step 2/2: Converting ONNX model to OpenVINO IR (.xml and .bin)...")

        # The main_export creates a 'model.onnx' file in the specified directory
        onnx_model_file = onnx_path / "model.onnx"

        if not onnx_model_file.exists():
             print(f"\n❌ Error: Could not find the generated ONNX model at {onnx_model_file}.")
             return

        # Convert the ONNX model to OpenVINO IR
        ov_model = convert_model(onnx_model_file)
        
        # Save the IR model (.xml and .bin)
        save_model(ov_model, openvino_path / "model.xml")

        # Copy tokenizer and other necessary files from the original model directory
        print("    > Copying tokenizer and configuration files...")
        openvino_path.mkdir(parents=True, exist_ok=True)
        for filename in os.listdir(original_model_path):
            if filename.endswith(('.json', '.txt')):
                shutil.copy(original_model_path / filename, openvino_path / filename)

        print("\n🎉 Optimization Complete! 🎉")
        print(f"✅ The optimized OpenVINO model is saved at: {openvino_path}")
        print("\n💡 To use it, update the 'BLIP_MODEL_PATH' in 'app.py' to this new path.")

    except ImportError:
        print("\n❌ Error: Required libraries are not installed.")
        print("Please run 'pip install optimum[openvino]' to install the necessary packages.")
    except Exception as e:
        print(f"\n❌ An unexpected error occurred: {e}")
        print("Please check the console for more details.")

if __name__ == "__main__":
    optimize_blip_model()

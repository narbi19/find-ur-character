# Find Ur Character

**Live Prototype:** https://narbi19.github.io/find-ur-character/

A 3D cartoon-avatar project that analyzes a portrait and transforms the detected facial characteristics into a Pixar/Disney-style clay character.

The project combines:

- `dlib` and OpenCV 68-point facial-landmark detection
- Facial geometry and color analysis
- Stable Diffusion XL image generation
- Real-time browser rendering with HTML5 Canvas
- A Gradio interface for Google Colab

## Live Interactive Prototype

The browser prototype is located in [`docs/index.html`](docs/index.html). It supports:

- Portrait photo upload
- Webcam capture
- Built-in sample portraits
- Gender, age, face-shape, and eye-size controls
- Skin, hair, and eye-color sampling
- A simplified facial-landmark overlay
- Live 3D-clay avatar preview
- Dynamic SDXL prompt construction

The browser prototype creates an immediate local Canvas preview. Neural image synthesis runs in the Python notebook because it requires a CUDA GPU and the Stable Diffusion XL model.

## Full Avatar Generator

Open [`Find_ur_char.ipynb`](Find_ur_char.ipynb) in Google Colab, enable a GPU runtime, and run the notebook cells.

The notebook:

1. Captures a portrait from the webcam or accepts an uploaded image.
2. Detects the face and 68 facial landmarks.
3. Measures face shape, cheeks, eyes, nose, lips, chin, jaw, and brows.
4. Samples skin, eye, and hair colors from stable regions.
5. Builds a detailed positive prompt and anti-realism negative prompt.
6. Uses `SG161222/RealVisXL_V4.0_Lightning` to generate the avatar.
7. Displays the generated image and detected “human DNA” characteristics in Gradio.

## How It Works

The portrait is first converted to grayscale for dlib face detection. The 68 landmark points are then used to calculate relative proportions and identify likely facial features.

For example, the system compares:

- Face height and width for elongated, balanced, or wide facial proportions
- Eye height relative to face height for eye size
- Cheek and jaw landmark distances for fullness and structure
- Nose and lip proportions for feature descriptions
- Average brightness in forehead and cheek zones for skin tone

These values are converted into weighted prompt terms. Terms such as `massive expressive eyes`, `full chubby cheeks`, `matte vinyl skin`, and `octane render` encourage a consistently stylized 3D character appearance.

## Technology

- Python
- Google Colab
- OpenCV
- dlib
- NumPy
- PyTorch
- Diffusers
- Hugging Face Stable Diffusion XL
- Gradio
- HTML, CSS, and JavaScript
- HTML5 Canvas

## Run the Colab Notebook

1. Upload `Find_ur_char.ipynb` to Google Colab.
2. Set **Runtime > Change runtime type > T4 GPU**.
3. Run the installation cells.
4. Download the dlib 68-point landmark model when prompted.
5. Run the webcam capture and Gradio interface cells.

The notebook loads the SDXL Lightning model and runs diffusion inference with 8 steps.

## Repository Structure

```text
3D_cartoon_avatar/
├── Find_ur_char.ipynb
├── README.md
└── docs/
    └── index.html
```

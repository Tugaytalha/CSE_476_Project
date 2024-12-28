# NarraPhon: A Text-to-Speech System

NarraPhon is a text-to-speech (TTS) project that leverages the power of StyleTTS2 and Whisper models to generate natural-sounding speech from text input. This README will guide you through setting up the necessary environment and running the project.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

-   **Git:** For cloning the repository and managing large files.
-   **wget:** For downloading Miniconda.
-   **Bash/Zsh:**  The installation instructions assume you are using either Bash or Zsh as your shell.

## Installation

Follow these steps to set up the environment and install NarraPhon:

### 1. Install Miniconda

This will create a `miniconda3` directory in your home folder and install Miniconda into it.

```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```

**Important:** Restart your shell (e.g., close and reopen your terminal) for the changes to take effect.

### 2. Create and Activate Conda Environment

This creates a new Conda environment named "mooc" with Python 3.10.12 and activates it.

```bash
conda create -n mooc python=3.10.12
conda activate mooc
```

### 3. Clone the NarraPhon Repository and Install System Dependencies

Update the package list and install necessary system packages.

```bash
apt update
```

Clone the project repository and navigate into it.

```bash
git clone https://github.com/Tugaytalha/NarraPhon.git
cd NarraPhon
```

Install necessary system dependencies for text to speech, audio processing, and handling documents.

```bash
sudo apt-get install espeak-ng
sudo apt-get install ffmpeg
apt install poppler-utils
sudo apt-get install libreoffice
```

### 4. Download StyleTTS2 Model and Reference Audio

Install Git Large File Storage (LFS).

```bash
apt install git-lfs
```

Clone the StyleTTS2 model from Hugging Face (this may take some time due to the model's size).

```bash
git-lfs clone https://huggingface.co/yl4579/StyleTTS2-LibriTTS
```

Move the downloaded model and reference audio files to their appropriate locations within the project.

```bash
mv StyleTTS2-LibriTTS/Models .
mv StyleTTS2-LibriTTS/reference_audio.zip .
unzip reference_audio.zip
mv reference_audio Demo/reference_audio
```

### 5. Install Python Packages

Install the required Python packages, including the OpenAI Whisper model.

```bash
pip install -r requirements.txt
pip install git+https://github.com/openai/whisper.git
```

## Usage

After completing the installation steps, you are now ready to use NarraPhon.

(Add instructions on how to use your application here. For example, you might have a script that needs to be run or specific commands to generate speech).

**Example:**

```bash
python app.py
```

After running the script, you should see the link to the local server and a live DNS where you can access the web interface.

## Troubleshooting

-   **Conda environment issues:** If you encounter problems with the Conda environment, ensure you have restarted your shell after installing Miniconda. You can also try deactivating and reactivating the environment:
    ```bash
    conda deactivate
    conda activate mooc
    ```
-   **Model not found:** Double-check that you have correctly moved the `Models` directory and `reference_audio` files to the specified locations in step 4.
-   **Dependency errors:** If you face errors during the installation of Python packages, make sure you are using the correct Python version (3.10.12 as specified in the Conda environment).
-   **ImageMagick (libmagic) Issues:** Some features may require ImageMagick. If you encounter errors related to ImageMagick, follow these steps:
    1. **Installation:**
        ```bash
        sudo apt-get update
        sudo apt-get install imagemagick
        ```
        Verify installation:
        ```bash
        convert --version
        ```
    2. **Configuration:**
        Add to your `~/.bashrc` or `~/.zshrc`:
        ```bash
        export IMAGE_MAGICK_BINARY="/usr/bin/convert"
        ```
        Reload configuration:
        ```bash
        source ~/.bashrc  # or source ~/.zshrc
        ```
    3. **Security Policy (if needed):** If you still have issues, it might be due to ImageMagick's security policy.
        -   Locate the policy file (usually `/etc/ImageMagick-6/policy.xml` or `/etc/ImageMagick/policy.xml`).
        -   Edit with root privileges (e.g., `sudo nano /etc/ImageMagick-6/policy.xml`).
        -   Change `rights="none"` to `rights="read|write"` for relevant policies like `path` and `delegate`. Example:
            ```xml
            <policy domain="path" rights="read|write" pattern="@*" />
            <policy domain="delegate" rights="read|write" pattern="*" />
            ```
        -   Save the file and restart any services using ImageMagick.

## Contributing

Contributions are welcome! If you encounter any issues or have suggestions for improvements, please open an issue or submit a pull request on the GitHub repository.

## Acknowledgements

-   **StyleTTS2:**  We thank the creators of StyleTTS2 for their excellent work.
-   **OpenAI Whisper:** We acknowledge the developers of Whisper for their contribution to speech recognition.

```

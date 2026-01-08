🪟 Windows / 🍎 macOS Development Setup Guide for OM1

This guide describes how to set up OpenMind OM1 on Windows and macOS for local development.

🪟 Windows Setup (Tested on Windows 10 / 11)

Recommended: WSL2 (Ubuntu 22.04)
Native Windows Python is not recommended due to audio & dependency issues.

1️⃣ Install WSL2 (Ubuntu)

Open PowerShell (Admin):

wsl --install


Reboot, then install Ubuntu 22.04 from Microsoft Store.

2️⃣ Install system dependencies

Inside WSL Ubuntu:

sudo apt update
sudo apt install -y \
  git \
  python3 \
  python3-venv \
  build-essential \
  portaudio19-dev \
  ffmpeg

3️⃣ Install uv
curl -Ls https://astral.sh/uv/install.sh | sh
source ~/.bashrc
uv --version

4️⃣ Clone OM1
git clone https://github.com/OpenMind/OM1.git
cd OM1
git submodule update --init

5️⃣ Create virtual environment & install deps
uv venv
uv pip install -r requirements.txt

6️⃣ Configure environment variables
cp env.example .env


Edit .env and set your API keys.

7️⃣ Run a sample agent
uv run src/run.py conversation

⚠️ Windows Notes

Audio input/output requires WSL + PulseAudio

USB microphones may need additional WSL configuration

Native Windows Python is not officially supported

🍎 macOS Setup (Tested on macOS 13+)
1️⃣ Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2️⃣ Install system dependencies
brew update
brew install python ffmpeg portaudio git

3️⃣ Install uv
curl -Ls https://astral.sh/uv/install.sh | sh
source ~/.zshrc
uv --version

4️⃣ Clone OM1
git clone https://github.com/OpenMind/OM1.git
cd OM1
git submodule update --init

5️⃣ Create virtual environment
uv venv
uv pip install -r requirements.txt

6️⃣ Configure .env
cp env.example .env


Set required API keys.

7️⃣ Run agent
uv run src/run.py conversation

🍎 macOS Notes

Grant Microphone Access to Terminal

Apple Silicon (M1/M2/M3) works without Rosetta

If pyaudio fails, ensure portaudio is installed

✅ Common Issues
❌ ModuleNotFoundError
uv add <missing_package>

❌ pyaudio build error

Ensure:

portaudio19-dev (Linux)
brew install portaudio (macOS)

📌 Contribution Status

This guide was tested on:

Windows 11 (WSL2 Ubuntu 22.04)

macOS 13+ (Apple Silicon)
#  Research Paper Summarizer - Multi-Agent System 

This is a Python-based **multi-agent system** that automates research paper processing. It supports PDF ingestion (local or URL), topic classification, summarization, and generates an audio podcast version of the summary. All outputs are neatly saved in topic-specific folders for easy access and organization.

---

## 🚀 Setup Instructions

### ✅ Prerequisites

- Python 3.8 or later
- `pip` for installing packages
- Internet connection (for model and voice download)

### Installation

1. **Clone the Repository**
   git clone https://github.com/jharianeetu/Research-Paper-Summarization-Multi-Agent-System/blob/main/research_summarizer.zip
   cd research-summarizer

2. **Using a Virtual Environment (Recommended)**
   Create a virtual environment
     python -m venv venv
   
   Activate it
      On Windows:
          venv\Scripts\activate
      On Mac/Linux:
          source venv/bin/activate
   
4. **Install dependencies**
       pip install -r requirements.txt

5.**Run the Application**
       python main.py   


*******************************************************************
**System Architecture**

The system follows a clean, modular multi-agent pipeline:

User Input (PDF or URL)
   ↓
[IngestionAgent] → Extract text from PDF using pdfplumber
   ↓
[TopicClassifierAgent] → Classify research topic using zero-shot NLP
   ↓
[SummarizationAgent] → Generate summary using BART Transformer
   ↓
[PodcastAgent] → Convert summary to audio using gTTS
   ↓
Output (saved under output/<topic>/)

******************************************************************
**Multi-Agent Design & Coordination Approach**

The application consists of the following agents:

1. **IngestionAgent**
Extracts text from PDF using pdfplumber

Accepts both local file paths and direct PDF URLs

Handles downloading and temporary storage

2. **TopicClassifierAgent**
Uses a zero-shot classification transformer (like facebook/bart-large-mnli)

Predicts the research domain (e.g., AI, NLP, Robotics)

3. **SummarizationAgent**
Summarizes extracted text using facebook/bart-large-cnn

Handles long text by splitting it into manageable chunks

Includes an synthesis method for multi-paper capability

4. **PodcastAgent**
Converts summary text to MP3 audio using Google Text-to-Speech (gTTS)

Saves audio and summary in output/<topic_name>/ folder

***********************************************************************

**Paper Processing Methodology**

1.User provides a PDF file or a direct URL

2.System downloads and reads the PDF

3.Full paper text is extracted using pdfplumber

4.Topic is classified using a zero-shot transformer

5.The extracted text is summarized

6.The summary is saved to a .txt file

7.The summary is converted to audio podcast (.mp3)

8.All results are saved in:

output/
  └── <topic_name>/
      ├── summary.txt
      └── podcast.mp3

*******************************************************************************

**Audio Generation Implementation**

.Uses gTTS to generate audio from text

.Output is saved as MP3 file

.Each audio file is organized into folders based on topic:
     output/<topic>/podcast.mp3
     
.Audio is natural-sounding and plays on all devices

******************************************************************************
**Output Structure Example**

After processing a research paper classified under "Natural Language Processing", the structure looks like:

output/
└── Natural Language Processing/
    ├── summary.txt
    └── podcast.mp3

*******************************************************************************

**Sample Input and Output**
Input:
A sample research PDF file on Cybersecurity (research_summarizer\sample_pdf\Cybersecurity.pdf)

Output:
A folder: research_summarizer\output\Cybersecurity

summary.txt — contains the generated summary

summary.mp3 — audio version of the summary

*****************************************************************************

**Limitations**

No OCR: Image-only PDFs are not supported

English only: Summarization and audio are in English

Summaries may simplify complex technical details

****************************************************************************
**Future Improvements**

Integrate Tesseract for OCR of scanned documents

Add support for multilingual summarization

Improve model with domain-specific fine-tuning

Build an interactive web UI using Streamlit/Gradio
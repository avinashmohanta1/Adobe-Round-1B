Round 1B – Persona-Based Intelligence Extractor (Adobe Hackathon)
This project processes a given persona and job-to-be-done and intelligently extracts relevant sections from PDF reports. It is designed for offline use and delivers clean, ranked JSON outputs that highlight the most useful insights for the selected persona.

🔍 Objective
The goal of this project is to build a smart PDF processor that:

Understands a persona and their information need (job)

Reads PDF files from an input folder

Extracts and ranks the most relevant sections based on keyword and intent matching

Outputs structured JSON that can be used in further stages like visual display (e.g., Round 2)

This is done entirely offline, without internet access or large external models.

📁 Folder Structure
The project follows a clean and modular structure inside the round1b_persona_intelligence/ folder:

📁 input/ – This folder contains the PDF files that are to be analyzed. You should place your input .pdf files here.

📁 output/ – After running the script, the results are saved as structured JSON files in this folder.

📄 persona.json – A small JSON file where you define the persona and their job-to-be-done. This acts as the query/input for the system.

📄 persona_extractor.py – This is the main Python script that processes PDFs, extracts relevant sections, ranks them, and writes the output.

📄 requirements.txt – Lists the Python dependencies required to run the script. Use it to quickly install everything with pip install -r requirements.txt.

📄 Dockerfile – (Optional) You can use this to run your solution inside a Docker container as expected in the hackathon.

📄 README.md – Documentation that explains the setup, execution, and overall approach for Round 1B.

🧠 How It Works (Logic Overview)
Reads persona.json to understand the target persona and their job-to-be-done.

Loads all .pdf files from the /input folder using PyMuPDF.

Scans text from each page, and runs basic ranking using keyword matching based on the job description.

Uses langdetect to optionally detect non-English sections (multilingual support).

Creates an output JSON file that contains:

Input persona and job

Timestamp

A ranked list of relevant sections with page numbers

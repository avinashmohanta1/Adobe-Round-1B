Approach – Round 1B: Persona-Based Intelligence Extractor
The core objective of this round is to go beyond generic PDF parsing and extract persona-specific insights from any PDF document. Given a user persona and their job-to-be-done, our system scans the document and outputs only the most relevant sections, ranked by importance. The focus is on offline execution, speed, and flexibility — without using any heavy ML models or internet services.

We use PyMuPDF (fitz) to parse the PDF and keyword-matching logic to filter sections based on the persona’s needs. Additionally, langdetect is used for multilingual support, ensuring non-English content is appropriately identified.

⚙ Step-by-Step Process
1️⃣ Reading the Persona
The script starts by reading persona.json, which contains:

A persona (e.g., “Investment Analyst”)

A job_to_be_done (e.g., “Analyze revenue trends, R&D investments...”)

This defines the intent and guides the ranking logic.

2️⃣ Reading the PDF
All .pdf files inside the /input folder are processed.

Using PyMuPDF, we iterate through each page of each document.

The page content is extracted using page.get_text("dict"), giving access to individual spans (blocks of text).

3️⃣ Language Detection (Multilingual Support)
Using langdetect, we test each block of text to detect if it’s in English or another language.

This allows us to:

Include non-English content in the future

Warn or skip unsupported languages

Prepare for multilingual extensions in Round 2

4️⃣ Section Filtering & Relevance Scoring
Text blocks are split into lines.

Each line is checked for keywords from the job_to_be_done.

A basic scoring system ranks sections by counting how many keywords are matched.

High-scoring sections are assumed to be important and are selected for the output.

Example keywords for an investment analyst might include:

revenue, income, R&D, growth, strategy, market, competitor, innovation

5️⃣ Output Structuring
Each relevant section is saved in the output JSON with:

📄 Document name

📄 Page number (1-indexed)

📌 Extracted section text

⭐ Importance rank (higher score = higher rank)

Example:

json
Copy
Edit
{
  "document": "annual_report.pdf",
  "page_number": 5,
  "section_title": "The TPS review of UI Revenue Operations completed April 30",
  "importance_rank": 1
}
This output is saved in /output/persona_output.json.

6️⃣ Automation Across Files
All .pdf files in the /input folder are processed in a loop.

The script can handle multiple PDFs and append results.

Fully compatible with Adobe's expected Docker directory structure.

⚡ Performance & Efficiency
Entire pipeline runs in under 10 seconds for medium-sized PDFs (up to 50 pages).

No internet access required ✅

No GPU or external dependencies ✅

Lightweight: runs in Docker or native Python with minimal setup ✅

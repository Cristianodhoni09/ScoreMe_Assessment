🧾 Table Extractor

This project provides a Python-based solution for extracting structured transaction data from system-generated bank statement PDFs. Each transaction is expected to span two lines, following a consistent format that includes Date, Transaction Type, Description, Amount, and Balance. The extracted data is then saved as a clean, structured Excel spreadsheet.
🚀 Features

    🔍 Automatically detects transaction lines using date patterns.
    🧠 Handles two-line structured records (date, type, description, amount, balance).
    📄 Supports multi-page PDF documents.
    📤 Exports cleanly formatted tables to .xlsx using pandas and openpyxl.
    🧾 Designed for text-based system-generated PDFs (not scanned/image PDFs).

📂 Folder Structure

project/
├── extractor.py                 # Main extraction script
├── sample_input/
│   └── test31.pdf              # Sample input PDF
├── output/
│   └── extracted_tables.xlsx   # Generated output Excel
└── README.md                   # Project documentation

💾 Dependencies

To run this project, you'll need the following Python libraries installed:

pip install pdfplumber pandas openpyxl

These libraries handle:

    pdfplumber: Parsing and reading structured text from PDF pages.
    pandas: Organizing extracted data into structured tables.
    openpyxl: Writing the DataFrame to an Excel sheet.

🧠 Logic & How It Works

The script is crafted to work with PDFs where transactions follow this pattern:

04-Apr-2022 T   BY 06971000010040                        25,000.00     30,38,234.66Dr
04-Apr-2022 C   By Cash                                  40,000.00     29,98,234.66Dr

🧩 Extraction Process

    Step 1: Reads each page of the PDF using pdfplumber.
    Step 2: Splits page text into lines.
    Step 3: Detects a transaction using a date pattern \d{2}-[A-Z][a-z]{2}-\d{4} (e.g., 04-Apr-2022).
    Step 4: Combines each transaction’s two lines into one logical unit.
    Step 5: Extracts:
        Date: from the first segment.
        Type: either T or C, indicating transaction nature.
        Description: all remaining text excluding numeric values.
        Amount: the second-to-last number in the line.
        Balance: the final number before the string "Dr".

📤 Output Format (Excel)

Each extracted transaction is saved in the following tabular format:
Date 	Type 	Description 	Amount 	Balance
04-Apr-2022 	T 	BY 06971000010040 	25,000.00 	30,38,234.66
04-Apr-2022 	C 	By Cash 	40,000.00 	29,98,234.66
🛠 Usage Instructions
Copy your PDF file (bank statement) into the sample_input/ folder.
In extractor.py, set the input file path:

input_pdf = "sample_input/your_pdf.pdf"

Run the script:

python extractor.py

Your output will be saved at:

output/extracted_tables.xlsx

⚠️ Limitations

    ❌ This script does not work with scanned image PDFs or OCR-based documents.
    📄 Only works for transaction-style documents with date-based two-line structures.
    🧾 If your PDF contains Excel-style tables, a different logic (page.extract_table()) should be used.


# 💰 Transaction Log Extractor

---

## 📌 Overview

**Transaction Log Extractor** is a robust Python script designed to parse unstructured, multiline text logs and accurately extract structured financial transaction data. The project focuses on the core task of **Regular Expression (Regex) Capture**, transforming messy log entries into clean, actionable data tuples.

* The system uses **Python's `re` module** to match a specific, strict log pattern, filtering out noise and irrelevant data.
* It automatically handles complex **numeric parsing**, specifically converting comma-separated strings (like `1,250.50`) into precise floating-point numbers.

Built with **Python** and leveraging **Regex Mastery**, this solution addresses the critical challenge of converting raw log streams into structured transaction records for analysis or auditing.

---

## 🛠️ Features

* 🔎 **Regex-only Parsing**: Uses a single, high-performance regex pattern for extraction, avoiding slow string manipulation.
* 🔢 **Numeric Robustness**: Correctly parses amounts with or without thousands separators (commas) and decimal points.
* ✨ **Noise Tolerance**: Ignores malformed entries, random log lines, and non-conforming formats, ensuring data integrity.
* 📝 **Strict Pattern Matching**: Enforces a case-sensitive match for field labels (`TXN:`, `AMT:`, `ID:`) to maintain data source fidelity.
* 🧹 **Whitespace Agnostic**: Tolerates variable whitespace around the pipe (`|`) delimiters (`\s*\|\s*`).

---

## 🔁 Workflow
Input raw, multiline 'transactions.log' content into the function.

Compile and execute the regex pattern across the entire log text.

For each successful match, capture the three key groups (Type, Amount, ID).

Remove commas from the captured Amount string.

Convert the cleaned Amount string to a float.

Store the (Type, float Amount, ID) as a tuple in a list.

Return the final list of structured transaction tuples.
---

## 🚀 Technologies Used

* 🐍 **Python 3.x**: The core programming language.
* ⚙️ **`re` (Regular Expressions)**: The primary tool used for pattern matching and data extraction.
* 💻 **Jupyter Notebook**: The development and execution environment.
* 📚 **`typing`**: Used for type hinting (e.g., `List[Tuple[str, float, str]]`) to ensure code clarity and maintainability.

---

## 🧪 Sample Extraction Code

```python
import re
from typing import List, Tuple

def extract_transactions(log_text: str) -> List[Tuple[str, float, str]]:
    
    # Pattern to match numbers with optional commas and decimals
    amount_pattern = r"(?:\d{1,3}(?:,\d{3})+|\d+)(?:\\.\\d+)?"
    
    # Main pattern: captures Type (1), Amount (2), and ID (3)
    pattern = rf"TXN:([A-Z]+)\s*\\|\s*AMT:({amount_pattern})\s*\\|\s*ID:([A-Za-z0-9]+)"
    
    results: List[Tuple[str, float, str]] = []
    
    # Iterate over all non-overlapping matches
    for m in re.finditer(pattern, log_text):
        txn_type = m.group(1)
        # Convert to float after removing commas (handling "1,250.50" -> 1250.5)
        amount_val = float(m.group(2).replace(",", "")) 
        txn_id = m.group(3)
        results.append((txn_type, amount_val, txn_id))
        
    return results
```
# Example Test
log = 'TXN:CREDIT | AMT:1,250.50 | ID:AB123\\nTXN:DEBIT | AMT:500 | ID:XY789'
extracted = extract_transactions(log)
print(extracted)
📈 Summary Metrics
Based on the execution against the provided log file:

Total Records Found: 54

Unique Transaction Types: 11

Total Extracted Value: $136,177.37

Most Frequent Type: DEBIT (10 instances)

🖼️ Outputs
The final output is a list of structured tuples, ready for downstream processing:

Sample Extracted Data

('CREDIT', 1250.5, 'AB123')
('DEPOSIT', 12345.67, 'DEP12345')
('DEBIT', 500.0, 'XY789')
...

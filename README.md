# Transaction-Value-Extractor
Transaction Log Extractor
This project provides a code to parse and extract structured transaction data from a raw log file
📝 Overview
The script, contained within the Jupyter Notebook task 1.ipynb, uses Regular Expressions (regex) to identify and extract three key pieces of information from each valid transaction entry:

Transaction Type (TXN:)

Amount (AMT:)

Transaction ID (ID:)

It is designed to handle variations in whitespace and comma separators in the amount field, while filtering out noise and malformed entries.

🚀 Setup and Execution
Prerequisites
Python 3.x



# Stirling-PDF v1.3.2 - CSV Formula Injection

### Summary
CSV Formula Injection in Stirling-PDF v1.3.2: when converting PDF content to CSV the application does not neutralize cell values that begin with characters treated as formulas by spreadsheet software (for example =, +, -, @). A malicious PDF (or PDF containing attacker-controlled metadata) can inject spreadsheet formulas into exported CSVs; when a user opens that CSV in Excel/LibreOffice the formula is evaluated in the user’s spreadsheet context.

### PoC
Prepare a crafted CSV file, then export it to pdf.
<img width="940" height="287" alt="image" src="https://github.com/user-attachments/assets/c2f5d03b-5053-4cd6-b3b5-a6fb6fc4c02e" />
Navigate to "PDF to CSV" function, upload the exported pdf.
<img width="940" height="663" alt="image" src="https://github.com/user-attachments/assets/ba251205-d450-4a5c-839e-f092371bfb7a" />
Extract it.
<img width="940" height="465" alt="image" src="https://github.com/user-attachments/assets/0a287573-6f4d-4f81-a522-72d18d9d90de" />
Open the downloaded file.
<img width="940" height="459" alt="image" src="https://github.com/user-attachments/assets/6c9aebba-4ac9-4659-8537-41976f45ece3" />
Formula triggered.
<img width="940" height="354" alt="image" src="https://github.com/user-attachments/assets/26771a13-2060-4276-80d6-34e0a675b838" />

# Hash-Based Patient Identification on Registry submission

This repository contains a lightweight, secure, and reproducible method for hash-based deidentification in patient registries using Google Workspace tools (AppSheet + Google Sheets + Apps Script).

🔒 **Goal**: Enable anonymous, consistent patient tracking across submissions without risking reidentification.


## 🔧 Features

- SHA-256-based hashing function using a fixed salt  
- Integration with Google Apps Script triggered on data entry  
- Compatible with Google Sheets and AppSheet  
- One-way, deterministic hashing to enable anonymous longitudinal linkage  
- Spreadsheet-native design for rapid deployment and ease of use  
- Supports any clinical data submission tool

## 🧪 Live Test Spreadsheet

A live demo registry spreadsheet is available here:  
📎 [**Google Sheets Test Registry**](https://docs.google.com/spreadsheets/d/1heRFZB8s3mkwLX8RiM9hVUD9LU9jQq7l_pL_H3jDHiw/edit?usp=sharing)

## 🧬 How It Works

1. **AppSheet** collects patient-submitted or clinician-entered form data.  
2. Submissions are recorded in a Google Sheet.  
3. A Google Apps Script function (`checkAndHashNewRows`) is triggered on change.  
4. The script computes a SHA-256 hash of the patient ID (plus a salt).  
5. The hashed ID is stored in a hidden or protected column for deidentified record linkage.

## 🧑‍💻 Code Snippet

```javascript
function hashID(id, salt) {
  const raw = salt + id;
  const hash = Utilities.computeDigest(Utilities.DigestAlgorithm.SHA_256, raw);
  return hash.map(byte => ('0' + (byte & 0xff).toString(16)).slice(-2)).join('');
}

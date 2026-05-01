# 🏥 Medical System Management Project

A **Bash shell script** for managing medical test records stored in flat text files. The system provides a menu-driven CLI for adding, searching, updating, and analyzing patient medical test data.

---

## 📁 Repository Structure

| File | Description |
|------|-------------|
| `shell.sh` | Main program — 310-line interactive Bash script |
| `midecalRecord.txt` | Patient medical test records (data file) |
| `medicalTest.txt` | Reference file with normal ranges per test type |

---

## ⚙️ How It Works

The system runs entirely in the terminal. On launch it checks that `midecalRecord.txt` exists, then presents a looping menu with 5 options:

```
1) Add a new medical test record
2) Search for a test by patient ID
3) Average test value
4) Update an existing test result
5) Exit
```

---

## 🧾 Record Format

Each record stored in `midecalRecord.txt` follows this structure:

```
"id" : "name" , "year-month" , "result" , "status"
```

**Validation rules enforced on input:**
- `id` must be exactly **7 characters**
- `name` must be fewer than **5 characters**
- `year` must be **4 digits**, `month` must be **2 digits**
- `result` must be fewer than **5 characters**
- `status` must be fewer than **12 characters**

---

## 🔍 Feature Breakdown

### 1️⃣ Add a New Medical Test Record
Prompts the user for a new record, validates every field, and appends it to `midecalRecord.txt` only if all checks pass.

### 2️⃣ Search by Patient ID
Accepts a patient ID and opens a **nested sub-menu**:

| Sub-option | Action |
|------------|--------|
| 1 | Retrieve all tests for the patient |
| 2 | Retrieve only abnormal test results (compared against reference ranges) |
| 3 | Retrieve tests within a specific year/month period |
| 4 | Retrieve tests filtered by status (`completed` / `pending`) |
| 5 | Exit sub-menu |

Abnormal detection compares patient results against normal ranges read from `medicalTest.txt` for these test types: **Hgb**, **BGT**, **LDL**, **systole**, **diastole**.

### 3️⃣ Average Test Value
Calculates and displays the average result for each test type across all records:
- **RBC** — Red Blood Cell count
- **HGB** — Hemoglobin
- **BGT** — Blood Glucose Test
- **LDL** — Low-Density Lipoprotein (cholesterol)
- **SYS** — Systolic blood pressure
- **DIA** — Diastolic blood pressure

Uses `bc` for floating-point arithmetic with 2 decimal precision.

### 4️⃣ Update an Existing Test Result
Takes a patient ID (7 digits) and a test type (3 characters), locates the matching record, and uses `sed -i` to update the result value in-place inside `midecalRecord.txt`.

---

## 🚀 Setup & Usage

```bash
# Clone the repository
git clone https://github.com/yousefshanti/medical-system-mangment-project.git
cd medical-system-mangment-project

# Make the script executable
chmod +x shell.sh

# Run the program
./shell.sh
```

> **Requirement:** A Unix/Linux shell environment with `bc` installed for average calculations.

---

## 🛠️ Tech Stack

![Shell](https://img.shields.io/badge/Shell-Bash-green?logo=gnu-bash)
![Platform](https://img.shields.io/badge/Platform-Linux%20%2F%20Unix-lightgrey?logo=linux)
![Storage](https://img.shields.io/badge/Storage-Flat%20Text%20Files-blue)

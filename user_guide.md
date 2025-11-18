# [TEST] User Guide

# DataAnalyzer User Guide

## Table of Content

## Introduction

DataAnalyzer is a simple command-line tool designed to help users process large datasets quickly.  It allows you to import data (CSV or JSON format), export into a new file, run basic statistical operations (mean, median, and mode). 

This guide walks you through installation, basic commands, and an example use case in easy-to-understand steps.

---

## Features

- Import data from `.csv` or `.json`
- Calculate **mean**, **median**, and **mode**
- Export analysis results to a new file

---

## Tool Activity Flow

```
        ┌──────────────────────────────┐
        │            Start             │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  User opens Command Prompt   │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  User navigates to folder    │
        │  (C:\Users\Name\Documents)   │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  User runs DataAnalyzer.exe  │
        │  with input + options        │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  Tool reads input file       │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  Tool validates data         │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  Tool calculates statistics  │
        │  (mean / median / mode)      │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │  Tool writes output file     │
        │  (e.g., sales_analysis.txt)  │
        └─────────────┬────────────────┘
                      │
                      v
        ┌──────────────────────────────┐
        │            End               │
        └──────────────────────────────┘
```

---

## Getting Started

1. Requirements

No installation is required. Simply place the `DataAnalyzer.exe` file in any folder on your computer.

Note:
For example, place it in the Documents folder on your computer's C drive. The folder address will look like this:

```
C:\Users\Isnaini\Documents\DataAnalyzer.exe
```

1. Opening Your Command Line
    - **Windows:** Open *Command Prompt*
    - **Mac/Linux:** Open *Terminal*

1. Navigate to the folder containing the tool:

```
cd C:\Users\Isnaini\Documents
```

If successful, CMD will show:

```
C:\Users\Isnaini\Documents>
```

And you are now in the correct folder.

---

## How to Use the Tool

### Step 1: Importing a Data File

Run:

```
DataAnalyzer.exe --input data.csv
```

or for JSON:

```
DataAnalyzer.exe --input data.json
```

### Step 2: Choosing a Statistical Operation

You can select one or more operations:

```
--mean
--median
--mode
```

Example:

```
DataAnalyzer.exe --input data.csv --mean --median
```

### Step 3: Exporting the Results

To export results, use:

```
--output result.txt
```

Full example command:

```
DataAnalyzer.exe --input data.csv --mean --median --output result.txt
```

After pressing **Enter**, a new file will appear containing the results:

`result.txt`

### **Explanation**

- `DataAnalyzer.exe`
    
    The program you are executing.
    
- `--input data.csv`
    
    The CSV file you want to analyze.
    
- `--input data.json`
    
    The JSON file you want to analyze.
    
- `--mean`
    
    Calculates the **average**.
    
- `--median`
    
    Calculates the **middle value**.
    
- `--mode`
    
    Finds the **most frequent value**.
    
- `--output result.txt`
    
    The name of the output file that will be created.
    

---

## Example Use Case

You have a CSV file containing daily sales numbers. You want to understand your business performance without learning complex software.

**You can follow these steps:**

1. Place the file `sales.csv` and `DataAnalyzer.exe` in:

```
C:\Users\Isnaini\Documents
```

1. Open Command Prompt and navigate to Documents:

```bash
cd C:\Users\Isnaini\Documents
```

1. Run the analysis:

```
DataAnalyzer.exe --input sales.csv --mean --median --mode --output sales_analysis.txt
```

1. Open `sales_analysis.txt` to view:

```
Mean: 152.4
Median: 150
Mode: 148
```

This gives quick insight into your data in seconds.

---

## Tips

- Ensure the input file name is typed **exactly** as shown.
- Make sure your data file has numeric values only.
- If an error occurs, double‑check that your file is in CSV or JSON format.
- Keep the EXE and data files in the **same folder** for simplicity.
- Use `-help` to view all supported commands.

---

## Conclusion

DataAnalyzer makes statistical analysis simple, even for beginners. With just a few commands, you can turn raw data into meaningful insights.

Enjoy analyzing!
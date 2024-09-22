
# Healthcare Column Description Generator

This project utilizes a pre-trained **BioGPT** model to automatically generate concise and meaningful descriptions for healthcare-related database columns. The descriptions are generated based on column names provided in a CSV file, with the goal of helping data engineers and healthcare professionals better document and understand their datasets.

## Purpose

The tool aims to simplify and automate the generation of descriptions for healthcare database columns by leveraging a pre-trained language model. This is especially useful for large datasets where manually writing descriptions can be time-consuming.

## Features

- **Pre-trained BioGPT Model**: The project leverages **BioGPT** from Hugging Face, which is trained on biomedical text to generate human-like descriptions in the healthcare domain.
- **Post-Processing**: The tool includes custom cleaning functions to remove irrelevant characters and special tokens from the generated descriptions.
- **No Fine-Tuning Required**: The model works out-of-the-box, without needing additional training.

## Setup and Requirements

### 1. Files Needed

- **input.csv**: This file contains the names of the tables and columns for which descriptions are needed. The CSV should contain the following columns:
    - `table_name`: Name of the table (e.g., `patient_records`)
    - `column_name`: Name of the column (e.g., `heart_rate`)

    **Example:**

    ```csv
    table_name,column_name
    patient_records,heart_rate
    lab_results,hba1c_level
    medications,dosage
    ```

### 2. Installation of Libraries

Ensure you install the necessary Python libraries:

```bash
pip install datasets sacremoses
```


### 3. Load and Execute the Script

1. **Move the Input Files**

   Prepare the `input.csv` file and place it in the same directory where you plan to run the script.

2. **Run the Script**

   The script consists of the following key sections:

   - **Library Installation**: Installs required Python packages.
   - **Model Loading**: Automatically loads the pre-trained BioGPT model.
   - **Description Generation**: Reads the input CSV file and generates descriptions for each column using the model.
   - **Post-Processing**: Cleans the generated text, removing unwanted tokens and ensuring meaningful output.
   - **Saving Output**: Saves the generated descriptions to `output.csv`.

### 4. Generated Output

After running the script, the descriptions will be saved in `output.csv`, which will contain three columns:

- `table_name`: The name of the table.
- `column_name`: The column for which the description was generated.
- `description`: The generated description for the column.

**Example of `output.csv`:**

```csv
table_name,column_name,description
patient_records,heart_rate,The patient's heart rate measured in beats per minute.
lab_results,hba1c_level,The patient's HbA1c level indicating average blood sugar over the past 3 months.
medications,dosage,The prescribed dosage of the medication.
```

## Code Overview

### Key Functions:

1. **`load_model()`**: Loads the pre-trained BioGPT model and tokenizers.
2. **`generate_description()`**: Generates a description for a healthcare dataset column.
3. **`clean_generated_description()`**: Cleans up the generated text, removing unwanted tokens, symbols, and ensuring the description is concise.
4. **`process_input_csv()`**: Reads the input CSV, generates descriptions, and saves the output to a new CSV file.

### Cleaning Logic

- **Post-Processing**: The descriptions are cleaned using a custom function to ensure no special characters (`<`, `>`, etc.) or irrelevant tokens (`<|endoftext|>`, `▃`, etc.) appear in the final output.
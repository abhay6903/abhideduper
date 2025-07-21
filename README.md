README - PHY2 Normalization + MySQL Entity Search Pipeline

This repository implements an end-to-end normalization and entity resolution system using a fine-tuned Phi-2 model and a MySQL-connected search script.

--------------------------------------------------------------------------------
PIPELINE WORKFLOW (STEP-BY-STEP INSTRUCTION)
--------------------------------------------------------------------------------

1. RUNNING PHY2 MODEL FOR NORMALIZATION (on Google Colab)

- Open Google Colab.
- Go to Runtime > Change Runtime Type > Set Hardware Accelerator to "GPU".
- Make sure you upload all the files from phi2refined and data_normalization_phi2.jsonl onto your drive.
- Paste the fine-tuned Phi-2 inference/test script in the Colab notebook.
- Run the script to load the model and tokenizer.
- Input a raw query (e.g., "abhay panday, 44 near laxmi nagar delhi").
- The Phi-2 model will return a normalized version (e.g., "Abhay Pandey, 44 Laxmi Nagar, Delhi").

2. RUNNING LOCAL SEARCH SCRIPT (search.py)

- On your local machine, ensure MySQL is running and accessible.
- Ensure the `search.py` file is configured with the correct MySQL credentials.
- The script should use vectorization (TF-IDF or similar) and DBSCAN or cosine-based fuzzy matching.
- Run the script locally:

    python search.py

- This launches a local Gradio or Flask app (default on http://127.0.0.1:7860/).

3. INTERACTION BETWEEN THE TWO SYSTEMS

- Take the normalized query generated from the Phi-2 model in Colab.
- Paste it into the input box in the locally running `search.py` app.
- The app will search the connected MySQL table (e.g., "entity_records") for the best matching canonical record.
- The result returned is the resolved canonical entry (parent record) from the database.

4. REQUIREMENTS

- Google Colab with GPU runtime
- Local Python environment with:
    - mysql-connector-python
    - sklearn
    - pandas
    - numpy
    - rapidfuzz
    - gradio or flask (depending on implementation)
 
  Output : ![WhatsApp Image 2025-07-21 at 11 46 19_96fc46cd](https://github.com/user-attachments/assets/8cdb8848-1dab-4b08-8491-02abca34bb23)


--------------------------------------------------------------------------------
NOTES
- Tested with TinyLlama/Phi-2 based model and real-world entity variation records.

--------------------------------------------------------------------------------

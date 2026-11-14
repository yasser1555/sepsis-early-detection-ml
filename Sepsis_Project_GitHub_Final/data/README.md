# Dataset instructions

The full dataset is intentionally **not included** in this public repository.

- Original source: [PhysioNet / Computing in Cardiology Challenge 2019](https://physionet.org/content/challenge-2019/1.0.0/training/).
- Source license: [Creative Commons Attribution 4.0](https://physionet.org/content/challenge-2019/view-license/1.0.0/). Cite the original dataset if you reuse or adapt it.
- The academic project uses a **preprocessed** `Dataset.csv` containing **1,552,210** patient-hour records and 16 columns (including `SepsisLabel` and `Patient_ID`). It is derived from the challenge data, and is not identical to the source PSV files.
- To reproduce the saved notebook workflow, obtain or reconstruct the project's preprocessed `Dataset.csv` from the original PhysioNet records. The notebook's first loading cell prompts for a CSV upload in **Google Colab**.
- Do **not** upload individual patient records, protected clinical data, private patient information, local API keys, or checkpoints to this repository.

## Preprocessed CSV schema

`Hour, HR, O2Sat, Temp, SBP, MAP, DBP, Resp, Age, Gender, Unit1, Unit2, HospAdmTime, ICULOS, SepsisLabel, Patient_ID`

**Note:** The source PhysioNet dataset contains additional clinical columns that are not present in this project's reduced, preprocessed CSV; the included notebook was designed to use the reduced version.

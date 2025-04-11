# Lexid-qa2
Undergraduate Thesis - LexID-QA V2 - Development of Legal Question Answer Model with Knowledge Graph

---

## Bullet Points made simple
Developing Dataset and Building Pipeline Model consisted of Question Classification and Entity Extraction Model
- Goal: Compare Legal QA Model between BERT model with the baseline, Rule-Based model
- Transform free-text input from user into a Knowledge Graph Query Language
- The Question Dataset was created by paraphrasing 18 simple legal question types and the Answer was derived from the Knowledge Graph itself
- Fine-tuning BERT models as the Question Classification Model
- Entity recognition using BERT model to extract legal document’s title

Result of experimentation
- Bert model completely overthrown the Rule-Based model, due to the paraphrased question
- The BERT model performance is too high, nearly perfect
  - We can take an assumption, the question pattern is too easy for the BERT model, for instance, we can classify the question type by differentiating the verb and the structure

---

## Predecessor (LexID KG & LexID-QA)

- [LexID KG, the KG](https://github.com/ninggar17/Lexid)
- [LexID QA - Frontend](https://github.com/handi91/lexid-fe)
- [LexID QA - Backend, the baseline model](https://github.com/handi91/Lexid-be)

---

## How to navigate the unstructured page

**Starting point**
### Milestone 1: Creating the Legal QA dataset
1. Create list of paraphrased 17/18 question type from LexID KG by using chatGPT and manually create the question variations using paraphrased techniques and Indonesian Thesaurus. [List of paraphrased](https://github.com/rafifpriyo/Lexid-qa2/blob/master/Natural%20Language%20Questions.docx)
2. Extract the target entity (official legal document) from the LexID KG itself and populate the templates in point 1. [Populate ipynb](https://github.com/rafifpriyo/Lexid-qa2/blob/master/Question%20Generation%20Tesaurus%20(1).ipynb)
3. Dataset is ready

### Milestone 2: Fine-tune the Bert models
1. Search for Bert candidate, got three candidates, IndoBERT; MelayuBERT; MultilingualBERT
2. Train each one of them using the datasets
    - [IndoBERT](https://github.com/rafifpriyo/Lexid-qa2/blob/master/LexID%20QA2%20indoBERT%20Classification.ipynb)
    - [MelayuBERT](https://github.com/rafifpriyo/Lexid-qa2/blob/master/LexID%20QA2%20MelayuBERT%20Classification.ipynb)
    - [MultilingualBERT](https://github.com/rafifpriyo/Lexid-qa2/blob/master/LexID%20QA2%20multilingualBERT%20Classification.ipynb)
3. Evaluate each models on the respective ipynb

### Milestone 3: Evaluate the end-to-end pipeline with the baseline
1. Search for suitable [NER BERT](https://huggingface.co/kiipliwooke/KIPBERT) that have a LAW label
2. Evaluate the [end-to-end pipeline](https://github.com/rafifpriyo/Lexid-qa2/blob/master/LexID%20QA2%20App.ipynb)
3. Contrast with the [handi's Model](https://github.com/rafifpriyo/Lexid-qa2/blob/master/Handi_s%20LexID%20QA%20-%20Evaluation.ipynb)

### Result
![image](https://github.com/user-attachments/assets/3837370c-a003-4c36-a76f-34f0a0d2fadf)

**Finish Line**, Hooray

---

## Future Ideas (in Bahasa)

1. Melakukan fine-tuning terhadap model NER untuk mendapatkan kualitas ektraksi kalimat yang lebih baik.
2. Menambahakan label NER nomor pasal dan nomor ayat untuk menghindari ambiguitas pada kasus kata pasal atau kata ayat tidak terlabel oleh model NER.
3. Membuat dataset lebih objektif dengan menggunakan teknik-teknik parafrasa yang lebih terstruktur.
4. Memvalidasi dataset dengan ahli hukum.
5. Menambahkan data untuk jenis pertanyaan 14 dan 15, yaitu jenis pertanyaan ”Apa saja pasal yang dihapus dalam legal title?” dan ”Apa saja pasal yang ditambahkan dalam legal title?”. Bisa menambahkan data negatif, seperti yang jawabannya tidak ada yang dihapus atau ditambahkan, pada kedua jenis pertanyaan ini. Perhatikan persebaran entitas dokumen yang diambil serta persebaran dari data positf dan negatif.
6. Menambahkan variasi judul dokumen pada dataset. Dataset pada penelitian ini masih menggunakan judul dokumen secara penuh pada tiap kalimat pertanyaannya. Hal ini bisa dilakukan dengan
    - Menghapus beberapa kata dalam judul dokumen, contohnya pada judul dokumen "Menteri Riset Teknologi Dan Pendidikan Tinggi Republik Indonesia" bisa menjadi "Menteri Riset Teknologi" atau "Menteri Pendidikan Tinggi". Akan tetapi perlu dipastikan apakah penghapusan tersebut mengakibatkan ambiguitas atau tidak, seperti "Menteri Kebudayaan" bisa dipasangkan dengan entitas "Menteri Kebudayaan dan Pariwisata" serta "Menteri Pendidikan dan Kebudayaan”.
    - Menggunakan singkatan daripada judul dokumen penuh. Contohnya "Peraturan Pemerintah" menjadi "PP", "Undang-Undang Republik Indonesia" menjadi "UU", hingga "Peraturan Menteri Keuangan" menjadi "PMK" atau "Permenkeu".
7. Menambahkan jenis pertanyaan untuk cakupan informasi yang lebih luas. Hal ini didasarkan pada adanya informasi di LexID KG yang belum dibuat padananan jenis
pertanyaannya, seperti di mana atau kapan suatu dokumen diundangkan.
8. Menyelesaikan masalah semantik, terkait norma hukum. Hal ini bisa dilakukan dengan
    - Melakukan fine-tune lanjutan pada model klasifikasi untuk bisa membedakan antara pertanyaan yang sesuai dengan salah satu jenis pertanyaan dan yang tidak, yaitu memiliki kemungkinan menjadi pertanyaan semantik. Perhatikan overfit dari hasil fine-tune lanjutan.
    - Membuat model baru untuk mendeteksi entitas konsep dan entitas aksi karena pada pertanyaan semantik tidak disebutkan judul dokumen secara eksplisit.

bulgaria-imf-llm
This notebook reads the IMF's 2025 Article IV consultation for Bulgaria with two Gemini Flash models. It extracts summaries, themes, risks, indicators and trends from the report, then checks every model output against the report text.

Source document: IMF Country Report No. 25/306, Bulgaria: 2025 Article IV Consultation, Press Release; Staff Report; and Staff Supplement (November 2025, 66 pages). The PDF is in data/.

Contents
Path	What it holds
Bulgaria_IMF_LLM_Pipeline.ipynb	the notebook, saved with the outputs of its Colab run
data/	the IMF report
cache/replies.zip	every model reply of the recorded run, one JSON file per call
cache/chunk_vectors_*.npy	the gtr-t5-base vectors of the 141 chunks
artefacts/	all JSON outputs and the 300 dpi figures in artefacts/figures/
requirements.txt	package versions of the Colab runtime that produced the outputs
How to run
Open the notebook in Colab, with data/ and cache/ in the working directory.
Choose Runtime > Run all.
Every reply comes from cache/replies.zip, so the run needs no key and makes no model calls. To call the models again, store a Gemini API key as a Colab secret. The key_secret setting gives the secret's name and defaults to GEMINI_FREE_KEY. Then remove the archive.

Models in the recorded run: writer gemini-3.6-flash and judge gemini-3.5-flash-lite, both through the Gemini API. Retrieval uses sentence-transformers/gtr-t5-base with a FAISS IndexFlatL2, and cross-encoder/ms-marco-MiniLM-L-6-v2 reranks the results for the extension.

Note on the vectors: in the Colab run, PyTorch used a single CPU thread, and encoding the 141 chunks did not finish in 16 minutes. The chunk vectors were therefore encoded once with the same model, from the same chunk texts, on a local machine. The notebook loads them from cache/ because the cache key, a hash of the chunk texts and model name, matched. Deleting the file makes the notebook encode the chunks again.

Licence
MIT, see LICENSE. The IMF report remains the property of the International Monetary Fund and is included only so the notebook can run.

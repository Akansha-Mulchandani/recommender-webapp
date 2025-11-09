# SHL Assessment Recommender

End-to-end system to recommend SHL assessments from job descriptions or natural language queries.

## Project Structure

- /backend
- /frontend
- /data
- /experiments

## Setup

1) Create and activate a Python 3.10+ environment.
2) Install dependencies:

```
pip install -r requirements.txt
```

3) (Optional) Set Google Gemini API Key for reranking:

- On Windows PowerShell:
```
$env:GEMINI_API_KEY = "YOUR_KEY"
```

## Data

- Put/keep the uploaded Excel dataset in the project root as `Gen_AI Dataset.xlsx`.
- Crawl the SHL catalog (Individual Test Solutions only):

```
python data/crawl_shl_catalog.py
```
This creates `data/catalog.jsonl` and `data/catalog.parquet`.

- Process the dataset to CSVs for experiments:
```
python data/process_dataset.py
```

## Run Backend (FastAPI)

```
uvicorn backend.main:app --reload --port 8000
```

Health:
```
curl http://localhost:8000/health
```

Recommend:
```
curl -X POST http://localhost:8000/recommend -H "Content-Type: application/json" -d '{"query":"Java developer who collaborates well"}'
```

## Run Frontend (Streamlit)

```
streamlit run frontend/app.py
```

## Experiments

- Use `/experiments` for evaluation notebooks.

## Deployment

- Backend: Render/Railway/HF Spaces (FastAPI)
- Frontend: Streamlit Cloud or Hugging Face Spaces. Configure `API_BASE_URL` env in Streamlit to point to deployed backend.

# Shakespeare Autocomplete Project

A scratch-coded character-level LSTM autocomplete system with:
- preprocessing
- training script
- FastAPI backend
- React web editor UI
- Tab-to-accept inline autocomplete
- top suggestion box

## Data
Put your corpus here:

`data/Shakespeare.csv`

Preferred column:
- `PlayerLine`

The project also includes:
- `data/sample_shakespeare.csv`

If `Shakespeare.csv` is missing, the training script falls back to the bundled sample.

## Project structure

```text
backend/
  app.py
  infer.py
  model.py
  preprocess.py
  train.py
  artifacts/
frontend/
  src/
  package.json
  vite.config.js
data/
  Shakespeare.csv
  sample_shakespeare.csv
```

## Setup

### 1) Backend
```bash
cd backend
pip install -r ../requirements.txt
python train.py --data ../data/Shakespeare.csv
python app.py
```

If you do not have `Shakespeare.csv` yet, omit `--data` and the script will train on the sample data.

### 2) Frontend
```bash
cd frontend
npm install
npm run dev
```

## UI behavior

- Type in the editor.
- The predicted completion appears inline as ghost text.
- Press `Tab` to accept the suggestion.
- Top alternatives appear in the bottom-right suggestion box.
- Click a suggestion to insert it.

## Notes

- This is a character-level model.
- It predicts the next characters and converts that into a next-word autocomplete suggestion.
- For best results, train on the full `Shakespeare.csv` corpus.

## API

- `GET /health`
- `POST /predict`

Example:
```json
{
  "text": "to be or not to be",
  "top_k": 5,
  "temperature": 0.8
}
```


### Immediate demo mode
If you only want the UI to run immediately, use the bundled demo artifacts:

```bash
cd backend
python bootstrap_demo_artifacts.py
python app.py
```

Then open the frontend.

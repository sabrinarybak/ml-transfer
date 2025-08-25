# ml-transfer
kundrecension binär positiv /negativ
# Sentiment Analysis (Binary: Positive / Negative)

Klassificering av text (kundrecensioner) som **positiv** eller **negativ** med Hugging Face Transformers.

## Innehåll
- [Översikt](#översikt)
- [Dataset](#dataset)
- [Resultat](#resultat)
- [Miljö & installation](#miljö--installation)
- [Snabbstart](#snabbstart)
- [Träning & utvärdering](#träning--utvärdering)
- [Inferens (predict)](#inferens-predict)
- [Tips & felsökning](#tips--felsökning)
- [Projektstruktur](#projektstruktur)
- [Licens](#licens)

---

## Översikt
Det här projektet finjusterar en förtränad språkmodell för **binär sentimentanalys**. Målet är att kunna ta fri text (t.ex. kundomdömen) och avgöra om den uttrycker **positiv** eller **negativ** känsla.

**Modelltyp:** `AutoModelForSequenceClassification`  
**Tokenisering:** `AutoTokenizer`  
**Träningsloop:** `Trainer` + `TrainingArguments` (Transformers 4.55.4)

---

## Dataset
Exempel (som i IMDB-upplägget):
- `train`: 25 000 rader — features: `text`, `label`
- `test`: 25 000 rader — features: `text`, `label`
- `unsupervised`: 50 000 rader — features: `text`, `label`

> Etiketter förväntas vara `0 = negativ`, `1 = positiv`. Anpassa vid behov.

---

## Resultat

**Övergripande (test, n=1000):**
- **Accuracy:** 0.88  
- **Macro F1:** 0.8799  
- **Macro Precision:** 0.8834  
- **Macro Recall:** 0.8812  

**Klasspecifikt:**

| Klass     | Precision | Recall | F1   |
|-----------|-----------|--------|------|
| Negative  | 0.93      | 0.83   | 0.88 |
| Positive  | 0.84      | 0.93   | 0.88 |

**Tolkning:** Modellen är något mer **försiktig med negativa** exempel (hög precision, lägre recall) och mer **inkluderande för positiva** (hög recall, något lägre precision). Överlag stark och balanserad prestanda för baseline.

---

## Miljö & installation

> **Rekommenderad Python:** 3.11  
> (ML-stacken är stabilare här än på 3.13.)

**Virtuellt venv (exempel):**
```bash
python3.11 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# Osteovera

**Forensic biological profile estimation platform**  
osteovera.com

Osteovera is a browser-based platform for forensic anthropological analysis. It provides probabilistic biological profile estimates — age, sex, population affinity, and stature — from skeletal and fingerprint ridge breadth measurements.

> **Research tool only.** Output is probabilistic, not a determination. Must be interpreted by a qualified professional alongside all available case evidence.

---

## Models

| Module | Method | Accuracy |
|---|---|---|
| Age (subadult) | Fisher-KPP PINN with Riemannian metric | LOO-CV MAE 1.71 yr (ages 6–12) |
| Population affinity | LDA · Ledoit-Wolf shrinkage · Howells (n=2,524, 30 populations) | 87.84% 5-fold CV |
| Sex | MLP · Monte Carlo Dropout | 83.0% CV |

---

## Structure

```
osteovera/
├── index.html          # Full frontend — drop into Netlify to deploy
├── README.md           # This file
├── LICENSE             # MIT
└── backend/            # FastAPI backend (Railway)
    ├── osteovera_backend.py
    ├── inverse_pinn_shrinkage.py
    └── requirements.txt
```

## Deploy

**Frontend (Netlify):**  
Drag `index.html` into the Netlify dashboard. No build step required.

**Backend (Railway):**  
1. Fork this repo  
2. Connect to Railway  
3. Set environment variables: `JWT_SECRET`, `TESTING_MODE`  
4. Deploy — Railway auto-detects the Python service  

Update the `API` constant in `index.html` to your Railway URL.

---

## Data and Methods

All models are trained on reference data under appropriate ethical oversight. Cross-population validation (Greek n=200, American n=42) is reported in:

> Bhandare, N. (2026). A Riemannian Physics-Informed Neural Network for Subadult Age Estimation. *IEEE Transactions on Biomedical Engineering* (submitted).

Population affinity uses the public Howells craniometric dataset. Sex estimation uses a multilayer perceptron on the same dataset. Both comply with SWGANTH (2013) guidelines.

---

## Limitations

- Age model: ages 6–12 only, Greek/American reference populations
- Affinity model: 30 Howells reference populations only — not legal or ethnic categories
- No external validation on independent forensic casework
- All outputs require interpretation by a qualified forensic anthropologist

---

## Contact

niev841@gmail.com  
Rye Country Day School

---

## License

MIT — free to use, modify, and distribute. Attribution appreciated.  
Model weights and training notebooks available on request.

# Previsione del tempo nella mezza maratona

Progetto di tesi sull'analisi esplorativa e sulla previsione del tempo finale di una mezza maratona a partire da dati raccolti tramite questionario.

## Contenuto del repository

- [`data_analysis.ipynb`](data_analysis.ipynb): notebook completo per pulizia dei dati, analisi esplorativa, analisi del passo e confronto dei modelli predittivi.
- [`tesi.ltx`](tesi.ltx): sorgente LaTeX della tesi.
- [`requirements.txt`](requirements.txt): dipendenze Python con versioni fissate.

## Requisito dati

Il notebook legge un file locale chiamato `form_responses.csv` dalla stessa cartella di `data_analysis.ipynb`. Il file non è incluso nel repository.

Le colonne utilizzate dal notebook sono:

`Timestamp`, `sex`, `age`, `height`, `train_years`, `train_week`, `z2_train_week`, `fartelk_train_week`, `power_train_week`, `avg_km_week`, `sleep_hour`, `vo2_max`, `cadence`, `hm_time`, `mid_hm_time`.

I tempi `hm_time` e `mid_hm_time` devono essere nel formato `M:SS` oppure `H:MM:SS`. Il notebook converte il tempo finale in minuti (`hm_time_min`) e usa questo valore come variabile target.

## Installazione

Si consiglia di usare un ambiente virtuale:

```bash
python -m venv .venv
```

Attivare l'ambiente virtuale e installare le dipendenze:

```bash
python -m pip install -r requirements.txt
```

Per eseguire il notebook serve inoltre Jupyter Notebook o JupyterLab, se non già disponibile nell'ambiente Python.

## Esecuzione

1. Posizionare `form_responses.csv` nella root del progetto.
2. Avviare Jupyter dalla root:

   ```bash
   jupyter notebook
   ```

3. Aprire `data_analysis.ipynb` ed eseguire le celle in ordine.

Il notebook:

- ordina le risposte e rimuove/prepara le colonne necessarie;
- converte le variabili categoriche e i tempi in valori numerici;
- filtra i tempi finali superiori a 140 minuti;
- produce grafici e statistiche descrittive;
- analizza il passo sui primi 10 km e sulla parte restante della gara;
- addestra modelli di regressione e li confronta con RMSE, MAE e R².

Per la previsione vengono usate le feature `age`, `sex`, `height`, `avg_km_week`, `train_years` e `train_week`, con `hm_time_min` come target. Il notebook include regressione lineare, SVR, Random Forest, Gradient Boosting, XGBoost, Ridge, Lasso, Elastic Net e Gaussian Process, oltre a procedure di cross-validation e tuning degli iperparametri.

## Nota sulla riproducibilità

Il dataset contiene dati raccolti tramite questionario e non è versionato. I risultati dipendono quindi dal file `form_responses.csv` usato localmente. Il notebook usa `random_state=42` nei principali split e modelli stocastici.

## Tesi LaTeX

Per compilare `tesi.ltx` è necessario un ambiente LaTeX con i pacchetti usati nel preambolo, tra cui `babel`, `geometry`, `amsmath`, `graphicx` e `hyperref`.

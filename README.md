# Predizione della Sopravvivenza nei Pazienti con Insufficienza Cardiaca

## Panoramica del Progetto

L'obiettivo di questo progetto è analizzare dati clinici relativi a pazienti affetti da insufficienza cardiaca e sviluppare modelli di machine learning in grado di prevedere la probabilità di decesso durante il periodo di follow-up.

L'analisi comprende:

- Analisi esplorativa dei dati
- Test statistici inferenziali
- Preparazione e trasformazione delle variabili
- Costruzione di modelli predittivi
- Ottimizzazione degli iperparametri tramite Cross-Validation
- Confronto tra diversi algoritmi di Machine Learning
- Interpretazione dei risultati ottenuti

L'obiettivo finale è individuare i fattori clinici maggiormente associati alla mortalità e valutare la capacità predittiva dei modelli sviluppati.

---

## Dataset

Il progetto utilizza il dataset **Heart Failure Clinical Records**, contenente informazioni cliniche relative a pazienti affetti da insufficienza cardiaca.

### Variabile Target

- **DEATH_EVENT**
  - 0 = Paziente sopravvissuto
  - 1 = Paziente deceduto

### Variabili Disponibili

- Età (Age)
- Anemia (Anaemia)
- Creatinine Phosphokinase
- Diabete (Diabetes)
- Frazione di eiezione (Ejection Fraction)
- Ipertensione (High Blood Pressure)
- Piastrine (Platelets)
- Creatinina sierica (Serum Creatinine)
- Sodio sierico (Serum Sodium)
- Sesso (Sex)
- Fumo (Smoking)
- Tempo di follow-up (Time)

---

## Metodologia

### 1. Preparazione dei Dati

Le attività preliminari hanno incluso:

- Caricamento del dataset tramite Pandas
- Verifica della presenza di valori mancanti
- Conversione delle variabili dicotomiche in variabili categoriche
- Codifica delle variabili categoriali tramite variabili dummy

---

### 2. Analisi Esplorativa dei Dati 

È stata effettuata un'analisi esplorativa per comprendere la distribuzione delle variabili e la loro relazione con l'evento di morte.

In particolare sono stati analizzati:

- Distribuzione della variabile target
- Frequenze delle variabili categoriali
- Distribuzioni delle variabili numeriche
- Boxplot per il confronto tra gruppi
- Correlazioni tra variabili numeriche

---

### 3. Test Statistici

#### Test Chi-Quadrato

Utilizzato per valutare l'associazione tra variabili categoriali e mortalità.

Variabili analizzate:

- Anemia
- Diabete
- Ipertensione
- Sesso
- Fumo

#### Test di Mann-Whitney

Utilizzato per confrontare la distribuzione delle variabili numeriche tra pazienti sopravvissuti e deceduti.

Variabili analizzate:

- Età
- Frazione di eiezione
- Creatinina sierica
- Piastrine
- Sodio sierico
- Creatinine Phosphokinase

---

### 4. Selezione delle Variabili

La variabile **time** è stata esclusa dalla fase di modellazione.

Motivazioni:

- Rappresenta il tempo di follow-up del paziente.
- È fortemente legata all'evento osservato.
- Potrebbe introdurre fenomeni di data leakage.
- Non rappresenta una caratteristica clinica disponibile al momento iniziale della valutazione del paziente.

---

### 5. Suddivisione Train-Test

Il dataset è stato suddiviso in:

- 80% Training Set
- 20% Test Set

La divisione è stata effettuata utilizzando uno **stratified split**, mantenendo invariata la proporzione tra pazienti deceduti e sopravvissuti.

---

## Modelli Utilizzati

### Regressione Logistica

La regressione logistica è stata utilizzata come modello baseline grazie alla sua elevata interpretabilità.

#### Ottimizzazione

È stato ottimizzato il parametro:

- C (regolarizzazione)

mediante Grid Search e Cross-Validation.

---

### Random Forest

La Random Forest è stata utilizzata per catturare eventuali relazioni non lineari tra le variabili cliniche e l'outcome.

#### Ottimizzazione

Sono stati ottimizzati i seguenti parametri:

- Numero di alberi (`n_estimators`)
- Profondità massima (`max_depth`)
- Numero minimo di osservazioni nelle foglie (`min_samples_leaf`)

tramite Grid Search e Cross-Validation.

---

## Validazione e Valutazione

L'ottimizzazione degli iperparametri è stata effettuata tramite:

- Stratified 5-Fold Cross-Validation
- Grid Search

Metrica utilizzata:

- ROC-AUC

La valutazione finale è stata effettuata sul test set, mai utilizzato durante l'addestramento.

---

## Interpretazione dei Modelli

### Regressione Logistica

L'interpretazione è stata effettuata attraverso l'analisi dei coefficienti stimati.

Le variabili con maggiore impatto sono risultate:

- Ejection Fraction
- Serum Creatinine
- Age

---

### Random Forest

L'interpretazione è stata effettuata attraverso l'analisi dell'importanza delle variabili.

Le variabili più rilevanti risultano:

- Serum Creatinine
- Ejection Fraction
- Age
- Creatinine Phosphokinase
- Serum Sodium

---

## Principali Risultati

Entrambi i modelli individuano come fattori maggiormente associati alla mortalità:

- Età elevata
- Ridotta frazione di eiezione
- Elevati livelli di creatinina sierica

Dal punto di vista clinico:

- Una minore capacità di pompaggio del cuore aumenta il rischio di morte.
- Una peggiore funzionalità renale è associata a una prognosi peggiore.
- L'età avanzata rappresenta un importante fattore di rischio.

---

## Performance dei Modelli

### Regressione Logistica

- ROC-AUC ≈ 0,81

Il modello mostra una buona capacità discriminante mantenendo un'elevata interpretabilità.

### Random Forest

- ROC-AUC ≈ 0,99

La Random Forest raggiunge prestazioni estremamente elevate nel test set, evidenziando una capacità quasi perfetta di distinzione tra le classi.

---

## Limiti dello Studio

I risultati devono essere interpretati con cautela.

### Dataset di Dimensioni Ridotte

Il numero relativamente limitato di osservazioni può rendere le performance particolarmente sensibili alla specifica suddivisione train-test.

### Possibile Overfitting

L'elevata performance della Random Forest potrebbe essere dovuta a:

- Forte separabilità delle classi
- Presenza di pattern molto informativi
- Adattamento eccessivo ai dati disponibili

Sarebbe opportuno validare il modello su dataset esterni indipendenti.

### Finalità Didattica

Questo progetto è stato realizzato con finalità formative e di portfolio personale, per rmigliorare le competenze nell'utilizzo di Python

---

## Tecnologie Utilizzate

- Python
- Pandas
- Matplotlib
- Seaborn
- SciPy
- Scikit-Learn

## Possibili Sviluppi Futuri

Alcuni possibili miglioramenti includono:

- Implementazione di XGBoost
- Analisi Precision-Recall
- Interpretazione tramite SHAP Values
- Curve di calibrazione
- Validazione esterna del modello
- Applicazione di tecniche di Survival Analysis

---

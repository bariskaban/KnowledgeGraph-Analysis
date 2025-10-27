# UFC Knowledge Graph Project
**Group 69 – Knowledge and Data (VU Amsterdam)**  
**Authors:** Barış Kaban, Göktuğ Yıldırım, Danila Popuşoi 
**Project Title:** UFC Knowledge Graph and Analysis Pipeline  

---

## 1) Project Overview
This project builds a knowledge graph for the Ultimate Fighting Championship (UFC).  
The ontology models Fighters, Fights, Events, Venues, Divisions, Methods, and Outcomes and aligns them with DBpedia classes (e.g., `dbo:Athlete`, `dbo:SportsEvent`, `dbo:Place`) for interoperability.  
Data are integrated from RDF (DBpedia) and non-RDF (Kaggle CSV) sources, converted into RDF triples, and analyzed/visualized in a Jupyter notebook.

---

## 2) Repository Structure
```
UFC_KnowledgeGraph_Project/
├── ufc-ontology.ttl                 # Ontology (classes, properties, restrictions)
├── ufc-instances.ttl                # Instances (fighters, fights, events, venues…)
├── ufc_analysis.ipynb               # Notebook for querying + visualization
└── README.md                        # This file
```

---

## 3) Requirements
Install Python packages:

~~~bash
pip install rdflib pandas matplotlib seaborn
~~~

Tools:
- **Protégé** (https://protege.stanford.edu/) with **HermiT** reasoner

---

## 4) How to Run

### A. Explore in Protégé
1. Open Protégé.  
2. **File → Open…** and select `ufc-instances.ttl`.  
3. In *Ontology imports*, ensure `ufc-ontology.ttl` is listed (it should auto-import).  
4. Start **Reasoner → HermiT → Start reasoner** to see inferred types (e.g., `ex:ChampionshipFight`), winners, participants, etc.

### B. Run the Jupyter Notebook
1. Open `ufc_analysis.ipynb` (VS Code or Jupyter).  
2. Run all cells to:
   - Load `ufc-ontology.ttl` + `ufc-instances.ttl` via RDFLib  
   - Issue SPARQL queries  
   - Convert results to Pandas DataFrames  
   - Plot analyses (win methods, title-fight ratios, top winners)

**Example SPARQL used in the notebook (illustrative):**
~~~sparql
PREFIX ex:  <http://example.org/ufc#>

SELECT ?fighter ?event
WHERE {
  ?fight a ex:Fight ;
         ex:hasWinner ?fighter ;
         ex:partOfEvent ?event .
}
LIMIT 50
~~~

---

## 5) Data Sources
- **DBpedia Ontology** – https://dbpedia.org/ontology/  
- **FOAF Vocabulary** – https://xmlns.com/foaf/spec/  
- **Kaggle UFC Fights Dataset (2022)** – https://www.kaggle.com/datasets/calmdownkarm/ufc-fights-dataset  

---

## 6) Notes
- Ontology aligns core classes with DBpedia to ease linking and reuse.  
- Reasoning was validated in Protégé (HermiT).  
- The TTL files are self-contained; the notebook reads them directly.

---

## 7) Reproduce Figures (quick guide)
1. Run the notebook end-to-end.  
2. Generated plots include:  
   - Distribution of win methods  
   - Title vs non-title bout ratio per year or event  
   - Top fighters by wins (if present in instances)

---

## 8) Troubleshooting
- If Protégé shows missing imports: **Ontology → Ontology imports → Add → Local file → select `ufc-ontology.ttl`**.  
- If notebook can’t find files, ensure paths point to the same folder as this README.

---

## 9) License
Built for the **Vrije Universiteit Amsterdam – Knowledge and Data** course (Fall 2025).  
For academic/educational use only.

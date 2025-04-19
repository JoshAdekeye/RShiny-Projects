# GraphShiny

Clinical‑trial data pipelines can become labyrinthine. **GraphShiny** simplifies oversight by visualising dataset lineage and flagging discrepancies before they become costly.

<img  width="885" height="655" src="https://github.com/JoshAdekeye/RShiny-Projects/blob/master/img/clinical_graph.gif">

### Key Benefits

- **Interactive lineage map** – explore how raw, SDTM and ADaM datasets connect at a glance  
- **Change notifications** – automatically alert main/QC programmers when an upstream dataset is updated  
- **Necessity check** – verify that every raw dataset present is actually required for the study  
- **Standards compliance** – validate that observed data flow matches specifications and industry or company conventions  
- **Main vs QC comparison** – compare inputs referenced by main and QC programs side‑by‑side  
- **Domain readiness** – confirm that all prerequisite datasets exist for each derived domain  

## How It Works

1. **create_graph_input.R** scans SAS programs with regular expressions, searching for references to the *RAW*, *SDTM* and *ADaM* layers.  
2. The script produces two outputs:  
   * **nodes** – a unique list of all dataset names discovered  
   * **edges** – directional links, e.g. `RAW.DM → SDTM.DM`  
3. Sensitive identifiers are anonymised for this public repo via **masking.py**.  
4. The Shiny app ingests the two tables and renders an interactive network using **visNetwork**.  
5. Inside the app users can:  
   * Filter the graph to focus on specific datasets  
   * Download the complete or filtered edge list as CSV  

## Live Screenshots

### Complete Data‑flow Graph

When the app starts, it shows the full lineage across all datasets:

<img  width="885" height="655" src="https://github.com/JoshAdekeye/RShiny-Projects/blob/master/img/data_flow.png">

### Focused View – *SDTM.MM*

Selecting a node filters the graph to that dataset’s direct relationships. A reactive table lists the same information and can be downloaded.

<img  width="743" height="611" src="https://github.com/JoshAdekeye/RShiny-Projects/blob/master/img/shiny_graph.png">

### End‑to‑End Pipeline into Shiny

<img  width="920" height="760" src="https://github.com/JoshAdekeye/RShiny-Projects/blob/master/img/shiny_graph_mm.png">

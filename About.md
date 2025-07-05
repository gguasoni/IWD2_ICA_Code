## Task
The focus of this assignment was to create and design a website on the UoE server that allowed users to retrieve protein sequences for any chosen branch of the taxonomic tree, run conservation, PROSITE-motif, and other EMBOSS (or equivalent) analyses—complete with downloadable reports and plots — while offering a pre-processed glucose-6-phosphatase *Aves* dataset as a demo. The site was also had to give users the ability to revisit their previously generated data sets.

## Script Details
### Front-End Scripts
- analytis.php
  -  powers the PROTEIGNOSIA home screen: it starts a session, renders a CSS-styled form where users enter a protein family, a taxonomic group, and tick check-boxes for multiple-sequence alignment, PROSITE motif scan, and/or a protein-statistics report. Upon submission it sanitises the inputs, spawns backend_python.py with the chosen options, waits for the pipeline to create a results ZIP, offers an instant “Download Results” button, and prints an HTML table of hits if the PROSITE scan was requested.
- aesthetics2.php
  - the stylesheet that gives PROTEIGNOSIA its Greek-inspired look, styling everything from the blue-and-gold navigation bar and Palatino/Optima typography to zebra-striped tables, hoverable buttons, and subtle geometric borders so the web app feels cohesive and classical.
- statement_of_credit.html
  - the credits page. Provides links to websites consulted in the making of this website and a declaration of AI usage. 

### Back-End Scripts
- backend_python.py
  - is the command-line engine behind PROTEIGNOSIA: it retrieves proteins from NCBI for a specified taxon and family, optionally runs an alignment, a PROSITE motif scan, and basic protein-stat checks, then zips every result file into <taxon>_<family>_results.zip for the web front-end to serve.
- functions.py
  - supplies the heavy-lifting routines for PROTEIGNOSIA: it aligns sequences with Clustal-O or MAFFT and plots similarity, scans FASTA input with EMBOSS patmatmotifs then converts the TSV to CSV, and runs EMBOSS pepstats for basic protein metrics—returning or saving each analysis in project-specific filenames so the main pipeline can zip them for download.
- php_functions.php
  - bundles the small helpers the site relies on: id_maker() assigns visitors a persistent cookie-based user ID, and motifs_table_maker($pdo) sets up the MySQL table that stores PROSITE motif hits for later display and querying.

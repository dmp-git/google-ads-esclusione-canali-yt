# Script esclusione canali YouTube
Escludi i canali youtube che non rispettano il criterio di lingua desiderato

# Come utilizzarlo
1. Duplica questo template: https://docs.google.com/spreadsheets/d/1oxKdx5izqP4BS1QnzEZvBbTDn6oJ_VmrNLDETKvHC9I/edit?gid=0#gid=0
2. Crea un nuovo script su Google Ads, vai sulla sezione "Advanced API" e attiva le opzioni "YouTube" e "YouTube Analytics"
3. Copia/Incolla lo script
4. Associa alla variabile "SPREADSHEET_URL" il link al Google Sheet duplicato al punto 1
5. Avvia lo script. Verrà generato una lista di placement negativi con nome impostato come da variabile "EXCLUSION_LIST_NAME"
6. Associa la lista generata alle campagne target
7. Imposta l'avvio dello script ogni giorno
   

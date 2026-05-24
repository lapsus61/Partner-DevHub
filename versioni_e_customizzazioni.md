---   
title:Versioni e customizzazioni    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Versioni e customizzazioni 
Keywords  [ORG][SETTORE][TRIGGER][TIPO][CUSTOM][PERSONALIZZAZIONI]

Partner ha diversi livelli di verticalizzazioni  
   
## Organizzazione    >o2b_org utilizzata come prefisso della directory F (esempio GF\f\)  
## Verticalizzazione PARTNER  >dis_omeo / dis_omeoD attiva o disattiva alcune funzionalita'/files/programmi    
## Internal Trigger   >Gestisce i diversi utilizzi di uno stesso programma  
## Custom Trigger   >Gestisce le personalizzazioni SPECIFICHE per il cliente  
   
## Organizzazione         -------->stbl o2b_org utilizzata come prefisso della directory F (esempio GF\f\)  
Va utilizzata  
-quando piu' aziende condividono le stesso server ma se ne vuole tenere separate le directory F  
per esempio per limitare le operazioni di backup. In questi casi si potrebbe comunque pensare  
    di condividere alcuni file (tport ad esempio) memorizzandoli in una cartella di livello piu' alta   
-e' obbligatoria quando le aziende sono sul server cloud Oblivion  
   
## Verticalizzazione PARTNER ----->stbl dis_omeo / dis_omeoD attiva o disattiva alcune funzionalita'/files/programmi    
- Y Farmaceutico  
- Y e Recs00(251,1)="Y" Omeopatico  
- P Prodotti/Modelli Pel  
- C Cantina  
- F Prodotti/ModelliD Flex  
- R Recupero Plastiche  
- S Siderurgico  
   
## Internal Trigger           ---->Gestisce i diversi utilizzi di uno stesso programma stbl dis_ome2  
Esempio  
Il programma g-epelav viene utilizzato sia per l'inserimento di ordini Farmaceutici che ordini Siderurgia.  
Per far si che, ad esempio in fase di modifica ordine, sia riconoscibile la versione che lo ha generato,  
la template della testata contiene un campo specifico OR1.PGM_ORG$  
Utilizzare  
blank Nessuna distinizione  
EP    Ordine Siderurgia    
   
## Custom Trigger            ----->Gestisce le personalizzazioni SPECIFICHE per il cliente  
Va utilizzata per implementare specifiche personalizzazioni per specifici clienti  
Utilizza la variabile globale dis_ome2 per distinguere la specifica installazione oppure il codice societa'.  
Per ERP/LGT sarebbe piu' conveniente utilizzare il gruppo, pero' in alcuni casi anche tra le due societa' vi e' differenza. Ad esempio LGT accede ai certificati ferro di EP ma non il contrario   
Ogni installazione ha una specifica sigla UNIVOCA  
Il nome del modulo esterno che viene richiamato e' composto da  
<dis_ome2><nomeprogrammastandard> ad esempio GFIg-rmgana  
Utilizzare  
| Mne | Soc | Assegnato a |  
| GFI   | 22  | GruppoFarmaimpresa |  
| ERP | 03   | EdilProdotti |     
| ERP  | 05   | Lgt |  
| LC    | 25   | Licla |  
| DF   | 11   | DinaFlex |  
| CM  | 01 | Cemon |  
| SV   | 01 | Svas |  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:27 in ambiente Oblivion/ECHO*

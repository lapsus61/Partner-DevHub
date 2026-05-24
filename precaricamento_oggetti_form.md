---   
title:Precaricamento oggetti form    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Precaricamento oggetti form 
Keywords  [FORM][SET][MEM][CHILD][rbglng][lingua][Funzionalita]

A partire dalla build 92, e' presente una nuova funzionalita' attraverso la quale e' possibile memorizzare il contenuto dei campi di una form/child e richiamarlo quando necessario. E' possibile quindi per un utente memorizzare le preferenze di impostazi  
one di un programma, ad esempio di una elaborazione, e rcihiamarle quando necessario cosi da evitare di dover eseguire operazioni ripetitive.  
Ho modificato/creato gb.ini, gb_std.ini, rbgres e rbglng. Quest'ultimo era un progetto di tanti anni fa con il quale intendevo cambiare il testo degli static text se vendevo a clienti inglesi o francesi perche' cemon voleva installare il programma in  
una azienda collegata in Cornovaglia.  
---  
## esempio  
- l'utente entra in Inquiry ordini fornitore  
- setta i campi cosi come li usa di solito (ad esempio io metto sempre deposito 001 e tu sempre deposito 010)  
- clicca sul tasto stampante in alto (si dovra' trovare un'altra icona e sostituirla in rbgres)  
- si apre una form con  
- i dati di ingresso programma/nrpgm/utente  
- un list button dove appaiono tutte le configurazioni che quell utente ha salvato per quel programma/nrpgm  
- un campo descrittivo se vuoi creare una nuova configurazione (selezionando nel list button la voce 00 che appare in fondo)  
- un tasto salva configurazione per salvare una nuova configurazione o per modificare i dati di una vecchia, che genera un file txt nella cartella F con il contenuto di tutti gli oggetti del programma   
- un tasto attiva configurazione per attivare una configurazione salvata che legge il file e setta tutti gli oggetti con il relativo contenuto presente  
in alto a destra la X per uscire  
   
Se salvi una configurazione come 01 ad esempio, poi entri e attivi la configurazione, vedi che il i campi vengono modificati  
Nota  
!!! info    "Informazioni"  
    *Non ho fatto tutti i tasti, ad esempio non ho ancora attivato i custom edit, ma le routine sono intuitive. Ho fatto inputE, inputN, RadioButton, check, list button. Il programma salva il contenuto di TUTTE le child e quando attivi la configurazione modifica il contenuto degli oggetti di TUTTE le child. Per g-rmuvis e' una cosa non utile perche' se entriamo con numero programma 12 vogliamo usare solo quello, ma per g-rmgana invece serve perche' sono tante child ma dello stesso programma. Forse potremmo fare che se c'e' nrpgm salva solo la child da cui provengo e se non c'e' tutto.. pero' non so*  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*

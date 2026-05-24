---   
title:SQL - caratteristiche generali   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# SQL - caratteristiche generali
Keywords  

premessa  
utilizzero' il database nativo come transazionale ed utilizzero un database standard sql che aggiornero in replica e sul quale faro solo query quindi read  
Separo il database dove "scrivi" (le transazioni di Partner su VisualPro5) da quello dove "leggi" (le analisi e le query  
Questa scelta protegge le performance del gestionale (che non viene rallentato da query complesse) e rende il software molto piu' appetibile per gli operatori che vogliono estrarre dati velocemente.  
   
## Tabella 1 - Motore  
Ecco una tabella comparativa dei motori SQL piu' adatti per essere usati come "Read Replica" (copia di sola lettura) nel tuo contesto:  
   
<table><caption><b>SCELTA DEL MOTORE SQL PER REPLICA DATI (READ)</b></caption><thead> <tr> <th>Database SQL</th> <th>Installazione</th> <th>Manutenzione Sistemista</th> <th>Integrazione VPro5</th> <th>Ideale per...</th> </tr> </thead><tbody><tr> <td>  
<b>SQLite</b></td> <td>Massima (e' solo un file)</td> <td>Zero (non serve un server)</td> <td>Facile via JDBC/ODBC</td> <td>Analisi locali e reportistica veloce su PC singolo.</td> </tr><tr> <td><b>MariaDB / MySQL</b></td> <td>Media</td> <td>Bassa (mo  
lto documentato)</td> <td>Ottima via JDBC/ODBC</td> <td>Piccole/Medie imprese. Il piu' leggero tra i server veri.</td> </tr><tr> <td><b>PostgreSQL</b></td> <td>Media</td> <td>Media</td> <td>Ottima via JDBC/ODBC</td> <td>Analisi dati molto complesse e  
grandi volumi di dati.</td> </tr><tr> <td><b>MS SQL Server Express</b></td> <td>Alta (su Windows)</td> <td>Media</td> <td>Ottima via JDBC/ODBC</td> <td>Clienti con infrastruttura Windows Server esistente.</td> </tr></tbody></table>  
## Tabella 2 - Comparazione  
<table> <caption><b>COMPARAZIONE MOTORI SQL PER REPLICA (READ-ONLY)</b></caption> <thead> <tr> <th>Caratteristica</th> <th>SQLite</th> <th>MariaDB</th> <th>PostgreSQL</th> <th>MS SQL Express</th> </tr> </thead> <tbody> <tr> <td><b>Tipo Architettura</  
b></td> <td>File locale (.db)</td> <td>Server (Servizio)</td> <td>Server (Servizio)</td> <td>Server (Servizio)</td> </tr> <tr> <td><b>Complessita' Sistema</b></td> <td>Nessuna (Zero conf)</td> <td>Bassa (Installer)</td> <td>Media (Tuning)</td> <td>Med  
ia (Windows)</td> </tr> <tr> <td><b>Intervento Sistemista</b></td> <td>Non richiesto</td> <td>Installazione una tantum</td> <td>Configurazione iniziale</td> <td>Installazione/Setup</td> </tr> <tr> <td><b>Performance Lettura</b></td> <td>Alta (singolo  
utente)</td> <td>Ottima (multiutente)</td> <td>Eccellente (complessa)</td> <td>Buona</td> </tr> <tr> <td><b>Accesso da Esterno</b></td> <td>Solo tramite file</td> <td>IP e Porta standard</td> <td>IP e Porta standard</td> <td>IP e Porta standard</td>  
</tr> <tr> <td><b>Limiti Versione Free</b></td> <td>Nessuno</td> <td>Nessuno (Open)</td> <td>Nessuno (Open)</td> <td>Limite 10GB / RAM</td> </tr> <tr> <td><b>Appeal Sviluppatori</b></td> <td>Discreto</td> <td>Molto Alto (Web/Standard)</td> <td>Alto  
(Professionale)</td> <td>Buono (Aziendale)</td> </tr> </tbody> </table>  
## Tabella 3 -INNODB  
<table><caption><b>CARATTERISTICHE TECNICHE INNODB (PER REPLICA PARTNER)</b></caption><thead> <tr> <th>Funzionalita'</th> <th>Descrizione per il Programmatore</th> <th>Vantaggio Operativo</th> </tr> </thead><tbody><tr> <td><b>ACID Compliant</b></td> <  
td>Garantisce Transazioni sicure (Atomicita, Coerenza, Isolamento, Durabilita').</td> <td>Se la tua routine di replica si interrompe a meta', il DB non si corrompe. O tutto il blocco dati e' scritto, o nulla.</td> </tr><tr> <td><b>Row-level Locking</b><  
/td> <td>Il blocco avviene sulla singola riga e non sull'intera tabella.</td> <td>Mentre la tua routine VPro5 aggiorna un record, gli operatori possono interrogare tutti gli altri senza attese.</td> </tr><tr> <td><b>Foreign Keys</b></td> <td>Supporto  
nativo ai vincoli di integrita' referenziale (chiavi esterne).</td> <td>Puoi impedire che vengano cancellati record "padre" (es. Clienti) se esistono ancora "figli" (es. Fatture) nella replica.</td> </tr><tr> <td><b>Crash Recovery</b></td> <td>Gestio  
ne automatica del log delle operazioni (Redo Log).</td> <td>In caso di mancanza di corrente al server, InnoDB ripristina lo stato coerente dei dati al riavvio senza intervento del sistemista.</td> </tr><tr> <td><b>Buffer Pool</b></td> <td>Mantiene in  
RAM i dati e gli indici piu' utilizzati.</td> <td>Le query degli operatori su Partner diventano velocissime perche' il DB risponde dalla memoria anziche' dal disco.</td> </tr></tbody></table>  
Perche' InnoDB e' la scelta giusta per te e il tuo collaboratore:  
Per te (Sviluppatore): Quando scrivi la routine di replica, puoi usare SQLCOMMIT e SQLROLLBACK. Questo ti da' una sicurezza che i vecchi file MKEYED non potevano gestire nativamente a livello di singola istruzione.  
Per il Sistemista: InnoDB e' lo standard. Qualsiasi sistemista sa come ottimizzarlo e fare il backup (tramite hot backup, ovvero senza fermare il database).  
Per il futuro di Partner: Utilizzando InnoDB, rendi il database "standard professionale". Se un domani uno sviluppatore giovane dovesse collegare un'interfaccia web, trovera' un ambiente familiare, robusto e performante.  
Un piccolo consiglio: Quando crei le tabelle su MariaDB per la replica, assicurati che la clausola finale della CREATE TABLE sia ENGINE=InnoDB;. Ormai e' il default, ma esplicitarlo e' sempre buona norma.  
## Come implementare questa architettura con il tuo stack:  
Dato che sei un programmatore esperto ma preferisci non toccare i componenti di sistema, ecco come puoi dividere i compiti con il tuo collaboratore:  
Tuo compito (Programmazione):  
Routine di Replica: Dovrai creare una routine in VisualPro5 che, a intervalli (es. ogni notte o ogni ora), legga i file MKEYED e scriva i record sul database SQL scelto.  
Utilizzo dei dati: Utilizzerai i comandi SQL (tramite i canali SQL di BASIS) per popolare dashboard o griglie di ricerca veloci dentro Partner.  
Compito del Sistemista:  
Installazione del motore SQL (se scegli MariaDB o SQL Server).  
Configurazione del Bridge ODBC/JDBC in modo che VisualPro5 possa "parlare" con il database SQL.  
Gestione dei backup del solo database SQL.  
Un consiglio specifico per "Partner"  
Se vuoi rendere il software piu' semplice da implementare per altri sviluppatori, ti suggerisco di scegliere MariaDB.   il "giusto mezzo":  
  gratuito e Open Source.  
  estremamente veloce nelle letture (SELECT).  
Esistono infiniti strumenti gratuiti (come HeidiSQL o DBeaver) che i tuoi collaboratori possono usare per guardare i dati senza "entrare" nel codice VisualPro5.  
Questa separazione ti permettera' di mantenere la stabilita' del codice storico Nixdorf/Basis per la parte contabile/fiscale, offrendo pero' ai clienti una reportistica moderna e veloce che oggi e' fondamentale per vendere un gestionale  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*

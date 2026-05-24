---   
title:Invia e-mail    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Invia e-mail 
Keywords  [E-MAIL][EMAIL][INVIO][MAIL][SEND]

   
   
Premessa: Aruba e SiteGround non accettano che l'indirizzo mittente (from) sia diverso dall'indirizzo di autenticazione. Volendo farlo bisogna abilitare degli indirizzi alias ma poi si deve stare attenti ad altri parametri che non conosco (SMTK,etc)  
altrimenti le email vanno in spam.  
Quindi se vogliamo che un utente mandi con la propria email, e quindi NON CI ACCONTENTIAMO che appaia il 'rispondi a',  siamo costretti a far inserire agli utenti la password di posta in Partner.  
Se invece potrebbe essere sufficiente il 'rispondi a', allora possiamo inviare le email con majordomo, quindi con una unica casella, e passare l'indirizzo email di risposta in -o reply-to=.  
Cosi   
 l'utente mette la sua email nella gestione utenti, non inserisce niente in password ne in smtp  
 g-dmnams utilizza le credenziali di majordomo (prende email password e server smtp) ed aggiunge nella riga  
 di comando -o reply-to= quello che appare nel record dell'utente alla voce indirizzo e-mail  
   
RIGA DI COMANDO  
c:\masbi-sun\sendemail.exe -f t.pirozzi@edilprodottispa.eu -t rdep@rdepartner.it -u "Avviso emissione documento 010266 del 14/04/2025" -s smtp.edilprodottispa.eu:25 -v -m "prova" -xu t.pirozzi@edilprodottispa.eu -xp !TillyLide2020! -cc rdep@rdepartne  
r.it  -o tls=auto -o reply-to=iu8pic@gmail.com -l c:\masbi-sun\log_email202504141131    
   
NOTE  
Manda una mail  
from  t.pirozzi@edilprodottispa.eu  
to  rdep@rdepartner.it  
oggetto  Avviso emissione documento 010266 del 14/04/2025  
Server SMTP smtp.edilprodottispa.eu:25  (aruba)  
testo  prova  
user aut t.pirozzi@edilprodottispa.eu  
user pwd  !TillyLide2020!  
cc  rdep@rdepartner.it  
protocollo TLS auto  
rispondi a iu8pic@gmail.com  
log  c:\masbi-sun\log_email202504141131  
se ci fossero stati allegati ci sarebbe stato anche -a <nomeallegato> -a <nomeallegato>  
HELP COMPLETO di sendemail    
c:\masbi-sun\sendemail --help  
   
   
CALL "sumatc",FILEnm$,0; REM move allegato nella cartella corretta   
NOTE$="In allegato la copia del documento richiesto"         
DIM GB__ARG$:"mail[15]:c(2000*=0)"                                           
GB__ARG.MAIL$[1]="amministrazione@cemon.eu"                                          
GB__ARG.MAIL$[2]=email$                                 
GB__ARG.MAIL$[3]="Copia del documento richiesto "+d2_tmv$+" "+d2_dtrg$+" "+d2_nrrf$                
GB__ARG.MAIL$[4]=NOTE$                                                   
GB__ARG.MAIL$[6]=""                                                      
GB__ARG.MAIL$[8]=FILEnm$; REM   attachment                             
GB__ARG.MAIL$[10]="Y"; REM invio senza conferma                          
GB__ARG.MAIL$[12]="-v"; REM verbose                                      
WAIT 3                                                                      
NOTE$=note$+$0A$+$0A$+"(Questa e-mail e' stata spedita all'indirizzo "+EMAIL$+" il "+DATE(0:"%Dz/%Mz/%Y")+" ore "+DATE(0:"%Hz:%mz:%sz")+" )"       
GB__ARG.MAIL$[4]=NOTE$  
rem            USR$     FROM$             TO$               OBJ$           NOTE$            ATTACH$       EMAIL$     CC$              BCC$  
CALL "suaams",OWNER$,GB__ARG.MAIL$[1],GB__ARG.MAIL$[2],GB__ARG.MAIL$[3],GB__ARG.MAIL$[4],GB__ARG.MAIL$[8],EMAIL$,GB__ARG.MAIL$[6],GB__ARG.MAIL$[7]                                                          
filenm$=path_dst$+filenm$   
##############################################################################################################  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:21 in ambiente Oblivion/ECHO*

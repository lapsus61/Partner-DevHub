---   
title:Lanciare una sessione partner    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Lanciare una sessione partner 
Keywords  [SESSIONE][SESSIONI][RUN][NUOVA][rduSmov][g-rmelav][MV1][MV2][GENERA]

   
Utile quando si vuole lanciare una sessione di Partner che esegua una funzione in modo trasparente. Non e possibile passare parametri se non quelli contenuti nella riga di comando estesa, ma si potrebbe comunque implementare creando un file di inters  
cambio.  
   
- Esempio  
path_exe=C:\BASIS223\VPRO5\vpro5.exe  
path_cfg=\\stampante\usb\d-zip\rps_ds\configds.bbx  
   
<path_exe> -q -m90000 -tT40 -nT0 -c<path_cfg> rduSmov - null usr:000;soc:03;cfg:c:\masbi-sun\smd_20231127024543T40.txt;  
- in questo esempio dal proghramma G-RMELAV viene lanciato il programma rduSmov passando lo usr 000, la societa 03 ed un file che contiene le righe movimento da generare.  
Il modulo da lanciare dovra contenere di certo queste righe di codice cosi da permettere di posizionarsi nella societa giusta, leggere info utili e rendere la sessione invisibile  
   
PRINT 'MINIMIZE'; rem .....................................................................................> minimiza cosi da evitare che appaia lo splash  
CALL "rbgset::SUB_SET_ARGV"; rem ..........................................................> legge parametri  
SOC$=STBL("ps_argsoc"); REM ....................................................................> set Societa  
USR$=STBL("ps_argusr"); REM .....................................................................> set User  
FILENM$=STBL("ps_argcfg"); REM ...............................................................> set File da elaborare  
CALL "susenv",USR$,SOC$; OPEN (104)"tfil"+SOC$; rem ........................> inizializza ambiente  
   
---------------------------------------------------------------------------------------------------------------------  
vedi G-rmelav per la riga di comando da lanciare  
vedi rduSmov per le operazioni da eseguire  
vedi rbgset::SUB_SET_ARGV per l'elenco completo e aggiornato dei parametri che si possono trasferire --------------------------------------------------------------------------------------------------------------------------------------  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:29 in ambiente Oblivion/ECHO*

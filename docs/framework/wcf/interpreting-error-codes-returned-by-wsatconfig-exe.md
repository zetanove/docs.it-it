---
title: "Interpretazione dei codici errore restituiti da wsatConfig.exe | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab65f22b-0d69-4c21-9aaf-74acef0ca102
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Interpretazione dei codici errore restituiti da wsatConfig.exe
Questo argomento elenca tutti i codici errore generati dall'utilità di configurazione WS\-AtomicTransaction \(wsatConfig.exe\) e azioni consigliate da intraprendere.  
  
## Elenco dei codici di errore  
  
|Codice di errore|Descrizione|Azione consigliata da intraprendere|  
|----------------------|-----------------|-----------------------------------------|  
|0|L'operazione è stata completata|Nessuna|  
|1|Errore imprevisto|Contattare Microsoft|  
|2|Si è verificato un errore imprevisto durante il tentativo di contattare MSDTC per recuperare le impostazioni di sicurezza.|Assicurarsi che il servizio MSDTC non sia disabilitato e risolvere tutti i problemi elencati nell'eccezione restituita.|  
|3|L'account utilizzato per l'esecuzione di WsatConfig.exe non dispone delle autorizzazioni necessarie per leggere le impostazioni di sicurezza di rete.|Eseguire WsatConfig.exe con un account utente Amministratore.|  
|4|Abilitare "Accesso di rete DTC" per MSDTC prima di tentare di abilitare il supporto WS\-AT.|Abilitare “Accesso di rete DTC” per MSDTC ed eseguire nuovamente l'utilità.|  
|5|La porta immessa non è compresa nell'intervallo consentito.Il valore deve essere compreso tra 1 e 65535.|Correggere l'opzione della riga di comando `-port:<portNum>`<br /><br /> come indicato nel messaggio di errore.|  
|6|Nella riga di comando è stato specificato un certificato dell'endpoint non valido.Non è stato possibile individuare un certificato o non ha superato la verifica.|Correggere l'opzione della riga di comando `-endpointCert`.Assicurarsi che il certificato abbia una chiave privata, sia destinato a ClientAuthentication e ServerAuthentication, sia installato nell'archivio certificati LocalMachine\\MY e sia completamente attendibile.|  
|7|Nella riga di comando è stato specificato un certificato di account non valido.|Correggere l'opzione della riga di comando `-accountsCerts`.Il certificato specificato non è stato correttamente specificato o non è stato individuato.|  
|8|È stato specificato un timeout predefinito non compreso tra 1 e 3600 secondi.|Immettere un valore di timeout predefinito corretto come indicato.|  
|10|Si è verificato un errore imprevisto nel tentativo di accesso al Registro di sistema.|Verificare messaggio di errore e codice di errore per individuare elementi su cui sia possibile intervenire.|  
|11|Impossibile scrivere nel Registro di sistema.|Assicurarsi che la chiave elencata nel messaggio di errore sia in grado di supportare l'accesso al Registro di sistema da parte dell'account WsatConfig.exe utilizzato per l'esecuzione.|  
|12|Si è verificato un errore imprevisto nel tentativo di accesso all'archivio certificati.|Utilizzare il codice di errore restituito per eseguire il mapping all'errore di sistema appropriato.|  
|13|La configurazione di http.sys non è riuscita.Impossibile creare una nuova prenotazione della porta HTTPS per MSDTC.|Utilizzare il codice di errore restituito per eseguire il mapping all'errore di sistema appropriato.|  
|14|La configurazione di http.sys non è riuscita.Impossibile rimuovere la precedente prenotazione della porta HTTPS per MSDTC.|Utilizzare il codice di errore restituito per eseguire il mapping all'errore di sistema appropriato.|  
|15|La configurazione di http.sys non è riuscita.Esiste già una prenotazione della porta HTTPS precedente per la porta specificata.|Un'altra applicazione è già diventata proprietaria della porta specifica.Cambiare porta o disinstallare o riconfigurare l'applicazione corrente.|  
|16|La configurazione di http.sys non è riuscita.Impossibile associare il certificato specificato alla porta.|Utilizzare il codice errore restituito nel messaggio di errore per eseguire il mapping all'errore di sistema appropriato.|  
|17|La configurazione di http.sys non è riuscita.Impossibile annullare l'associazione del certificato SSL dalla porta precedente.|Utilizzare il codice errore restituito nel messaggio di errore per eseguire il mapping all'errore di sistema adatto.Se necessario, utilizzare httpcfg.exe o netsh.exe per rimuovere le prenotazioni di porta errate.|  
|18|La configurazione di http.sys non è riuscita.Impossibile associare il certificato specificato alla porta in quanto esiste già un'associazione SSL precedente.|Un'altra applicazione è già diventata proprietaria della porta specifica.Cambiare porta o disinstallare o riconfigurare l'applicazione corrente.|  
|19|Il riavvio di MSDTC non è riuscito.|Riavviare manualmente MSDTC, se necessario.Se il problema persiste, contattare Microsoft.|  
|20|[!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] non è installato nel computer remoto o non è installato correttamente.|Installare [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] sul computer.|  
|21|La configurazione remota non è riuscita in quanto si è verificato il timeout dell'operazione.|La chiamata per configurare WS\-AT sul computer remoto richiede più di 90 secondi.|  
|22|[!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] non è installato nel computer remoto o non è installato correttamente.|Installare [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] sul computer.|  
|23|La configurazione remota non è riuscita a causa di un'eccezione sul computer remoto.|Verificare il messaggio di errore per individuare elementi su cui sia possibile intervenire.|  
|26|È stato passato un argomento non valido a WsatConfig.exe.|Verificare eventuali errori nella riga di comando.|  
|27|Opzione della riga di comando `-accounts` non valida.|Correggere l'opzione della riga di comando \-`accounts` per specificare correttamente un account utente.|  
|28|Opzione della riga di comando `-network` non valida.|Correggere l'opzione della riga di comando `-network` per specificare correttamente "abilita" o "disabilita".|  
|29|Opzione della riga di comando `-maxTimeout` non valida.|Correggere l'opzione della riga di comando `-maxTimeout` come indicato.|  
|30|Opzione della riga di comando `-timeout` non valida.|Correggere l'opzione della riga di comando `-timeout`come indicato.|  
|31|Opzione della riga di comando `-traceLevel` non valida.|Correggere l'opzione della riga di comando `-traceLevel` per specificare uno dei seguenti valori validi:<br /><br /> -   Off<br />-   Error<br />-   Critico<br />-   Avviso<br />-   Informazioni<br />-   Verbose<br />-   Tutto|  
|32|Opzione della riga di comando `-traceActivity` non valida.|Correggere l'opzione della riga di comando `-traceActivity` specificando "abilita" o "disabilita".|  
|33|Opzione della riga di comando `-traceProp` non valida.|Correggere l'opzione della riga di comando `-traceProp` specificando "abilita" o "disabilita".|  
|34|Opzione della riga di comando `-tracePII` non valida.|Correggere l'opzione della riga di comando `-tracePII` specificando "abilita" o "disabilita".|  
|37|WsatConfig.exe non è stato in grado di determinare il certificato del computer esatto.Questo potrebbe verificarsi quando esiste più di un candidato o quando non ne esiste nessuno.|Specificare un'identificazione digitale o una coppia Issuer\\SubjectName per identificare correttamente il certificato esatto da configurare.|  
|38|Il processo o l'utente non dispone delle autorizzazioni sufficienti per modificare la configurazione del firewall.|Eseguire WsatConfig.exe con un account utente Amministratore.|  
|39|Si è verificato un errore di WsatConfig.exe durante l'aggiornamento della configurazione del firewall.|Verificare il messaggio di errore per individuare elementi su cui sia possibile intervenire.|  
|40|WsatConfig.exe non è in grado concedere a MSDTC l'accesso in lettura al file di chiave privata del certificato.|Eseguire WsatConfig.exe con un account utente Amministratore.|  
|41|Non è stata individuata alcuna installazione di [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] o la versione trovata non corrisponde alla funzionalità di configurazione dello strumento.|Assicurarsi che [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] sia installato correttamente e utilizzare soltanto lo strumento WsatConfig.exe fornito con tale versione di [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] per configurare WS\-AT.|  
|42|Uno stesso argomento è stato specificato più volte nella riga di comando.|Specificare ogni argomento una sola volta quando si esegue WsatConfig.exe.|  
|43|WsatConfig.exe non è in grado di aggiornare le impostazioni di WS\-AT se WS\-AT non è abilitato.|Specificare `-network:enable` come argomento della riga di comando aggiuntivo.|  
|44|Un hotfix necessario risulta mancante ed è impossibile configurare WS\-AT finché non viene installato tale hotfix.|Vedere le note sulla versione di [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] per istruzioni sull'installazione dell'hotfix necessario.|  
|45|Opzione della riga di comando `-virtualServer` non valida.|Correggere l'opzione della riga di comando `-virtualServer` specificando il nome di rete della risorsa cluster in cui eseguire la configurazione.|  
|46|Si è verificato un errore imprevisto nel tentativo di avvio della sessione di traccia ETW|Utilizzare il codice di errore restituito per eseguire il mapping all'errore di sistema appropriato.|  
|47|Il processo o l'utente non dispone delle autorizzazioni necessarie per abilitare la sessione di traccia ETW.|Eseguire WsatConfig.exe con un account utente Amministratore.|  
|48|Si è verificato un errore imprevisto nel tentativo di avvio della sessione di traccia ETW.|Contattare Microsoft.|  
|49|Impossibile creare un nuovo file di log per mancanza di spazio su %systemdrive%|Assicurarsi che %systemdrive% disponga di spazio sufficiente per il file di log.|  
|51|Si è verificato un errore imprevisto nel tentativo di avvio della sessione di traccia ETW.|Contattare Microsoft.|  
|52|Si è verificato un errore imprevisto nel tentativo di avvio della sessione di traccia ETW.|Contattare Microsoft.|  
|53|Il backup del file di log della sessione ETW precedente non è riuscito.|Assicurarsi che %systemdrive% disponga di spazio sufficiente per il file di log e per il backup del file di log precedente \(se presente\).Rimuovere manualmente il file di log precedente, se necessario.|  
|55|Si è verificato un errore imprevisto nel tentativo di avvio della sessione di traccia ETW.|Contattare Microsoft.|  
|56|Si è verificato un errore imprevisto nel tentativo di avvio della sessione di traccia ETW.|Contattare Microsoft.|  
  
## Vedere anche  
 [Utilità di configurazione WS\-AtomicTransaction \(wsatConfig.exe\)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
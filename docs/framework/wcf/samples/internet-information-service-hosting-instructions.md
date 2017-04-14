---
title: "Istruzioni per l&#39;hosting su IIS (Internet Information Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 959a21c8-9d9d-4757-b255-4e57793ae9d6
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Istruzioni per l&#39;hosting su IIS (Internet Information Services)
Per eseguire gli esempi ospitati su Internet Information Services \(IIS\) è necessario assicurarsi che IIS sia installato correttamente e sia in esecuzione.  
  
### Installazione di IIS versione 7.5 in Windows Server 2008 R2  
  
1.  In **Server Manager** selezionare **Ruoli**. In **Riepilogo ruoli** fare clic su **Aggiungi ruoli**.  
  
2.  Fare clic su **Avanti** per visualizzare la finestra di dialogo **Selezione ruoli server**.  
  
3.  Selezionare **Server applicazioni** nell'elenco **Ruoli**, quindi fare clic su **Avanti** due volte per visualizzare la finestra di dialogo **Selezione servizi ruolo** per il ruolo Server applicazioni.  
  
4.  Selezionare la casella di controllo **Server Web \(IIS\)**.  Se viene richiesto di installare servizi e funzionalità di ruolo aggiuntivi, fare clic su **Aggiungi funzionalità necessarie**.  Fare clic su **Avanti** due volte per visualizzare la finestra di dialogo **Selezione servizi ruolo** per il ruolo Server Web \(IIS\).  
  
5.  Espandere **Strumenti di gestione**, quindi espandere **Compatibilità gestione IIS 6**.  Selezionare **Strumenti di scripting di IIS 6**.  Se viene richiesto di installare servizi e funzionalità di ruolo aggiuntivi, fare clic su **Aggiungi servizi ruolo necessari**.  Scegliere **Avanti**.  
  
6.  Se il riepilogo delle selezioni è corretto, fare clic su **Installa**.  
  
7.  Al termine dell'installazione, fare clic su **Chiudi**.  
  
### Per installare IIS versione 7.5 in Windows 7  
  
1.  Fare clic sul pulsante **Start** e scegliere **Pannello di controllo**.  
  
2.  Aprire il gruppo **Programmi**.  
  
3.  In **Programmi e funzionalità** fare clic su **Attivazione o disattivazione delle funzionalità Windows**.  
  
4.  Verrà visualizzata la finestra di dialogo **Controllo account utente**.  Scegliere **Continua**.  
  
5.  Verrà visualizzata la finestra di dialogo **Funzionalità Windows**.  Espandere l'elemento **Internet Information Services**.  
  
6.  Espandere l'elemento **Servizi World Wide Web**.  
  
7.  Espandere l'elemento **Funzionalità per lo sviluppo di applicazioni**.  
  
8.  Verificare che gli elementi seguenti siano selezionati:  
  
    1.  **Estensibilità .NET**  
  
    2.  **ASP.NET**  
  
    3.  **Estensioni ISAPI**  
  
    4.  **Filtri ISAPI**  
  
9. Nell'elemento **Servizi Web** espandere **Funzionalità HTTP comuni**.  
  
10. Verificare che **Contenuto statico** sia selezionato.  
  
11. Nell'elemento **Servizi World Wide Web** espandere **Sicurezza**  
  
12. Verificare che sia selezionata l'opzione **Autenticazione di Windows**.  
  
13. Nella directory **Internet Information Services** espandere l'elemento **Strumenti di gestione Web**, quindi selezionare **Console di gestione IIS**.  
  
14. Espandere l'elemento **Compatibilità di gestione con IIS 6**, quindi selezionare **Strumenti di script di IIS 6**.  
  
15. Nella directory **Internet Information Services** espandere l'elemento **Microsoft .NET Framework 3.5.1**, quindi selezionare **Attivazione HTTP Windows Communication Foundation**.  
  
16. Fare clic su **OK**.  
  
### Installazione di IIS versione 7.0 in Windows Server 2008  
  
1.  In **Server Manager** selezionare **Ruoli**.  In **Riepilogo ruoli** fare clic su **Aggiungi ruoli**.  
  
2.  Fare clic su **Avanti** per visualizzare la finestra di dialogo **Selezione ruoli server**.  
  
3.  Selezionare **Server applicazioni** nell'elenco **Ruoli**, quindi fare clic su **Avanti** due volte per visualizzare la finestra di dialogo **Selezione servizi ruolo** per il ruolo Server applicazioni.  
  
4.  Selezionare la casella di controllo **Server Web \(IIS\)**.  Se viene richiesto di installare servizi e funzionalità di ruolo aggiuntivi, fare clic su **Aggiungi funzionalità necessarie**.  Fare clic su **Avanti** due volte per visualizzare la finestra di dialogo **Selezione servizi ruolo** per il ruolo Server Web \(IIS\).  
  
5.  Espandere **Strumenti di gestione**, quindi espandere **Compatibilità gestione IIS 6**.  Selezionare **Strumenti di scripting di IIS 6**.  Se viene richiesto di installare servizi e funzionalità di ruolo aggiuntivi, fare clic su **Aggiungi servizi ruolo necessari**.  Scegliere **Avanti**.  
  
6.  Se il riepilogo delle selezioni è corretto, fare clic su **Installa**.  
  
7.  Al termine dell'installazione, fare clic su **Chiudi**.  
  
### Per installare IIS sulla versione 7.0 in Windows Vista  
  
1.  Fare clic sul pulsante Start, quindi scegliere Pannello di controllo.  
  
2.  Selezionare il gruppo **Programmi**.  
  
3.  In **Programmi e funzionalità** fare clic su **Attivazione o disattivazione delle funzionalità Windows**.  
  
4.  Verrà visualizzata la finestra di dialogo **Controllo account utente**.  Scegliere **Continua**.  
  
5.  Verrà visualizzata la finestra di dialogo **Funzionalità Windows**.  Espandere l'elemento **Internet Information Services**.  
  
6.  Espandere l'elemento **Servizi World Wide Web**.  
  
7.  Espandere l'elemento **Funzionalità per lo sviluppo di applicazioni**.  
  
8.  Verificare che gli elementi seguenti siano selezionati:  
  
    1.  **Estensibilità .NET**  
  
    2.  **ASP.NET**  
  
    3.  **Estensioni ISAPI**  
  
    4.  **Filtri ISAPI**  
  
9. Espandere l'elemento **Strumenti di gestione Web**, quindi selezionare **Console di gestione IIS**.  
  
10. Nell'elemento **Servizi Web** espandere **Funzionalità HTTP comuni**.  
  
11. Verificare che **Contenuto statico** sia selezionato.  
  
12. Nell'elemento **Servizi World Wide Web** espandere **Sicurezza**  
  
13. Verificare che l'opzione **Autenticazione di Windows** sia selezionata.  
  
14. Espandere l'elemento **Compatibilità di gestione con IIS 6**, quindi selezionare **Strumenti di script di IIS 6**.  
  
15. Espandere l'elemento **Microsoft .NET Framework 3.0**, quindi selezionare **Attivazione di Windows Communication Foundation HTTP**.  
  
16. Fare clic su **OK**.  
  
### Per installare IIS versione 6.0 in Windows Server 2003  
  
1.  In **Amministrazione server** fare clic su **Aggiungi o rimuovi un ruolo**, quindi fare clic su **Avanti**.  
  
2.  Nella pagina **Server applicazioni \(IIS, ASP.NET\)** selezionare l'elenco **Ruolo server**, quindi fare clic su **Avanti**.  
  
3.  Selezionare la casella di controllo **Abilita ASP.NET** e quindi fare clic su **Avanti**.  
  
4.  Se il riepilogo delle selezioni è corretto, fare clic su Avanti.  
  
### Per installare IIS versione 5.1 in Windows XP con Service Pack 2 e Service Pack 3 installati  
  
1.  In Pannello di controllo aprire **Installazione applicazioni**.  
  
2.  Nella finestra di dialogo **Installazione applicazioni** scegliere **Installazione componenti di Windows**.  
  
3.  In **Aggiunta guidata componenti di Windows** selezionare la casella di controllo **Internet Information Services \(IIS\)**, quindi fare clic su **Avanti**.  
  
4.  Se la finestra di dialogo **Richiesta file** viene visualizzata, inserire il disco di installazione del sistema operativo, selezionare la cartella i386, quindi fare clic su **OK**.  
  
5.  Al termine dell’installazione fare clic su **Fine**.  
  
6.  Chiudere la finestra di dialogo **Installazione applicazioni**, quindi chiudere **Pannello di controllo**.  
  
### Per verificare l'installazione di IIS e ASP.NET  
  
1.  Salvare il file HTML trovato alla fine di questo argomento nella directory radice \\InetPub\\wwwroot e rinominarlo Default.aspx.  
  
2.  Aprire una finestra di browser.  
  
3.  Digitare `http://localhost/Default.aspx` nella casella degli indirizzi, quindi premere INVIO.  
  
4.  Dovrebbe venire visualizzata una pagina Web contenente il testo "Hello World".  
  
> [!NOTE]
>  Ogni volta che si installa una nuova versione di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], è necessario registrare di nuovo aspnet\_isapi come estensione del servizio Web per IIS.  A tale scopo, eseguire il comando `aspnet_regiis –I –enable`.  
  
## Codice di esempio  
  
```  
<html>  
   <body>  
       <form >  
           <h3> Hello World  
           </h3>  
       </form>  
   </body>  
</html>  
```
---
title: "Procedura: abilitare il rilevamento della riproduzione di token | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5a9f5771-f5f6-4100-8501-406aa20d731a
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# Procedura: abilitare il rilevamento della riproduzione di token
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 In questa procedura vengono fornite le procedure dettagliate per abilitare il rilevamento riproduzione di token in un'applicazione ASP.NET che utilizza WIF.  Fornisce inoltre le istruzioni su come verificare l'applicazione per verificare che il rilevamento di riproduzione sia attivato.  In questa procedura non ha dettagliato le istruzioni per creare un servizio token di sicurezza \(STS\) e ne utilizza lo sviluppo servizio token di sicurezza fornite dallo strumento di Accesso e di identità.  Lo sviluppo servizio token di sicurezza non esegue l'autenticazione reale ed è destinata a scopo di test solo.  È necessario configurare l'identità e lo strumento di accesso per tale tipo.  Può essere scaricato dal seguente percorso: [Identità e strumento Access](http://go.microsoft.com/fwlink/?LinkID=245849)  
  
## Contenuto  
  
-   Obiettivi  
  
-   Panoramica  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice e abilitare il rilevamento riproduzione  
  
-   Passaggio 2 \- eseguire il test della soluzione  
  
## Obiettivi  
  
-   Creare una semplice applicazione ASP.NET che utilizza WIF e lo sviluppo servizio token di sicurezza dall'identità e accedere allo strumento  
  
-   Abilitare il rilevamento riproduzione di token e verificare che sia funzionante  
  
## Panoramica  
 Un attacco di tipo replay si verifica quando un client tenta di autenticare un componente con un token di servizio token di sicurezza che il client ha già utilizzato.  Per impedire questo attacco, WIF contiene una cache di rilevamento riproduzione dei token utilizzati in precedenza di servizio token di sicurezza.  Una volta abilitata, il rilevamento riproduzione controlla il token della richiesta in arrivo e verifica se il token in precedenza è stato utilizzato.  Se il token è stato già utilizzato, la richiesta viene rifiutato e un'eccezione <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> viene generata un'eccezione.  
  
 I passaggi seguenti illustrano le modifiche di configurazione necessarie per abilitare il rilevamento riproduzione.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice e abilitare il rilevamento riproduzione  
  
-   Passaggio 2 \- eseguire il test della soluzione  
  
## Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice e abilitare il rilevamento riproduzione  
 In questo passaggio, verrà creata una nuova applicazione Web Form ASP.NET e si modifica *il file Web.config* per abilitare il rilevamento riproduzione.  
  
#### Per creare una semplice applicazione ASP.NET  
  
1.  Avviare Visual Studio e clic **File**, **Nuova**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto **TestApp** in **Esplora soluzioni**, quindi selezionare **Identità e accesso**.  
  
5.  La finestra **Identità e accesso** visualizzato.  In **Provider**, **Verifica applicazione con STS di sviluppo locale**selezionato, quindi scegliere **Applica**.  
  
6.  Aggiungere il seguente elemento **\<tokenReplayDetection\>** *al file di configurazione Web.config* subito dopo gli elementi **\<identityConfiguration\>** e **\<system.identityModel\>**, come indicato:  
  
    ```  
    <system.identityModel>  
        <identityConfiguration>  
            <tokenReplayDetection enabled=”true”/>  
    ```  
  
## Passaggio 2 \- eseguire il test della soluzione  
 In questo passaggio, è consigliabile testare l'applicazione WIF\- abilitata ASP.NET verificare che il rilevamento riproduzione sia stato abilitato.  
  
#### Per testare l'applicazione WIF\- abilitata ASP.NET di rilevamento riproduzione  
  
1.  Eseguire la soluzione premendo il tasto **F5**.  Dovrebbe essere visualizzata la home page ASP.NET predefinito e automaticamente essere autenticati con il nome utente *Terry*, che corrisponde all'utente predefinito restituito dallo sviluppo servizio token di sicurezza.  
  
2.  Premere il pulsante **Indietro** del browser.  Dovrebbe essere visualizzata una pagina **Errore del server nell'applicazione "\/"** con la descrizione seguente: *ID1062: Il tipo replay è stato rilevato per: token: "System.IdentityModel.Tokens.SamlSecurityToken"*, seguito da un *AssertionId* e da un autorità *Issuer*.  
  
     Si sta visualizzando la pagina di errore perché un'eccezione di tipo <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> è stata generata quando il tipo replay di token è stato rilevato.  Questo errore si verifica perché si sta tentando di inviare la richiesta del primo utilizzo quando il token è stato verificato.  Il pulsante **Indietro** non genererà questo comportamento le richieste successive al server.
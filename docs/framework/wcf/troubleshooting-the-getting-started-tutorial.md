---
title: "Risoluzione dei problemi relativi all&#39;esercitazione introduttiva | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 69a21511-0871-4c41-9a53-93110e84d7fd
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Risoluzione dei problemi relativi all&#39;esercitazione introduttiva
In questo argomento vengono elencati i problemi più comuni che possono verificarsi durante l'Esercitazione introduttiva e le relative soluzioni.  
  
1.  [Impossibile trovare i file di progetto nell'unità disco rigido.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q1)  
  
2.  [Se si tenta di eseguire l'applicazione del servizio, viene visualizzato l'errore seguente: HTTP non è stato in grado di registrare l'URL http://+:8000/ServiceModelSamples/Service/.Il processo non dispone dei diritti di accesso a questo spazio dei nomi.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q2)  
  
3.  [Se si tenta di utilizzare lo strumento Svcutil.exe, viene visualizzato l'errore seguente: 'svcutil' non è riconosciuto come comando interno o esterno, un programma eseguibile o un file batch.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q3)  
  
4.  [Impossibile trovare il file App.config generato da Svcutil.exe.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q4)  
  
5.  [Durante la compilazione dell'applicazione client, viene visualizzato l'errore seguente: 'CalculatorClient' non contiene una definizione per '&lt;nome metodo&gt;' e non è stato trovato alcun metodo di estensione '&lt;nome metodo&gt;' che accetta un primo argomento di tipo 'CalculatorClient'. Probabilmente manca una direttiva using o un riferimento a un assembly.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q5).  
  
6.  [Durante la compilazione dell'applicazione client, viene visualizzato l'errore seguente: Impossibile trovare il tipo o il nome dello spazio dei nomi 'CalculatorClient'; probabilmente manca una direttiva using o un riferimento a un assembly.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q6)  
  
7.  [Eseguendo il client, viene visualizzato l'errore seguente: Eccezione non gestita: System.ServiceModel.EndpointNotFoundException: Impossibile connettersi a http://localhost:8000/ServiceModelSamples/Service/CalculatorService.Codice di errore TCP 10061: Impossibile stabilire la connessione. Rifiuto persistente del computer di destinazione.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q7)  
  
<a name="BKMK_q1"></a>   
## Impossibile trovare i file di progetto nell'unità disco rigido.  
 In [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] i file di progetto vengono salvati in c:\\users\\\<nome utente\\Documenti\\\<Versione di Visual Studio\>\\Projects in [!INCLUDE[wv](../../../includes/wv-md.md)] e in [!INCLUDE[win7_client_secondref](../../../includes/win7-client-secondref-md.md)], e in c:\\Documents and Settings\\\<nome utente\>\\Documenti\\\<Versione di Visual Studio\>\\Projects nelle versioni precedenti di Windows.  
  
<a name="BKMK_q2"></a>   
## Se si tenta di eseguire l'applicazione del servizio, viene visualizzato l'errore seguente: HTTP non è stato in grado di registrare l'URL http:\/\/\+:8000\/ServiceModelSamples\/Service\/.Il processo non dispone dei diritti di accesso a questo spazio dei nomi.  
 Il processo che ospita un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] deve essere eseguito con privilegi di amministratore.Se il servizio viene eseguito da [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], è necessario eseguire [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] come amministratore.A tale scopo, fare clic su **Start**, fare clic con il pulsante destro del mouse su [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] e selezionare **Esegui come amministratore**.Se il servizio viene eseguito da un prompt della riga di comando, è necessario avviare il prompt della riga di comando come amministratore.Fare clic sul pulsante **Start**, fare clic con il pulsante destro del mouse su **Prompt dei comandi**, quindi scegliere **Esegui come amministratore**.  
  
<a name="BKMK_q3"></a>   
## Se si tenta di utilizzare lo strumento Svcutil.exe, viene visualizzato l'errore seguente: 'svcutil' non è riconosciuto come comando interno o esterno, un programma eseguibile o un file batch.  
 Svcutil.exe deve trovarsi nel percorso di sistema.La soluzione più semplice consiste nell'utilizzare il prompt dei comandi.Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, quindi [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], **Visual Studio Tools** e [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]**Prompt dei comandi**.Questo prompt dei comandi consente di impostare il percorso di sistema sui percorsi corretti per tutti gli strumenti forniti con [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)].  
  
<a name="BKMK_q4"></a>   
## Impossibile trovare il file App.config generato da Svcutil.exe.  
 Per impostazione predefinita, nella finestra di dialogo **Aggiungi elemento esistente** vengono visualizzati solo i file con le estensioni cs, resx, settings, xsd e wsdl.È possibile impostare la visualizzazione di tutti i tipi di file selezionando **Tutti i file \(\*.\*\)** nella casella di riepilogo a discesa nell'angolo inferiore destro della finestra di dialogo **Aggiungi elementi esistente**.  
  
<a name="BKMK_q5"></a>   
## Durante la compilazione dell'applicazione client, viene visualizzato l'errore seguente: 'CalculatorClient' non contiene una definizione per '\<nome metodo\>' e non è stato trovato alcun metodo di estensione '\<nome metodo\>' che accetta un primo argomento di tipo 'CalculatorClient'. Probabilmente manca una direttiva using o un riferimento a un assembly.  
 Solo i metodi contrassegnati con `ServiceOperationAttribute` vengono esposti al mondo esterno.Se è stato omesso l'attributo `ServiceOperationAttribute` da uno dei metodi nell'interfaccia `ICalculator`, durante la compilazione di un'applicazione client che effettua una chiamata all'operazione a cui manca l'attributo viene visualizzato questo messaggio di errore.  
  
<a name="BKMK_q6"></a>   
## Durante la compilazione dell'applicazione client, viene visualizzato l'errore seguente: Impossibile trovare il tipo o il nome dello spazio dei nomi 'CalculatorClient'; probabilmente manca una direttiva using o un riferimento a un assembly.  
 Questo errore si verifica se il file Proxy.cs o Proxy.vb non viene aggiunto al progetto client.  
  
<a name="BKMK_q7"></a>   
## Eseguendo il client, viene visualizzato l'errore seguente: Eccezione non gestita: System.ServiceModel.EndpointNotFoundException: Impossibile connettersi a http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService.Codice di errore TCP 10061: Impossibile stabilire la connessione. Rifiuto persistente del computer di destinazione.  
 Si verifica questo errore se l'applicazione client viene eseguita senza eseguire il servizio.  
  
<a name="BKMK_q8"></a>   
## Eccezione non gestita: System.ServiceModel.Security.SecurityNegotiationException: Negoziazione di sicurezza SOAP con 'http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService' per la destinazione 'http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService' non riuscita  
 Questo errore si verifica in un computer aggiunto a un dominio senza connettività di rete.Connettere il computer alla rete o disattivare la sicurezza sia per il client che per il servizio.Per quest'ultimo, modificare inoltre il codice che crea WSHttpBinding nel modo seguente.  
  
```  
// Step 3 of the hosting procedure: Add a service endpoint  
selfhost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(SecurityMode.None), "CalculatorService");  
  
```  
  
 Per il client, modificare l'elemento **\<security\>** sotto l'elemento **\<binding\>** nel modo seguente:  
  
```  
<security mode="Node" />  
```  
  
## Vedere anche  
 [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md)   
 [Guida rapida alla risoluzione dei problemi di WCF](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md)   
 [Risoluzione dei problemi di installazione](../../../docs/framework/wcf/troubleshooting-setup-issues.md)
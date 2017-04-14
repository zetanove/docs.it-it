---
title: "Convalida client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0c1f805-1a81-4d0d-a112-bf5e2e87a631
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Convalida client
I servizi pubblicano spesso metadati per consentire la generazione e configurazione automatica di tipi di proxy client.  Quando il servizio non è considerato attendibile, le applicazioni client devono convalidare che i metadati siano conformi ai criteri dell'applicazione client riguardanti la sicurezza, le transazioni, il tipo di contratto di servizio e così via.  Nell'esempio seguente viene dimostrato come scrivere un comportamento dell'endpoint client che convalida l'endpoint del servizio per garantire che quest'ultimo possa essere usato senza rischi.  
  
 Il servizio espone quattro endpoint del servizio.  Il primo endpoint usa WSDualHttpBinding, il secondo usa l'autenticazione NTLM, il terzo abilita il flusso delle transazioni e il quarto usa l'autenticazione basata sui certificati.  
  
 Il client usa la classe <xref:System.ServiceModel.Description.MetadataResolver> per recuperare i metadati per il servizio.  Il client applica i criteri di proibizione delle associazioni duplex, autenticazione NTLM e flusso delle transazioni usando un comportamento di convalida.  Per ogni istanza <xref:System.ServiceModel.Description.ServiceEndpoint> importata dai metadati del servizio, l'applicazione client aggiunge un'istanza del comportamento dell'endpoint `InternetClientValidatorBehavior` a <xref:System.ServiceModel.Description.ServiceEndpoint> prima di tentare di usare un client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per connettersi all'endpoint.  Il metodo `Validate` del comportamento viene eseguito prima che venga chiamata qualsiasi operazione nel servizio e applica i criteri del client generando `InvalidOperationExceptions`.  
  
### Per compilare l'esempio  
  
1.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
### Per eseguire l'esempio nello stesso computer  
  
1.  Aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.  In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
2.  Eseguire l'applicazione di servizio da \\service\\bin\\Debug.  
  
3.  Eseguire l'applicazione client da \\client\\bin\\Debug.  L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
4.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
5.  Rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio.  Negli altri esempi relativi alla sicurezza vengono usati gli stessi certificati.  
  
### Per eseguire l'esempio tra più computer  
  
1.  Sul server aprire un prompt dei comandi di Visual Studio con privilegi di amministratore, quindi digitare `setup.bat service`.  Quando si esegue `setup.bat` `` con l'argomento `service` viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service.cer.  
  
2.  Modificare App.config sul server per riflettere il nome del nuovo certificato,  ovvero modificare l'attributo `findValue` nell'elemento [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) con il nome di dominio completo del computer.  
  
3.  Copiare il file Service.cer dalla directory del servizio nella directory del client sul computer relativo.  
  
4.  Sul client aprire un prompt dei comandi di Visual Studio con privilegi di amministratore, quindi digitare `setup.bat client`.  Quando si esegue `setup.bat` `` con l'argomento `client` viene creato un certificato client denominato client.com che viene esportato in un file denominato Client.cer.  
  
5.  Nel file client.cs modificare il valore dell'indirizzo dell'endpoint MEX e il `findValue` per impostare il certificato del server predefinito in modo che corrisponda al nuovo indirizzo del servizio.  Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server.  Ricompilare il file.  
  
6.  Copiare il file Client.cer dalla directory del client nella directory del servizio sul server.  
  
7.  Sul client aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire ImportServiceCert.bat.  In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
8.  Sul server aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire ImportClientCert.bat.  In questo modo viene importato il certificato del client dal file Client.cer nell'archivio LocalMachine \- TrustedPeople.  
  
9. Nel computer del servizio compilare il progetto di servizio in Visual Studio ed eseguire service.exe.  
  
10. Nel computer client eseguire client.exe.  
  
    1.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
    > [!NOTE]
    >  Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.  Se sono stati eseguiti esempi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che usano certificati tra più computer, verificare di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.  A questo scopo, usare il comando seguente: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Nome completo del computer server>. Ad esempio: certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
## Vedere anche  
 [Utilizzo di metadati](../../../../docs/framework/wcf/feature-details/using-metadata.md)
---
title: "Procedura: creare un&#39;associazione di sessione affidabile personalizzata con HTTPS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa772232-da1f-4c66-8c94-e36c0584b549
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: creare un&#39;associazione di sessione affidabile personalizzata con HTTPS
In questo argomento viene illustrato l'uso della protezione del trasporto SSL \(Secure Sockets Layer\) con sessioni affidabili.  Per usare una sessione affidabile su HTTPS è necessario creare un'associazione personalizzata che usa una sessione affidabile e il trasporto HTTPS.  È possibile attivare la sessione affidabile in modo imperativo, mediante codice, o in modo dichiarativo, nel file di configurazione.  In questa procedura vengono usati i file di configurazione del client e del servizio per attivare la sessione affidabile e l'elemento [\<trasportoHttps\>](../../../../docs/framework/configure-apps/file-schema/wcf/httpstransport.md).  
  
 La parte principale della procedura è rappresentata dall'elemento di configurazione `endpoint` che contiene un attributo `bindingConfiguration` che fa riferimento a una configurazione di associazione personalizzata denominata "reliableSessionOverHttps".  L'elemento di configurazione [\<associazione\>](../../../../docs/framework/misc/binding.md)`reliableSession può quindi fare riferimento a questo nome, per specificare che vengono usati una sessione affidabile e il trasporto HTTPS, includendo gli elementi` `httpsTransport e` .  
  
 Per l'originale di questo esempio, vedere [Sessione affidabile di associazione personalizzata su HTTPS](../../../../docs/framework/wcf/samples/custom-binding-reliable-session-over-https.md).  
  
### Per configurare il servizio con una CustomBinding per usare una sessione affidabile con HTTPS  
  
1.  Definire un contratto di servizio per il tipo di servizio.  
  
     [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1121)]  
  
2.  Implementare il contratto di servizio in una classe del servizio.  Si noti che le informazioni sull'indirizzo o sull'associazione non sono specificate nell'implementazione del servizio.  Non è necessario, inoltre, scrivere codice per recuperarle dal file di configurazione.  
  
     [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1122)]  
  
3.  Creare un file Web.config per configurare un endpoint per `CalculatorService` con un'associazione personalizzata denominata "reliableSessionOverHttps" che usa una sessione affidabile e il trasporto HTTPS.  
  
     [!code[c_HowTo_CreateReliableSessionHTTPS#2111](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/web.config#2111)]  
  
4.  Creare un file Service.svc che contenga la riga:  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
5.  Posizionare il file Service.svc nella directory virtuale di Internet Information Services \(IIS\).  
  
### Per configurare il client con una CustomBinding per usare una sessione affidabile con HTTPS  
  
1.  Usare lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) dalla riga di comando per generare codice dai metadati del servizio.  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  Il client generato contiene l'interfaccia `ICalculator` che definisce il contratto di servizio che l'implementazione del client deve soddisfare.  
  
     [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1221)]  
  
3.  L'applicazione client generata contiene inoltre l'implementazione di `ClientCalculator`.  Si noti che le informazioni sull'indirizzo e sull'associazione non sono specificate nell'implementazione del servizio.  Non è necessario, inoltre, scrivere codice per recuperarle dal file di configurazione.  
  
     [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1222)]  
  
4.  Configurare un'associazione personalizzata denominata "reliableSessionOverHttps" per usare il trasporto HTTPS e sessioni affidabili.  
  
     [!code[C_HowTo_CreateReliableSessionHTTPS#2211](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/app.config#2211)]  
  
5.  Creare un'istanza di `ClientCalculator` in un'applicazione, quindi chiamare le operazioni del servizio.  
  
     [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1223)]  
  
6.  Compilare ed eseguire il client.  
  
## Esempio  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## Sicurezza di .NET Framework  
 Poiché il certificato usato in questo esempio è un certificato di prova creato con Makecert.exe, viene visualizzato un avviso di sicurezza quando si tenta di accedere a un indirizzo HTTPS quale https:\/\/localhost\/servicemodelsamples\/service.svc dal browser.  
  
## Vedere anche  
 [Sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)
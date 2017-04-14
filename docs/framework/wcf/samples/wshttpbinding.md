---
title: "WSHttpBinding | Microsoft Docs"
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
helpviewer_keywords: 
  - "Associazione profilo WS"
ms.assetid: 22d85b19-0135-4141-9179-a0e9c343ad73
caps.latest.revision: 39
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 39
---
# WSHttpBinding
In questo esempio viene illustrato come implementare un servizio tipico e un client tipico utilizzando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Questo esempio è costituito da un programma di console client \(client.exe\) e da una libreria di servizi ospitati da Internet Information Services \(IIS\).Il servizio implementa un contratto che definisce un modello di comunicazione request\/reply.Il contratto viene definito dall'interfaccia `ICalculator` che espone operazioni matematiche \(somma, sottrazione, moltiplicazione e divisione\).Il client esegue richieste sincrone a un'operazione matematica specificata e il servizio risponde fornendo il risultato.L'attività del client è visibile nella finestra della console.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\WS\wsHttp`  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Questo esempio espone il contratto `ICalculator` utilizzando [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).La configurazione di questa associazione è stata espansa nel file Web.config.  
  
```  
<bindings>  
  <wsHttpBinding>  
    <!--The following is the expanded configuration section for a-->  
    <!--WSHttpBinding. Each property is configured with the default-->   
    <!--value. See the ReliableSession, TransactionFlow, -->  
    <!--TransportSecurity, and MessageSecurity samples in the WS -->  
    <!--directory to learn how to configure these features. -->  
    <binding name="Binding1"  
              bypassProxyOnLocal="false"   
              transactionFlow="false"   
              hostNameComparisonMode="StrongWildcard"  
              maxBufferPoolSize="524288"   
              maxReceivedMessageSize="65536"  
              messageEncoding="Text"   
              textEncoding="utf-8"   
              useDefaultWebProxy="true"  
              allowCookies="false">  
      <reliableSession ordered="true"   
                       inactivityTimeout="00:10:00"  
                       enabled="false" />  
      <security mode="Message">  
        <message clientCredentialType="Windows"   
                 negotiateServiceCredential="true"  
                 algorithmSuite="Default"   
                 establishSecurityContext="true" />  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 Sull'elemento `binding` di base, il valore `maxReceivedMessageSize` consente di configurare la dimensione massima di un messaggio in arrivo \(in byte\).Il valore `hostNameComparisonMode` consente di configurare se il nome host viene considerato quando si esegue il demultiplexing dei messaggi al servizio.Il valore `messageEncoding` consente di configurare se utilizzare la codifica di testo o MTOM per i messaggi.Il valore `textEncoding` consente di configurare la codifica dei caratteri per i messaggi.Il valore `bypassProxyOnLocal` consente di configurare se utilizzare un proxy HTTP per la comunicazione locale.Il valore `transactionFlow` configura se la transazione corrente viene propagata \(se un'operazione è configurata per il flusso delle transazioni\).  
  
 Sull'elemento [\<sessioneAttendibile\>](../../../../docs/framework/configure-apps/file-schema/wcf/reliablesession.md), il valore booleano abilitato configura se le sessioni affidabili sono abilitate.Il valore `ordered` configura se l'ordinamento dei messaggi viene mantenuto.Il valore `inactivityTimeout` configura per quanto tempo una sessione può essere inattiva prima che venga generato un errore.  
  
 In [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md), il valore `mode` configura quale modalità di sicurezza deve essere utilizzata.In questo esempio viene utilizzata la sicurezza dei messaggi e pertanto [\<messaggio\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) viene specificato in [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md).  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 utilizzando il comando seguente.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Verificare di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche
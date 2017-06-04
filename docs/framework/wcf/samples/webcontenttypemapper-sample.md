---
title: "Esempio di WebContentTypeMapper | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Esempio di WebContentTypeMapper
In questo esempio viene illustrato come eseguire il mapping di nuovi tipi di contenuto a formati del corpo del messaggio di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
 L'elemento <xref:System.ServiceModel.Description.WebHttpEndpoint> inserisce il codificatore di messaggi Web, che consente a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di ricevere messaggi JSON, XML o binari non elaborati sullo stesso endpoint.Il codificatore determina il formato del corpo del messaggio analizzando il tipo di contenuto HTTP della richiesta.In questo esempio viene presentata la classe <xref:System.ServiceModel.Channels.WebContentTypeMapper>, che consente all'utente di controllare il mapping tra il tipo di contenuto e il formato del corpo.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un set di mapping predefiniti per i tipi di contenuto.Ad esempio, `application/json` esegue il mapping a JSON e `text/xml` esegue il mapping a XML.Qualsiasi tipo di contenuto per cui non viene eseguito il mapping a JSON o a XML, viene associato al formato binario non elaborato.  
  
 In alcuni scenari \(ad esempio, API di tipo push\), lo sviluppatore del servizio non controlla il tipo di contenuto restituito dal client.Ad esempio, i client potrebbero restituire JSON come `text/javascript` anziché `application/json`.In questo caso, lo sviluppatore del servizio deve fornire un tipo che deriva da <xref:System.ServiceModel.Channels.WebContentTypeMapper> per gestire correttamente il tipo di contenuto specificato, come illustrato nell'esempio di codice seguente.  
  
```  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
  
```  
  
 È necessario che il tipo esegua l'override del metodo <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29>.Il metodo deve valutare l'argomento `contentType` e restituire uno dei seguenti valori: <xref:System.ServiceModel.Channels.WebContentFormat>, <xref:System.ServiceModel.Channels.WebContentFormat>, <xref:System.ServiceModel.Channels.WebContentFormat>, or <xref:System.ServiceModel.Channels.WebContentFormat>.La restituzione di <xref:System.ServiceModel.Channels.WebContentFormat> rinvia ai mapping del codificatore di messaggi Web predefiniti.Nell'esempio di codice precedente il tipo di contenuto `text/javascript` viene associato a JSON e tutti gli altri mapping rimangono immutati.  
  
 Per utilizzare la classe `JsonContentTypeMapper`, modificare il file Web.config nel modo seguente:  
  
```  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 Per verificare il requisito per l'utilizzo di JsonContentTypeMapper, rimuovere l'attributo contentTypeMapper dal file di configurazione illustrato in precedenza.Si verifica un errore durante il caricamento della pagina client quando si tenta di utilizzare  `text/javascript` per inviare contenuto JSON.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Compilare la soluzione WebContentTypeMapperSample.sln come descritto in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Passare a http:\/\/localhost\/ServiceModelSamples\/JCTMClientPage.htm \(non aprire JCTMClientPage.htm nel browser dalla directory del progetto\).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
  
## Vedere anche
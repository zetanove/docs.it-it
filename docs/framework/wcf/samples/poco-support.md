---
title: "Supporto POCO | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3846ca73-2819-4ca2-8367-dc739dde5a5b
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Supporto POCO
In questo esempio viene illustrato il supporto di serializzazione per i tipi non contrassegnati, ovvero tipi ai quali non sono stati applicati attributi di serializzazione, definiti talvolta tipi di oggetto POCO \(Plain Old CLR Object\).Tramite <xref:System.Runtime.Serialization.DataContractSerializer> viene dedotto un contratto dati per tutti i tipi contrassegnati pubblici che dispongono di un costruttore predefinito.I contratti dati consentono di passare dati strutturati a e da i servizi.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] tipi non contrassegnati, vedere [Tipi serializzabili](../../../../docs/framework/wcf/feature-details/serializable-types.md).  
  
 Questo esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), ma utilizza numeri complessi anziché tipi numerici primitivi.È inoltre simile all'esempio [Contratto dati di base](../../../../docs/framework/wcf/samples/basic-data-contract.md), tranne per il fatto che gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> non vengono utilizzati.  
  
 Il servizio è ospitato da Internet Information Services \(IIS\) e il client è un'applicazione console \(con estensione exe\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 La classe `ComplexNumber` viene utilizzata in `ServiceContract`.Il tipo `ComplexNumber` non dispone degli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute>, come illustrato nel codice di esempio seguente.Per impostazione predefinita, le proprietà e i campi pubblici vengono serializzati.  
  
```  
public class ComplexNumber  
{  
    public double Real;  
    public double Imaginary;  
    public ComplexNumber()  
    {  
        Real = double.MinValue;  
        Imaginary = double.MinValue;  
    }  
    public ComplexNumber(double real, double imaginary)  
    {  
        this.Real = real;  
        this.Imaginary = imaginary;  
    }  
}  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Contract\Data\POCO`  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>   
 [Tipi serializzabili](../../../../docs/framework/wcf/feature-details/serializable-types.md)
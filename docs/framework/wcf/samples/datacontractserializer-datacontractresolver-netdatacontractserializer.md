---
title: "Utilizzo di DataContractSerializer e DataContractResolver per fornire la funzionalit&#224; di NetDataContractSerializer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1376658f-f695-45f7-a7e0-94664e9619ff
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Utilizzo di DataContractSerializer e DataContractResolver per fornire la funzionalit&#224; di NetDataContractSerializer
Questo esempio dimostra come l'utilizzo di <xref:System.Runtime.Serialization.DataContractSerializer> con un <xref:System.Runtime.Serialization.DataContractResolver> appropriato offra la stessa funzionalità di <xref:System.Runtime.Serialization.NetDataContractSerializer>.Questo esempio mostra come creare il <xref:System.Runtime.Serialization.DataContractResolver> appropriato e come aggiungerlo a <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
## Dettagli dell'esempio  
 Le classi <xref:System.Runtime.Serialization.NetDataContractSerializer> e <xref:System.Runtime.Serialization.DataContractSerializer> differiscono per un aspetto importante: la classe <xref:System.Runtime.Serialization.NetDataContractSerializer> include informazioni di tipo CLR nell'XML serializzato, a differenza della classe <xref:System.Runtime.Serialization.DataContractSerializer>.Pertanto, la classe <xref:System.Runtime.Serialization.NetDataContractSerializer> può essere utilizzata solo se le estremità di serializzazione e deserializzazione condividono gli stessi tipi CLR.Si consiglia tuttavia di utilizzare la classe <xref:System.Runtime.Serialization.DataContractSerializer> perché le prestazioni sono migliori rispetto alla classe <xref:System.Runtime.Serialization.NetDataContractSerializer>.È possibile modificare le informazioni serializzate in <xref:System.Runtime.Serialization.DataContractSerializer> aggiungendo un <xref:System.Runtime.Serialization.DataContractResolver>.  
  
 L'esempio è costituito da due progetti.Il primo progetto utilizza <xref:System.Runtime.Serialization.NetDataContractSerializer> per serializzare un oggetto.Il secondo progetto utilizza <xref:System.Runtime.Serialization.DataContractSerializer> con un <xref:System.Runtime.Serialization.DataContractResolver> per offrire la stessa funzionalità del primo progetto.  
  
 Nell'esempio di codice seguente viene mostrata l'implementazione di un <xref:System.Runtime.Serialization.DataContractResolver> personalizzato, denominato `MyDataContractResolver`, aggiunto a <xref:System.Runtime.Serialization.DataContractSerializer> nel progetto DCSwithDCR.  
  
```  
class MyDataContractResolver : DataContractResolver  
{  
    private XmlDictionary dictionary = new XmlDictionary();  
  
    public MyDataContractResolver()  
    {  
    }  
  
    // Used at deserialization  
    // Allows users to map xsi:type name to any Type   
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        Type type = knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        if (type == null)  
        {  
            type = Type.GetType(typeName + ", " + typeNamespace);  
        }  
        return type;  
    }  
  
    // Used at serialization  
    // Maps any Type to a new xsi:type representation  
    public override void ResolveType(Type dataContractType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        knownTypeResolver.ResolveType(dataContractType, null, out typeName, out typeNamespace);  
        if (typeName == null || typeNamespace == null)  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add(dataContractType.FullName);  
            typeNamespace = dictionary.Add(dataContractType.Assembly.FullName);  
        }  
    }  
}  
  
```  
  
#### Per utilizzare questo esempio  
  
1.  Utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], aprire il file della soluzione DCRSample.sln.  
  
2.  Fare clic con il pulsante destro del mouse sul file della soluzione e scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Pagine proprietà soluzione**, in **Proprietà comuni**, **Progetto di avvio**, selezionare **Progetti di avvio multipli:**.  
  
4.  Accanto al progetto **DCSwithDCR**, selezionare **Avvia** dall'elenco a discesa **Azione**.  
  
5.  Accanto al progetto **NetDCS**, selezionare **Avvia** dall'elenco a discesa **Azione**.  
  
6.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
7.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
8.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Contract\Data\NetDcSasDcSwithDCR`  
  
## Vedere anche
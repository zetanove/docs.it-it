---
title: "Esempio di DataContractSerializer | Microsoft Docs"
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
  - "Formattatore XML"
ms.assetid: e0a2fe89-3534-48c8-aa3c-819862224571
caps.latest.revision: 37
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 37
---
# Esempio di DataContractSerializer
Nell'esempio relativo a DataContractSerializer viene illustrata la classe <xref:System.Runtime.Serialization.DataContractSerializer>, che esegue servizi generali di serializzazione e di deserializzazione per le classi del contratto dati.  L'esempio crea un oggetto `Record` , lo serializza a un flusso di memoria e quindi deserializza il flusso di memoria a un altro oggetto `Record` per illustrare l'uso di <xref:System.Runtime.Serialization.DataContractSerializer>.  L'esempio serializza quindi l'oggetto `Record` usando un writer binario per illustrare come il writer influisce sulla serializzazione.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Il contratto dati per `Record` viene illustrato nell'esempio di codice seguente.  
  
```  
[DataContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
internal class Record  
{  
    private double n1;  
    private double n2;  
    private string operation;  
    private double result;  
  
    internal Record(double n1, double n2, string operation, double result)  
    {  
        this.n1 = n1;  
        this.n2 = n2;  
        this.operation = operation;  
        this.result = result;  
    }  
  
    [DataMember]  
    internal double OperandNumberOne  
    {  
        get { return n1; }  
        set { n1 = value; }  
    }  
  
    [DataMember]  
    internal double OperandNumberTwo  
    {  
        get { return n2; }  
        set { n2 = value; }  
    }  
  
    [DataMember]  
    internal string Operation  
    {  
        get { return operation; }  
        set { operation = value; }  
    }  
  
    [DataMember]  
    internal double Result  
    {  
        get { return result; }  
        set { result = value; }  
    }  
  
    public override string ToString()  
    {  
        return string.Format("Record: {0} {1} {2} = {3}", n1,  
            operation, n2, result);  
    }  
}  
```  
  
 L'esempio di codice crea un oggetto `Record` denominato `record1`, quindi visualizza l'oggetto.  
  
```  
Record record1 = new Record(1, 2, "+", 3);  
Console.WriteLine("Original record: {0}", record1.ToString());  
  
```  
  
 L'esempio usa quindi <xref:System.Runtime.Serialization.DataContractSerializer> per serializzare `record1` in un flusso di memoria.  
  
```  
MemoryStream stream1 = new MemoryStream();  
  
//Serialize the Record object to a memory stream using DataContractSerializer.  
DataContractSerializer serializer = new DataContractSerializer(typeof(Record));  
serializer.WriteObject(stream1, record1);  
  
```  
  
 L'esempio usa quindi <xref:System.Runtime.Serialization.DataContractSerializer> per deserializzare di nuovo il flusso di memoria in un nuovo oggetto `Record` e lo visualizza.  
  
```  
stream1.Position = 0;  
  
//Deserialize the Record object back into a new record object.  
Record record2 = (Record)serializer.ReadObject(stream1);  
  
Console.WriteLine("Deserialized record: {0}", record2.ToString());  
  
```  
  
 Per impostazione predefinita, `DataContractSerializer` codifica gli oggetti in un flusso usando una rappresentazione testuale di XML.  Tuttavia, è possibile influenzare la codifica del XML usando un writer diverso.  Nell'esempio viene creato un writer binario chiamando <xref:System.Xml.XmlDictionaryWriter.CreateBinaryWriter%2A>.  Il writer e l'oggetto record vengono quindi passati al serializzatore quando chiama <xref:System.Runtime.Serialization.DataContractSerializer.WriteObjectContent%2A>.  Infine, l'esempio scarica il writer e segnala la lunghezza dei flussi.  
  
```  
MemoryStream stream2 = new MemoryStream();  
  
XmlDictionaryWriter binaryDictionaryWriter = XmlDictionaryWriter.CreateBinaryWriter(stream2);  
serializer.WriteObject(binaryDictionaryWriter, record1);  
binaryDictionaryWriter.Flush();  
  
//report the length of the streams  
Console.WriteLine("Text Stream is {0} bytes long", stream1.Length);  
Console.WriteLine("Binary Stream is {0} bytes long", stream2.Length);  
```  
  
 Quando si esegue l'esempio, vengono visualizzati il record originale e il record deserializzato, seguiti dal confronto tra la lunghezza della codifica del testo e della codifica binaria.  Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Original record: Record: 1 + 2 = 3  
Deserialized record: Record: 1 + 2 = 3  
Text Stream is 233 bytes long  
Binary Stream is 156 bytes long  
  
Press <ENTER> to terminate client.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio, avviare il client dal prompt dei comandi digitando client\\bin\\client.exe.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Contract\Data\DataContractSerializer`  
  
## Vedere anche
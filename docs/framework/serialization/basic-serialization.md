---
title: "Serializzazione di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "serializzazione binaria, serializzazione di base"
  - "serializzazione, serializzazione di base"
ms.assetid: d899d43c-335a-433e-a589-cd187192984f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Serializzazione di base
Il modo più semplice per rendere serializzabile una classe è contrassegnarla con l'attributo [Serializable](frlrfSystemSerializableAttributeClassTopic), come riportato di seguito.  
  
```csharp  
[Serializable]  
public class MyObject {  
  public int n1 = 0;  
  public int n2 = 0;  
  public String str = null;  
}  
```  
  
 Nell'esempio di codice riportato di seguito viene illustrato come è possibile serializzare un'istanza di tale classe in un file.  
  
```csharp  
MyObject obj = new MyObject();  
obj.n1 = 1;  
obj.n2 = 24;  
obj.str = "Some String";  
IFormatter formatter = new BinaryFormatter();  
Stream stream = new FileStream("MyFile.bin", FileMode.Create, FileAccess.Write, FileShare.None);  
formatter.Serialize(stream, obj);  
stream.Close();  
```  
  
 In questo esempio viene utilizzato un formattatore binario per eseguire la serializzazione.È sufficiente creare un'istanza del flusso e il formattatore che si intende di utilizzare, quindi chiamare il metodo **Serialize** sul formattatore.Il flusso e l'oggetto da serializzare vengono forniti a questa chiamata come parametri.Sebbene non sia stato dimostrato in modo esplicito in questo esempio, verranno serializzate tutte le variabili del membro di una classe, anche quelle contrassegnate come private.Da questo punto di vista, la serializzazione binaria differisce dalla [classe XMLSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)che serializza solo campi pubblici.Per informazioni sull'esclusione di variabili membro dalla serializzazione binaria, vedere [Serializzazione selettiva](../../../docs/framework/serialization/selective-serialization.md).  
  
 Il ripristino dell'oggetto allo stato antecedente risulta molto semplice.Innanzitutto, creare un flusso per la lettura e un [formattatore](frlrfSystemRuntimeSerializationFormatterClassTopic), quindi istruire il formattatore in modo che deserializzi l'oggetto.Nell'esempio di codice riportato di seguito viene illustrato come fare.  
  
```csharp  
IFormatter formatter = new BinaryFormatter();  
Stream stream = new FileStream("MyFile.bin", FileMode.Open, FileAccess.Read, FileShare.Read);  
MyObject obj = (MyObject) formatter.Deserialize(stream);  
stream.Close();  
  
// Here's the proof.  
Console.WriteLine("n1: {0}", obj.n1);  
Console.WriteLine("n2: {0}", obj.n2);  
Console.WriteLine("str: {0}", obj.str);  
```  
  
 La classe [BinaryFormatter](frlrfSystemRuntimeSerializationFormattersBinaryBinaryFormatterClassTopic) utilizzata in precedenza è molto efficiente e produce un flusso di byte compresso.Tutti gli oggetti serializzati con questo formattatore possono inoltre essere deserializzati con lo stesso formattatore, rendendolo uno strumento ideale per la serializzazione di oggetti che saranno deserializzati su .NET Framework.È importante notare che i costruttori non vengono chiamati quando un oggetto viene deserializzato.Questo vincolo è posizionato sulla deserializzazione per motivi di prestazioni.Tuttavia, in tal modo vengono violati alcuni dei normali contratti stabiliti tra il runtime e il writer dell'oggetto e gli sviluppatori devono essere certi di comprendere le ramificazioni quando contrassegnano un oggetto come serializzabile.  
  
 Se la portabilità è un requisito, utilizzare [SoapFormatter](frlrfSystemRuntimeSerializationFormattersSoapSoapFormatterClassTopic).Sostituire semplicemente **BinaryFormatter** nel codice riportato in precedenza con **SoapFormatter**, quindi chiamare **Serialize** e **Deserialize** come fatto in precedenza.Questo formattatore produce il seguente output per l'esempio utilizzato in precedenza.  
  
```  
<SOAP-ENV:Envelope  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
  xmlns:SOAP- ENC="http://schemas.xmlsoap.org/soap/encoding/"  
  xmlns:SOAP- ENV="http://schemas.xmlsoap.org/soap/envelope/"  
  SOAP-ENV:encodingStyle=  
  "http://schemas.microsoft.com/soap/encoding/clr/1.0"  
  "http://schemas.xmlsoap.org/soap/encoding/"  
  xmlns:a1="http://schemas.microsoft.com/clr/assem/ToFile">  
  
  <SOAP-ENV:Body>  
    <a1:MyObject id="ref-1">  
      <n1>1</n1>  
      <n2>24</n2>  
      <str id="ref-3">Some String</str>  
    </a1:MyObject>  
  </SOAP-ENV:Body>  
</SOAP-ENV:Envelope>  
```  
  
 È importante notare che l'attributo **Serializable** non può essere ereditato.Se una nuova classe viene derivata da `MyObject`, tale classe deve anche essere contrassegnata con l'attributo; in caso contrario non sarà possibile serializzarla.Ad esempio, se si tenta di serializzare un'istanza della classe riportata di seguito, si riceverà una [SerializationException](frlrfSystemRuntimeSerializationSerializationExceptionClassTopic) che informa che il tipo `MyStuff` non è contrassegnato come serializzabile.  
  
```csharp  
public class MyStuff : MyObject   
{  
  public int n3;  
}  
```  
  
 L'utilizzo dell'attributo **Serializable** è comodo ma ha limitazioni come dimostrato in precedenza.Fare riferimento alle [Linee guida relative alla serializzazione](../../../docs/framework/serialization/serialization-guidelines.md) per le informazioni su quando è necessario contrassegnare una classe per la serializzazione; la serializzazione non può essere aggiunta a una classe dopo la sua compilazione.  
  
## Vedere anche  
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)   
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)
---
title: "Esempio di tecnologia di serializzazione di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9d824e16-08d1-4a36-bc7f-2388c1f75f34
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Esempio di tecnologia di serializzazione di base
[Scarica esempio](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/Basic.zip.exe)  
  
 In questo esempio viene illustrata la capacità di Common Language Runtime di serializzare in un flusso il grafico di un oggetto contenuto in memoria.Per la serializzazione, è possibile utilizzare l'oggetto <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.Un elenco collegato, contenente dati, viene serializzato in un flusso di file o deserializzato da tale flusso.In entrambi i casi l'elenco viene visualizzato per consentire di esaminare i risultati.L'elenco collegato è di tipo `LinkedList`, un tipo definito in questo esempio.  
  
 Per ulteriori informazioni sulla serializzazione, vedere i commenti nei file di codice sorgente e build.proj.  
  
### Per compilare l'esempio utilizzando il prompt dei comandi  
  
1.  Spostarsi in una delle sottodirectory specifiche del linguaggio della directory Technologies\\Serialization\\Runtime Serialization\\Basic utilizzando il prompt dei comandi.  
  
2.  Dalla riga di comando digitare **msbuild SerializationCS.sln**, **msbuild SerializationJSL.sln** o **msbuild SerializationVB.sln**, a seconda del linguaggio di programmazione che si desidera utilizzare.  
  
### Per compilare l'esempio utilizzando Visual Studio  
  
1.  Aprire [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)], quindi passare a una delle sottodirectory specifiche del linguaggio relative all'esempio.  
  
2.  Fare doppio clic sull'icona relativa a SerializationCS.sln, SerializationJSL.sln o SerializationVB.sln, a seconda del linguaggio di programmazione che si desidera utilizzare, per aprire il file in Visual Studio.  
  
3.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
 L'applicazione verrà compilata nella sottodirectory predefinita \\bin o \\bin\\Debug.  
  
### Per eseguire l’esempio  
  
1.  Spostarsi nella directory contenente l'eseguibile compilato.  
  
2.  Digitare **Serialization.exe**, con i valori di parametro desiderati, dalla riga di comando.  
  
    > [!NOTE]
    >  L'esempio compila un'applicazione console.Per visualizzare l'output dell'applicazione, è necessario avviarla dalla finestra del prompt dei comandi.  
  
## Osservazioni  
 L'applicazione di esempio accetta parametri della riga di comando che indicano il test da eseguire.Per serializzare un elenco costituito da 10 nodi in un file denominato **Test.xml** mediante il formattatore SOAP, utilizzare i parametri **sx Test.xml 10**.  
  
 Di seguito è riportato un esempio:  
  
 **Serialize.exe \-sx Test.xml 10**  
  
 Per deserializzare il file **Test.xml** dell'esempio precedente, utilizzare i parametri **dx Test.xml**.  
  
 Di seguito è riportato un esempio:  
  
 **Serialize.exe \-dx Test.xml**  
  
 Nei due esempi precedenti, la lettera "x" nell'opzione della riga di comando indica che si desidera utilizzare la serializzazione SOAP XML.Per utilizzare la serializzazione binaria, è possibile utilizzare la lettera "b".Se si desidera eseguire la serializzazione con un numero di nodi molto elevato, può essere opportuno reindirizzare l'output della console in un file.  
  
 Di seguito è riportato un esempio:  
  
 **Serialize.exe \-sb Test.bin 10000 \>somefile.txt**  
  
 Nell'elenco riportato di seguito vengono descritte in modo sintetico le classi e le tecnologie utilizzate nell'esempio.  
  
-   Serializzazione in fase di esecuzione  
  
    -   <xref:System.Runtime.Serialization.IFormatter> \- Consente di fare riferimento a un oggetto <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> o <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>.  
  
    -   <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> \- Consente di serializzare un elenco collegato in un flusso in formato binario.Il formattatore binario utilizza un formato riconosciuto solo dal tipo <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.Tuttavia, i dati sono concisi.  
  
    -   <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> \- Consente di serializzare un elenco collegato in un flusso in formato SOAP,che è un formato standard.  
  
-   I\/O flusso  
  
    -   <xref:System.IO.Stream> \- Consente di eseguire la serializzazione e la deserializzazione.Il tipo di flusso specifico utilizzato in questo esempio è <xref:System.IO.FileStream>.È tuttavia possibile utilizzare la serializzazione con qualsiasi tipo derivato da <xref:System.IO.Stream>.  
  
    -   <xref:System.IO.File> \- Consente di creare oggetti <xref:System.IO.FileStream> per la lettura e la creazione di file su disco.  
  
    -   <xref:System.IO.FileStream> \- Consente di eseguire la serializzazione e la deserializzazione di elenchi collegati.  
  
## Vedere anche  
 [Classe BinaryFormatter](frlrfSystemRuntimeSerializationFormattersBinaryBinaryFormatterClassTopic)   
 [Classe File](frlrfSystemIOFileClassTopic)   
 [Classe FileStream](frlrfSystemIOFileStreamClassTopic)   
 [Interfaccia IFormatter](frlrfSystemRuntimeSerializationIFormatterClassTopic)   
 [Classe Random](https://msdn.microsoft.com/en-us/library/system.random.aspx)   
 [Attributo SerializableAttribute](frlrfSystemSerializableAttributeClassTopic)   
 [Classe SoapFormatter](frlrfSystemRuntimeSerializationFormattersSoapSoapFormatterClassTopic)   
 [Classe Stream](frlrfSystemIOStreamClassTopic)   
 [Spazio dei nomi System.IO](https://msdn.microsoft.com/en-us/library/system.io.aspx)   
 [Spazio dei nomi System.Runtime.Serialization](frlrfSystemRuntimeSerialization)   
 [Spazio dei nomi System.Xml.Serialization](frlrfSystemXmlSerialization)   
 [Serializzazione di base](../../../docs/framework/serialization/basic-serialization.md)   
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)   
 [Controllo della serializzazione XML mediante attributi](../../../docs/framework/serialization/controlling-xml-serialization-using-attributes.md)   
 [Introduzione alla serializzazione XML](../../../docs/framework/serialization/introducing-xml-serialization.md)   
 [Serializzazione](../../../docs/framework/serialization/index.md)   
 [SOAP Service](http://msdn.microsoft.com/it-it/2051c992-28d1-499e-961f-17e9b675cec9)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)
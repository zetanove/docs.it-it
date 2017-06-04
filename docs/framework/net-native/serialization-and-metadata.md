---
title: "Serializzazione e metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 619ecf1c-1ca5-4d66-8934-62fe7aad78c6
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Serializzazione e metadati
Se l'applicazione serializza e deserializza oggetti, potrebbe essere necessario aggiungere voci al file di direttive di runtime \(rd.xml\) per assicurarsi che i metadati necessari siano presenti in fase di esecuzione.  Esistono due categorie di serializzatori e ciascuna richiede una gestione differente nel file di direttive di runtime:  
  
-   Serializzatori di terze parti basati su reflection.  Richiedono modifiche al file di direttive di runtime e sono descritti nella sezione successiva.  
  
-   Serializzatori non basati su reflection, presenti nella libreria di classi di .NET Framework.  Possono richiedere modifiche al file di direttive di runtime e sono descritti nella sezione [Serializzatori Microsoft](#Microsoft).  
  
<a name="ThirdParty"></a>   
## Serializzatori di terze parti  
 I serializzatori di terze parti, incluso Newtonsoft.JSON, sono in genere basati su reflection.  Dato un oggetto binario di grandi dimensioni \(BLOB\) di dati serializzati, i campi dati vengono assegnati a un tipo concreto cercando i campi del tipo di destinazione per nome.  Come minimo, l'utilizzo di queste librerie provoca eccezioni [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) per ogni oggetto <xref:System.Type> che si prova serializzare o deserializzare in una raccolta `List<Type>`.  
  
 Il modo più semplice per risolvere i problemi causati da metadati mancanti per questi serializzatori è raccogliere i tipi che verranno usati nella serializzazione in un singolo spazio dei nomi \(ad esempio `App.Models`\) e applicarvi una direttiva metadati `Serialize`:  
  
```  
<Namespace Name="App.Models" Serialize="Required PublicAndInternal" />  
```  
  
 Per informazioni sulla sintassi usata in questo esempio, vedere [Elemento \<Namespace\>](../../../docs/framework/net-native/namespace-element-net-native.md).  
  
<a name="Microsoft"></a>   
## Serializzatori Microsoft  
 Nonostante le classi <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> e <xref:System.Xml.Serialization.XmlSerializer> non si basino sulla reflection, richiedono che il codice venga generato in base all'oggetto da serializzare o deserializzare.  I costruttori di overload per ciascun serializzatore includono un parametro <xref:System.Type> che specifica il tipo da serializzare o deserializzare.  Il modo in cui si specifica che il tipo nel codice definisce l'azione che l'utente deve accettare, come illustrato nelle due sezioni.  
  
### typeof usato nel costruttore  
 Se si chiama un costruttore di queste classi di serializzazione e si include la parola chiave [typeof](../Topic/typeof%20\(C%23%20Reference\).md) di C\# nella chiamata al metodo, **non è necessario effettuare operazioni aggiuntive**.  Ad esempio, in ognuna delle seguenti chiamate a un costruttore di classe di serializzazione, la parola chiave `typeof` viene usata come parte dell'espressione passata al costruttore.  
  
 [!code-csharp[ProjectN#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#5)]  
  
 Il compilatore [!INCLUDE[net_native](../../../includes/net-native-md.md)] gestirà automaticamente questo codice.  
  
### typeof usato fuori dal costruttore  
 Se si chiama un costruttore di queste classi di serializzazione e si usa la parola chiave [typeof](../Topic/typeof%20\(C%23%20Reference\).md) di C\# fuori dall'espressione fornita al parametro <xref:System.Type> del costruttore, come nel codice seguente, il compilatore di [!INCLUDE[net_native](../../../includes/net-native-md.md)] può risolvere il tipo:  
  
 [!code-csharp[ProjectN#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#6)]  
  
 In questo caso, è necessario specificare il tipo nel file di direttive di runtime con l'aggiunta di una voce simile alla seguente:  
  
```  
<Type Name="DataSet" Browse="Required Public" />  
```  
  
 Analogamente, se si chiama un costruttore come [XmlSerializer.XmlSerializer\(Type, Type\<xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=fullName> e si fornisce una matrice di oggetti <xref:System.Type> aggiuntivi da serializzare, come nel codice seguente, il compilatore di [!INCLUDE[net_native](../../../includes/net-native-md.md)] non riesce a risolvere questi tipi.  
  
 [!code-csharp[ProjectN#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#7)]  
  
 È necessario aggiungere come quelle riportate di seguito per ogni tipo al file di direttive del runtime:  
  
```  
<Type Name="t" Browse="Required Public" />  
```  
  
 Per informazioni sulla sintassi usata in questo esempio, vedere [Elemento \<Type\>](../../../docs/framework/net-native/type-element-net-native.md).  
  
## Vedere anche  
 [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Elemento \<Type\>](../../../docs/framework/net-native/type-element-net-native.md)   
 [Elemento \<Namespace\>](../../../docs/framework/net-native/namespace-element-net-native.md)
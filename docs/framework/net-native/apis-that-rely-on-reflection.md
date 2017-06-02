---
title: "API basate sulla reflection | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f9532629-6594-4a41-909f-d083f30a42f3
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# API basate sulla reflection
In alcuni casi, l'uso della reflection nel codice non è scontato, quindi la catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)] non conserva i metadati necessari al runtime.  In questo argomento vengono illustrati modelli di programmazione o API comuni non considerati parte dell'API di reflection ma basati sulla reflection per una corretta esecuzione.  Se vengono usati nel codice sorgente, è possibile aggiungere informazioni su di essi al file di direttive di runtime \(.rd.xml\) in modo che le chiamate a queste API non generino un'eccezione [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) o altre eccezioni al runtime.  
  
## Metodo Type.MakeGenericType  
 È possibile creare dinamicamente un'istanza di un tipo generico `AppClass<T>` chiamando il metodo <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> usando un codice simile al seguente:  
  
 [!code-csharp[ProjectN#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/type_makegenerictype1.cs#1)]  
  
 Per una corretta esecuzione del codice al runtime, sono necessari diversi elementi di metadati.  Prima di tutto, sono richiesti metadati `Browse` per il tipo generico privo di istanze, `AppClass<T>`:  
  
```  
<Type Name="App1.AppClass`1" Browse="Required PublicAndInternal" />  
```  
  
 Questo assicura l'esito positivo della chiamata al metodo <xref:System.Type.GetType%28System.String%2CSystem.Boolean%29?displayProperty=fullName> e la restituzione di un oggetto <xref:System.Type> valido.  
  
 Tuttavia, anche se si aggiungono i metadati per il tipo generico privo di istanze, la chiamata al metodo <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> genera un'eccezione [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md):  
  
```  
  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:  
  
App1.AppClass`1<System.Int32>.  
  
```  
  
 È possibile aggiungere la seguente direttiva di runtime al file di direttive di runtime per aggiungere i metadati `Activate` per la specifica creazione di un'istanza in `AppClass<T>` di <xref:System.Int32?displayProperty=fullName>:  
  
```  
  
<TypeInstantiation Name="App1.AppClass" Arguments="System.Int32"   
                   Activate="Required Public" />  
  
```  
  
 Le singole creazioni di istanze in `AppClass<T>` richiedono direttive separate se vengono create con il metodo <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> e non vengono usate staticamente.  
  
## Metodo MethodInfo.MakeGenericMethod  
 In una classe `Class1` con un metodo generico `GetMethod<T>(T t)`, `GetMethod` può essere richiamato mediante reflection usando un codice simile al seguente:  
  
 [!code-csharp[ProjectN#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/makegenericmethod1.cs#2)]  
  
 Per una corretta esecuzione, questo codice richiede diversi elementi di metadati:  
  
-   I metadati `Browse` per il tipo di metodo da chiamare.  
  
-   I metadati `Browse` per il metodo da chiamare.  Se si tratta di un metodo pubblico, l'aggiunta di metadati `Browse` pubblici per il tipo contenitore include anche il metodo.  
  
-   I metadati dinamici per il metodo da chiamare, in modo che il delegato di chiamata della reflection non venga rimosso dalla catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)].  Se i metadati dinamici non sono disponibili per il metodo, viene generata la seguente eccezione quando viene chiamato il metodo <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=fullName>:  
  
    ```  
  
    MakeGenericMethod() cannot create this generic method instantiation because the instantiation was not metadata-enabled: 'App1.Class1.GenMethod<Int32>(Int32)'.  
  
    ```  
  
 Le seguenti direttive di runtime assicurano la disponibilità di tutti i metadati necessari:  
  
```  
  
<Type Name="App1.Class1" Browse="Required PublicAndInternal">  
   <MethodInstantiation Name="GenMethod" Arguments="System.Int32" Dynamic="Required"/>  
</Type>  
  
```  
  
 È necessaria una direttiva `MethodInstantiation` per ogni singola creazione di un'istanza del metodo richiamato dinamicamente; l'elemento `Arguments` viene aggiornato per riflettere ogni singolo argomento di creazione di un'istanza.  
  
## Metodi Array.CreateInstance e Type.MakeTypeArray  
 Il seguente esempio chiama i metodi <xref:System.Type.MakeArrayType%2A?displayProperty=fullName> e <xref:System.Array.CreateInstance%2A?displayProperty=fullName> in un tipo `Class1`.  
  
 [!code-csharp[ProjectN#3](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/array1.cs#3)]  
  
 Se non sono presenti i metadati della matrice, si verificano i seguenti errori:  
  
```  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:  
  
App1.Class1[]  
  
Unfortunately, no further information is available.  
```  
  
 I metadati `Browse` per il tipo di matrice sono richiesti per la creazione dinamica di un'istanza.  La seguente direttiva di runtime consente la creazione dinamica di un'istanza di `Class1[]`.  
  
```  
<Type Name="App1.Class1[]" Browse="Required Public" />  
```  
  
## Vedere anche  
 [Introduzione](../../../docs/framework/net-native/getting-started-with-net-native.md)   
 [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)
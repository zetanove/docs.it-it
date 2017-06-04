---
title: "How to: Load Assemblies into the Reflection-Only Context | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "reflection, reflection-only loader context"
  - "assemblies [.NET Framework], loading for reflection"
  - "attributes [.NET Framework], retrieving"
  - "assemblies [.NET Framework], reflection-only loader context"
  - "reflection-only loader context"
ms.assetid: 9818b660-52f5-423d-a9af-e75163aa7068
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Load Assemblies into the Reflection-Only Context
Il contesto di caricamento Reflection\-Only consente di esaminare gli assembly compilati per altre piattaforme o altre versioni di .NET Framework.  Il codice caricato in questo contesto può essere solo esaminato e non eseguito.  Pertanto, poiché i costruttori non possono essere eseguiti, non è possibile creare oggetti.  Non essendo possibile eseguire il codice, le dipendenze non vengono caricate automaticamente.  Per esaminarle, è necessario caricarle manualmente.  
  
### Per caricare un assembly nel contesto di caricamento Reflection\-Only  
  
1.  Utilizzare l'overload del metodo <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.String%29> per caricare l'assembly in base al nome di visualizzazione oppure il metodo <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> per caricare l'assembly in base al percorso.  Se l'assembly è un'immagine binaria, utilizzare l'overload del metodo [ReflectionOnlyLoad\(Byte\<xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.Byte%5B%5D%29>.  
  
    > [!NOTE]
    >  Non è possibile utilizzare il contesto Reflection\-Only per caricare una versione di mscorlib.dll da una versione di .NET Framework diversa da quella installata nel contesto di esecuzione.  
  
2.  Se l'assembly contiene dipendenze, queste ultime non verranno caricate dal metodo <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>.  Per esaminare le dipendenze, è necessario caricarle manualmente.  
  
3.  Stabilire se un assembly viene caricato nel contesto Reflection\-Only utilizzando la proprietà <xref:System.Reflection.Assembly.ReflectionOnly%2A> dell'assembly.  
  
4.  Se all'assembly o ai tipi in esso contenuti sono applicati attributi, esaminare questi ultimi utilizzando la classe <xref:System.Reflection.CustomAttributeData>, in modo da accertarsi che non venga effettuato alcun tentativo di eseguire il codice nel contesto Reflection\-Only.  Utilizzare l'overload appropriato del metodo <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=fullName> per ottenere gli oggetti <xref:System.Reflection.CustomAttributeData> che rappresentano gli attributi applicati a un assembly, membro, modulo o parametro.  
  
    > [!NOTE]
    >  Gli attributi applicati all'assembly o al relativo contenuto possono essere definiti nell'assembly in questione o in un altro assembly caricato nel contesto Reflection\-Only.  Non è possibile stabilire in anticipo dove sono definiti gli attributi.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come esaminare gli attributi applicati a un assembly caricato nel contesto Reflection\-Only.  
  
 Nell'esempio di codice riportato di seguito viene definito un attributo personalizzato con due costruttori e una proprietà.  L'attributo è applicato all'assembly, a un tipo dichiarato nell'assembly, a un metodo del tipo e a un parametro del metodo.  Una volta eseguito, l'assembly verrà caricato automaticamente nel contesto Reflection\-Only e verranno visualizzate informazioni sugli attributi personalizzati applicati all'assembly e ai tipi e membri che contiene.  
  
> [!NOTE]
>  Per semplificare l'esempio di codice, l'assembly carica ed esamina se stesso.  In genere, non è probabile che lo stesso assembly venga caricato sia nel contesto di esecuzione che nel contesto Reflection\-Only.  
  
 [!code-cpp[CustomAttributeData#1](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source.cpp#1)]
 [!code-csharp[CustomAttributeData#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source.cs#1)]
 [!code-vb[CustomAttributeData#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source.vb#1)]  
  
## Vedere anche  
 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>   
 <xref:System.Reflection.Assembly.ReflectionOnly%2A>   
 <xref:System.Reflection.CustomAttributeData>
---
title: "Viewing Type Information | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
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
  - "types, viewing type information"
  - "Type object"
  - "viewing type information"
  - "reflection, viewing type information"
ms.assetid: 7e7303a9-4064-4738-b4e7-b75974ed70d2
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Viewing Type Information
La classe <xref:System.Type?displayProperty=fullName> è fondamentale per la reflection.  Quando la reflection lo richiede, Common Language Runtime crea l'oggetto **Type** relativo a un tipo caricato.  Per ottenere informazioni sul tipo, è possibile utilizzare metodi, campi, proprietà e classi annidate dell'oggetto **Type**.  
  
 Utilizzare <xref:System.Reflection.Assembly.GetType%2A?displayProperty=fullName> o <xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=fullName> per ottenere oggetti **Type** da assembly che non sono stati caricati, passando il nome del tipo o dei tipi desiderati.  Utilizzare <xref:System.Type.GetType%2A?displayProperty=fullName> per ottenere oggetti **Type** da un assembly già caricato.  Utilizzare <xref:System.Reflection.Module.GetType%2A?displayProperty=fullName> e <xref:System.Reflection.Module.GetTypes%2A?displayProperty=fullName> per ottenere il modulo degli oggetti **Type**.  
  
> [!NOTE]
>  Se si desidera esaminare e modificare tipi e metodi generici, vedere le informazioni aggiuntive disponibili in [Reflection and Generic Types](../../../docs/framework/reflection-and-codedom/reflection-and-generic-types.md) e [How to: Examine and Instantiate Generic Types with Reflection](../../../docs/framework/reflection-and-codedom/how-to-examine-and-instantiate-generic-types-with-reflection.md).  
  
 Nell'esempio riportato di seguito viene illustrata la sintassi necessaria per ottenere il modulo e l'oggetto <xref:System.Reflection.Assembly> relativi a un assembly.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source5.cpp#6)]
 [!code-csharp[Conceptual.Types.ViewInfo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source5.cs#6)]
 [!code-vb[Conceptual.Types.ViewInfo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source5.vb#6)]  
  
 Nell'esempio che segue viene illustrato come ottenere oggetti **Type** da un assembly caricato.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source5.cpp#7)]
 [!code-csharp[Conceptual.Types.ViewInfo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source5.cs#7)]
 [!code-vb[Conceptual.Types.ViewInfo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source5.vb#7)]  
  
 Una volta ottenuto un oggetto **Type**, è possibile avvalersi di svariati modi per ottenere informazioni sui membri del tipo.  Per ottenere informazioni su tutti i membri del tipo è ad esempio possibile chiamare il metodo <xref:System.Type.GetMembers%2A?displayProperty=fullName>, che ottiene una matrice di oggetti <xref:System.Reflection.MemberInfo>, ciascuno dei quali descrive un membro del tipo.  
  
 È inoltre possibile utilizzare i metodi della classe **Type** per recuperare informazioni su uno o più costruttori, metodi, eventi, campi o proprietà di cui si specifica il nome.  <xref:System.Type.GetConstructor%2A?displayProperty=fullName>, ad esempio, incapsula uno specifico costruttore della classe corrente.  
  
 Se si dispone di un oggetto **Type**, sarà possibile utilizzare la proprietà <xref:System.Type.Module%2A?displayProperty=fullName> per ottenere un oggetto che incapsula il modulo contenente il tipo.  Per individuare un oggetto che incapsula l'assembly contenente il modulo, utilizzare la proprietà <xref:System.Reflection.Module.Assembly%2A?displayProperty=fullName>.  Per ottenere direttamente l'assembly che incapsula il tipo, utilizzare la proprietà <xref:System.Type.Assembly%2A?displayProperty=fullName>.  
  
## System.Type e ConstructorInfo  
 Nell'esempio riportato di seguito viene illustrato come elencare i costruttori di una classe, nel caso specifico la classe <xref:System.String>.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.Types.ViewInfo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source1.cs#1)]
 [!code-vb[Conceptual.Types.ViewInfo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source1.vb#1)]  
  
## MemberInfo, MethodInfo, FieldInfo e PropertyInfo  
 Per ottenere informazioni su metodi, proprietà, eventi e campi del tipo, utilizzare gli oggetti <xref:System.Reflection.MemberInfo>, <xref:System.Reflection.MethodInfo>, <xref:System.Reflection.FieldInfo> o <xref:System.Reflection.PropertyInfo>.  
  
 Nell'esempio riportato di seguito viene utilizzato **MemberInfo** per elencare il numero di membri della classe **System.IO.File** e viene utilizzata la proprietà [System.Type.IsPublic](frlrfSystemTypeClassIsPublicTopic) per determinare la visibilità della classe.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.Types.ViewInfo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source2.cs#2)]
 [!code-vb[Conceptual.Types.ViewInfo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source2.vb#2)]  
  
 Nell'esempio che segue viene analizzato il tipo del membro specificato.  Viene eseguita una reflection su un membro della classe **MemberInfo** e ne viene elencato il tipo.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source3.cpp#3)]
 [!code-csharp[Conceptual.Types.ViewInfo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source3.cs#3)]
 [!code-vb[Conceptual.Types.ViewInfo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source3.vb#3)]  
  
 Nell'esempio riportato di seguito vengono utilizzate tutte le classi **\*Info** di Reflection insieme a <xref:System.Reflection.BindingFlags> per elencare tutti i membri \(costruttori, campi, proprietà, eventi e metodi\) della classe specificata, distinguendo tra membri statici e di istanza.  
  
 [!code-cpp[Conceptual.Types.ViewInfo#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.Types.ViewInfo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source4.cs#4)]
 [!code-vb[Conceptual.Types.ViewInfo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source4.vb#4)]  
  
## Vedere anche  
 <xref:System.Reflection.BindingFlags>   
 <xref:System.Reflection.Assembly.GetType%2A?displayProperty=fullName>   
 <xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=fullName>   
 <xref:System.Type.GetType%2A?displayProperty=fullName>   
 <xref:System.Type.GetMembers%2A?displayProperty=fullName>   
 <xref:System.Type.GetFields%2A?displayProperty=fullName>   
 <xref:System.Reflection.Module.GetType%2A?displayProperty=fullName>   
 <xref:System.Reflection.Module.GetTypes%2A?displayProperty=fullName>   
 <xref:System.Reflection.MemberInfo>   
 <xref:System.Reflection.ConstructorInfo>   
 <xref:System.Reflection.MethodInfo>   
 <xref:System.Reflection.FieldInfo>   
 <xref:System.Reflection.EventInfo>   
 <xref:System.Reflection.ParameterInfo>   
 [Reflection and Generic Types](../../../docs/framework/reflection-and-codedom/reflection-and-generic-types.md)
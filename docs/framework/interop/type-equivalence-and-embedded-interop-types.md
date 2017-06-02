---
title: "Type Equivalence and Embedded Interop Types | Microsoft Docs"
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
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "type equivalence"
  - "embedded interop types"
  - "primary interop assemblies,not necessary in CLR version 4"
  - "NoPIA"
ms.assetid: 78892eba-2a58-4165-b4b1-0250ee2f41dc
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Type Equivalence and Embedded Interop Types
A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Common Language Runtime supporta l'incorporamento delle informazioni sui tipi COM direttamente in assembly gestiti, anziché richiedere che tali assembly ottengano le informazioni dagli assembly di interoperabilità.  Poiché le informazioni sui tipi incorporate includono solo i tipi e i membri realmente utilizzati da un assembly gestito, è possibile che due assembly gestiti presentino visualizzazioni molto diverse dello stesso tipo COM.  Ogni assembly gestito dispone di un oggetto <xref:System.Type> diverso per rappresentare la visualizzazione del tipo COM.  Common Language Runtime supporta l'equivalenza del tipo tra queste visualizzazioni diverse per interfacce, strutture, enumerazioni e delegati.  
  
 Equivalenza del tipo significa che di un oggetto COM passato da un assembly gestito a un altro è possibile eseguire il cast al tipo gestito appropriato nell'assembly ricevente.  
  
> [!NOTE]
>  L'equivalenza del tipo e i tipi di interoperabilità incorporati semplificano la distribuzione di applicazioni e componenti aggiuntivi che utilizzano componenti COM, in quanto non è necessario distribuire assembly di interoperabilità con le applicazioni.  Gli sviluppatori di componenti COM devono comunque creare assembly di interoperabilità primari \(PIA\) se desiderano che i componenti vengano utilizzati dalle versioni di .NET Framework precedenti.  
  
## Equivalenza del tipo  
 L'equivalenza dei tipi COM è supportata per interfacce, strutture, enumerazioni e delegati.  I tipi COM sono qualificabili come equivalenti se soddisfano tutte le seguenti condizioni:  
  
-   I tipi sono entrambi interfacce, entrambi strutture, entrambi enumerazioni o entrambi delegati.  
  
-   L'identità dei tipi è la stessa, come descritto nella sezione che segue.  
  
-   Entrambi i tipi sono idonei per l'equivalenza del tipo, come descritto nella sezione [Contrassegno dei tipi COM per l'equivalenza del tipo](#type_equiv).  
  
### Identità del tipo  
 Si dice che due tipi hanno la stessa identità quando i relativi ambiti e le identità corrispondono; in altre parole, se ognuno di essi dispone dell'attributo <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> e i due attributi hanno proprietà <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> e <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A> corrispondenti.  Il confronto di <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> viene eseguito senza distinzione tra maiuscole e minuscole.  
  
 Se un tipo non dispone dell'attributo <xref:System.Runtime.InteropServices.TypeIdentifierAttribute>, o se dispone di un attributo <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> che non specifica l'ambito e l'identificatore, può ancora essere considerato per l'equivalenza come segue:  
  
-   Per le interfacce, il valore di <xref:System.Runtime.InteropServices.GuidAttribute> viene utilizzato al posto della proprietà <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A?displayProperty=fullName>, mentre la proprietà <xref:System.Type.FullName%2A?displayProperty=fullName> \(vale a dire il nome del tipo, incluso lo spazio dei nomi\) viene utilizzata al posto della proprietà <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A?displayProperty=fullName>.  
  
-   Per le strutture, le enumerazioni e i delegati, l'oggetto <xref:System.Runtime.InteropServices.GuidAttribute> dell'assembly contenitore viene utilizzato al posto della proprietà <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A>, mentre la proprietà <xref:System.Type.FullName%2A?displayProperty=fullName> viene utilizzata al posto della proprietà <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A>.  
  
<a name="type_equiv"></a>   
### Contrassegno dei tipi COM per l'equivalenza del tipo  
 Esistono due modi per contrassegnare un tipo come idoneo per l'equivalenza del tipo:  
  
-   Applicare l'attributo <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> al tipo.  
  
-   Rendere il tipo un tipo di importazione COM.  Un'interfaccia è un tipo di importazione COM se dispone dell'attributo <xref:System.Runtime.InteropServices.ComImportAttribute>.  Un'interfaccia, una struttura, un'enumerazione o un delegato è un tipo di importazione COM se l'assembly nel quale è definito dispone dell'attributo <xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute>.  
  
## Vedere anche  
 <xref:System.Type.IsEquivalentTo%2A>   
 [Using COM Types in Managed Code](http://msdn.microsoft.com/it-it/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66)   
 [Importing a Type Library as an Assembly](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)
---
title: "Blittable and Non-Blittable Types | Microsoft Docs"
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
  - "interop marshaling, blittable types"
  - "blittable types, interop marshaling"
ms.assetid: d03b050e-2916-49a0-99ba-f19316e5c1b3
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# Blittable and Non-Blittable Types
La maggior parte dei tipi di dati ha una rappresentazione comune sia nella memoria gestita che in quella non gestita e non richiede quindi una gestione particolare tramite il gestore di marshalling di interoperabilità.  Questi tipi sono denominati *tipi copiabili*, in quanto non richiedono la conversione quando vengono passati tra codice gestito e non gestito.  
  
 Le strutture che vengono restituite dalle chiamate platform invoke devono essere tipi non copiabili.  Platform invoke non supporta le strutture non copiabili come tipi restituiti.  
  
 I tipi dello spazio dei nomi <xref:System> elencati di seguito sono copiabili:  
  
-   <xref:System.Byte?displayProperty=fullName>  
  
-   <xref:System.SByte?displayProperty=fullName>  
  
-   <xref:System.Int16?displayProperty=fullName>  
  
-   <xref:System.UInt16?displayProperty=fullName>  
  
-   <xref:System.Int32?displayProperty=fullName>  
  
-   <xref:System.UInt32?displayProperty=fullName>  
  
-   <xref:System.Int64?displayProperty=fullName>  
  
-   <xref:System.UInt64?displayProperty=fullName>  
  
-   <xref:System.IntPtr?displayProperty=fullName>  
  
-   <xref:System.UIntPtr?displayProperty=fullName>  
  
-   <xref:System.Single?displayProperty=fullName>  
  
-   <xref:System.Double?displayProperty=fullName>  
  
 Anche i seguenti tipi complessi sono copiabili:  
  
-   Matrici unidimensionali di tipi copiabili, come una matrice di interi.  Un tipo contenente una matrice variabile di tipi copiabili tuttavia non è copiabile.  
  
-   Tipi di valore formattati contenenti solo tipi copiabili \(e classi se sottoposti a marshalling come tipi formattati\).  Per ulteriori informazioni sui tipi di valore formattati, vedere [Default Marshaling for Value Types](http://msdn.microsoft.com/it-it/4d9a876c-e05a-40ba-bd85-bd22877f984a).  
  
 I riferimenti a oggetti non sono copiabili,  incluse le matrici di riferimenti a oggetti, i quali invece sono copiabili.  È ad esempio possibile definire una struttura copiabile, ma non un tipo copiabile contenente una matrice di riferimenti a tali strutture.  
  
 Per ragioni di ottimizzazione, le matrici di tipi e classi copiabili contenenti solo membri copiabili vengono [bloccate](../../../docs/framework/interop/copying-and-pinning.md) e non copiate durante il marshalling.  Quando il chiamante e il chiamato si trovano nello stesso apartment, può sembrare che il marshalling di questi tipi venga eseguito come parametri In\/Out.  In realtà, il marshalling di questi tipi viene eseguito come parametri in ed è necessario applicare gli attributi <xref:System.Runtime.InteropServices.InAttribute> e <xref:System.Runtime.InteropServices.OutAttribute> se si desidera eseguire il marshalling dell'argomento come parametro in\/out.  
  
 Alcuni tipi di dati gestiti richiedono una rappresentazione diversa in un ambiente non gestito.  Questi tipi di dati non copiabili devono essere convertiti in un formato di cui è possibile eseguire il marshalling.  Le stringhe gestite, ad esempio, sono tipi non copiabili perché devono essere convertite in oggetti stringa prima di poter eseguire il marshalling.  
  
 Nella tabella riportata di seguito sono elencati i tipi non copiabili dello spazio dei nomi <xref:System>.  Anche i [delegati](http://msdn.microsoft.com/it-it/d176ee76-f982-494b-b03d-92e4118896e2), ossia le strutture di dati che fanno riferimento a un metodo statico o a un'istanza di classe, non sono copiabili.  
  
|Tipo non copiabile|Descrizione|  
|------------------------|-----------------|  
|[System.Array](../../../docs/framework/interop/default-marshaling-for-arrays.md)|Viene convertito in una matrice di tipo C o in `SAFEARRAY`.|  
|[System.Boolean](http://msdn.microsoft.com/it-it/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)|Viene convertito in un valore a 1, 2 o 4 byte con `true` pari a 1 o \-1.|  
|[System.Char](http://msdn.microsoft.com/it-it/cecc87c1-075e-4cde-aa56-33d189f66feb)|Viene convertito in un carattere Unicode o ANSI.|  
|[System.Class](http://msdn.microsoft.com/it-it/fe334af5-0123-43d8-be84-26f6f023ddb6)|Viene convertito in un'interfaccia di classe.|  
|[System.Object](../../../docs/framework/interop/default-marshaling-for-objects.md)|Viene convertito in un variant o in un'interfaccia.|  
|[System.Mdarray](../../../docs/framework/interop/default-marshaling-for-arrays.md)|Viene convertito in una matrice di tipo C o in `SAFEARRAY`.|  
|[System.String](../../../docs/framework/interop/default-marshaling-for-strings.md)|Viene convertito in una stringa che termina con un riferimento Null o un BSTR.|  
|[System.Valuetype](http://msdn.microsoft.com/it-it/4d9a876c-e05a-40ba-bd85-bd22877f984a)|Viene convertito in una struttura con un layout a memoria fissa.|  
|[System.Szarray](../../../docs/framework/interop/default-marshaling-for-arrays.md)|Viene convertito in una matrice di tipo C o in `SAFEARRAY`.|  
  
 I tipi di classe e oggetto sono supportati solo dall'interoperabilità COM.  Per i tipi corrispondenti in [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C\# e C\+\+, vedere [Cenni preliminari sulla libreria di classi](../../../docs/standard/class-library-overview.md).  
  
## Vedere anche  
 [Default Marshaling Behavior](../../../docs/framework/interop/default-marshaling-behavior.md)
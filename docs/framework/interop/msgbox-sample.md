---
title: "MsgBox Sample | Microsoft Docs"
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
  - "marshaling, MsgBox sample"
  - "data marshaling, MsgBox sample"
ms.assetid: 9e0edff6-cc0d-4d5c-a445-aecf283d9c3a
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# MsgBox Sample
Nell'esempio viene illustrato come passare i tipi stringa per valore come parametri in e quando utilizzare i campi <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>, <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> ed <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>.  
  
 Nell'esempio di MsgBox viene utilizzata la seguente funzione non gestita, illustrata con la dichiarazione di funzione originale:  
  
-   **MessageBox** esportata da User32.dll.  
  
    ```  
    int MessageBox(HWND hWnd, LPCTSTR lpText, LPCTSTR lpCaption,   
       UINT uType);  
    ```  
  
 In questo esempio, la classe `LibWrap` contiene un prototipo gestito per ciascuna funzione non gestita chiamata dalla classe `MsgBoxSample`.  I metodi del prototipo gestito `MsgBox`, `MsgBox2` e `MsgBox3` hanno dichiarazioni diverse per la stessa funzione non gestita.  
  
 La dichiarazione per `MsgBox2` produce output errato nella finestra di messaggio poiché il tipo di carattere, specificato come ANSI, non corrisponde alla funzione `MessageBoxW` del punto di ingresso, il cui nome è Unicode.  La dichiarazione per `MsgBox3` genera una mancata corrispondenza tra i campi **EntryPoint**, **CharSet** ed **ExactSpelling**.  Quando viene chiamato, `MsgBox3` genera un'eccezione.  Per informazioni dettagliate sulla denominazione delle stringhe e il marshalling dei nomi, vedere [Specifica di un set di caratteri](../../../docs/framework/interop/specifying-a-character-set.md).  
  
## Dichiarazione dei prototipi  
 [!code-cpp[Conceptual.Interop.Marshaling#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/msgbox.cpp#5)]
 [!code-csharp[Conceptual.Interop.Marshaling#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/msgbox.cs#5)]
 [!code-vb[Conceptual.Interop.Marshaling#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/msgbox.vb#5)]  
  
## Chiamata delle funzioni  
 [!code-cpp[Conceptual.Interop.Marshaling#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/msgbox.cpp#6)]
 [!code-csharp[Conceptual.Interop.Marshaling#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/msgbox.cs#6)]
 [!code-vb[Conceptual.Interop.Marshaling#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/msgbox.vb#6)]  
  
## Vedere anche  
 [Marshaling Strings](../../../docs/framework/interop/marshaling-strings.md)   
 [Platform Invoke Data Types](http://msdn.microsoft.com/it-it/16014d9f-d6bd-481e-83f0-df11377c550f)   
 [Default Marshaling for Strings](../../../docs/framework/interop/default-marshaling-for-strings.md)   
 [Creating Prototypes in Managed Code](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [Specifica di un set di caratteri](../../../docs/framework/interop/specifying-a-character-set.md)
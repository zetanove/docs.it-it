---
title: "Late bound resolution; runtime errors could occur | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42017"
  - "BC42017"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42017"
ms.assetid: 45f552c8-57c6-44c0-97d3-e510119b257a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Late bound resolution; runtime errors could occur
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un oggetto è assegnato a una variabile dichiarata di tipo [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md).  
  
 Quando si dichiara una variabile di tipo `Object`, è necessario che il compilatore esegua l'*associazione tardiva* che determina operazioni supplementari in fase di esecuzione.  L'applicazione viene anche esposta a possibili errori in fase di esecuzione.  Se, ad esempio, si assegna un oggetto <xref:System.Windows.Forms.Form> alla variabile `Object` e si tenta di accedere alla proprietà <xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=fullName>, il runtime genera un'eccezione <xref:System.MemberAccessException> perché la classe <xref:System.Windows.Forms.Form> non espone una proprietà `NameTable`.  
  
 Se si dichiara una variabile di tipo specifico, il compilatore può eseguire un'*associazione anticipata* in fase di compilazione.  Questo determina un miglioramento delle prestazioni, il controllo dell'accesso ai membri del tipo specificato e una maggiore leggibilità del codice.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42017  
  
### Per correggere l'errore  
  
-   Se è possibile, dichiarare il tipo specifico della variabile.  
  
## Vedere anche  
 [Early and Late Binding](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)   
 [Object Variable Declaration](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
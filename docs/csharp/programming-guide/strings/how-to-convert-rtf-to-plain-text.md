---
title: "Procedura: Convertire il formato RTF in testo normale (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "stringhe [C#], conversione da RTF"
ms.assetid: 3b386a87-899d-4d98-bc82-a980526ddaac
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: Convertire il formato RTF in testo normale (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Rich Text Format \(RTF\) è un formato di documento sviluppato da Microsoft negli ultimi anni Ottanta per consentire lo scambio di documenti tra sistemi operativi.  È possibile leggere e scrivere documenti RTF sia in Microsoft Word sia in WordPad.  In .NET Framework, è possibile utilizzare il controllo <xref:System.Windows.Forms.RichTextBox> per creare un elaboratore di testo che supporti il formato RTF e consenta di applicare formattazione al testo in modalità WYSIWIG.  
  
 È inoltre possibile utilizzare il controllo <xref:System.Windows.Forms.RichTextBox> per rimuovere a livello di codice i codici di formattazione RTF da un documento e convertirlo in testo normale.  Non è necessario incorporare il controllo in un Windows Form per eseguire questo tipo di operazione.  
  
### Per utilizzare il controllo RichTextBox in un progetto  
  
1.  Aggiungere un riferimento a System.Windows.Forms.dll.  
  
2.  Aggiungere una direttiva using per lo spazio dei nomi `System.Windows.Forms` \(facoltativo\).  
  
## Esempio  
 L'esempio seguente consente di convertire un file RTF di esempio in testo normale.  Il file contiene formattazione RTF quali le informazioni di carattere\), quattro caratteri unicode e quattro caratteri ASCII estesi.  Il codice di esempio viene aperto il file, passa il contenuto a <xref:System.Windows.Forms.RichTextBox> come RTF, recupera il contenuto come testo, visualizzare il testo in <xref:System.Windows.Forms.MessageBox>e restituisce il testo in un file in formato UTF\-8.  
  
 `MessageBox` e il file di output contengono il testo seguente:  
  
```  
The Greek word for "psyche" is spelled ψυχή. The Greek letters are encoded in Unicode.  
These characters are from the extended ASCII character set (Windows code page 1252):  âäӑå  
  
```  
  
 [!code-cs[csProgGuideStrings#33](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-rtf-to-plain-text_1.cs)]  
  
 I caratteri RTF sono codificati in otto bit.  Tuttavia, gli utenti possono specificare i caratteri unicode oltre ai caratteri ASCII estesi dalle tabelle codici specificate.  Poiché la proprietà <xref:System.Windows.Forms.RichTextBox.Text%2A?displayProperty=fullName> è di tipo [stringa](../../../csharp/language-reference/keywords/string.md), i caratteri sono codificati come Unicode UTF\-16.  Tutti i caratteri ASCII estesi e i caratteri Unicode del documento RTF di origine vengono codificati correttamente nell'output di testo.  
  
 Se si utilizza il metodo <xref:System.IO.File.WriteAllText%2A?displayProperty=fullName> per scrivere il testo su disco, il testo sarà codificato come UTF\-8 \(senza un indicatore per l'ordine dei byte\).  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox?displayProperty=fullName>   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)
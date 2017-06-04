---
title: "Procedura: utilizzare caratteri speciali in XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "caratteri, speciali"
  - "caratteri speciali"
  - "tipografia, caratteri speciali"
  - "Unicode UTF-8 (formato file)"
  - "UTF-8 (formato file)"
ms.assetid: a57776d1-f353-4794-afa0-bfa3c712ed1c
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# Procedura: utilizzare caratteri speciali in XAML
I file di markup creati in [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] vengono salvati automaticamente nel formato di file UTF\-8 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)], ovvero la maggior parte dei caratteri speciali, ad esempio gli accenti, sono codificati correttamente.  Tuttavia, un set di caratteri speciali di utilizzo comune viene gestito diversamente.  Questi caratteri speciali seguono lo standard [!INCLUDE[TLA#tla_w3c](../../../../includes/tlasharptla-w3c-md.md)] [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] per la codifica.  
  
 Nella tabella seguente è illustrata la sintassi per la codifica di questo set di caratteri speciali:  
  
|Carattere|Sintassi|Descrizione|  
|---------------|--------------|-----------------|  
|\<|`<`|Simbolo minore di.|  
|\>|`>`|Simbolo maggiore di.|  
|&|`&`|Simbolo e commerciale.|  
||`"`|Simbolo virgoletta doppia.|  
  
> [!NOTE]
>  Se si crea un file di markup utilizzando un editor di testo, ad esempio Blocco note di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)], è necessario salvare il file nel formato di file UTF\-8 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] per mantenere i caratteri speciali codificati.  
  
 Nell'esempio riportato di seguito viene illustrato come utilizzare i caratteri speciali nel testo durante la creazione del markup.  
  
## Esempio  
 [!code-xml[SpecialCharsSnippets#SpecialCharsSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpecialCharsSnippets/CS/Window1.xaml#specialcharssnippet1)]
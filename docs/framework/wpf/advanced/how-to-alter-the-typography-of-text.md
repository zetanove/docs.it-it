---
title: "Procedura: modificare le opzioni tipografiche del testo | Microsoft Docs"
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
  - "impostazione di attributi tipografici"
  - "attributi tipografici, impostazione"
ms.assetid: 19a3b49b-60a2-4c11-a786-e26b4c965588
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# Procedura: modificare le opzioni tipografiche del testo
Nell'esempio riportato di seguito viene illustrato come impostare l'attributo <xref:System.Windows.Documents.TextElement.Typography%2A>, utilizzando <xref:System.Windows.Documents.Paragraph> come elemento di esempio.  
  
## Esempio  
 [!code-xml[TextElementSnippets#_TextElement_TypogXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]  
  
 Nella figura riportata di seguito viene illustrato il rendering di questo esempio.  
  
 ![Schermata: testo con tipografia modificata](../../../../docs/framework/wpf/advanced/media/textelement-typog.png "TextElement\_Typog")  
  
 Per contro, la figura seguente mostra come viene eseguito il rendering di tale esempio con le proprietà tipografiche predefinite.  
  
 ![Schermata: testo con tipografia modificata](../../../../docs/framework/wpf/advanced/media/textelement-typog-default.png "TextElement\_Typog\_Default")  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come impostare la proprietà <xref:System.Windows.Controls.TextBox.Typography%2A> a livello di codice.  
  
 [!code-csharp[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
 [!code-vb[TextElementSnippets#_TextElement_Typog](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]  
  
## Vedere anche  
 [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)
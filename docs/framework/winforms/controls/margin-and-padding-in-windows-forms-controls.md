---
title: "Margini e spaziatura nei controlli Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "layout [Windows Form], margini e riempimento"
  - "Margin (proprietà) [Windows Form]"
  - "Padding (proprietà) [Windows Form]"
  - "Windows Form, layout"
ms.assetid: 3781b5a1-3085-4072-bed0-44670c23ffdc
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Margini e spaziatura nei controlli Windows Form
Per molte applicazioni è estremamente importante la sistemazione precisa dei controlli nel form.  A tale scopo, lo spazio dei nomi <xref:System.Windows.Forms?displayProperty=fullName> offre diversi strumenti di layout.  Due tra le più importanti sono le proprietà <xref:System.Windows.Forms.Control.Margin%2A> e <xref:System.Windows.Forms.Control.Padding%2A>.  
  
 La proprietà <xref:System.Windows.Forms.Control.Margin%2A> definisce lo spazio intorno al controllo per mantenere gli altri controlli a una specifica distanza dai bordi del controllo stesso.  
  
 La proprietà <xref:System.Windows.Forms.Control.Padding%2A> definisce lo spazio all'interno di un controllo per mantenere il contenuto del controllo, ad esempio il valore della proprietà <xref:System.Windows.Forms.Control.Text%2A>, a una specifica distanza dai bordi del controllo stesso.  
  
 L'illustrazione seguente mostra le proprietà <xref:System.Windows.Forms.Control.Padding%2A> e <xref:System.Windows.Forms.Control.Margin%2A> in un controllo.  
  
 ![Spaziatura e margine per controlli Windows Form](../../../../docs/framework/winforms/controls/media/vs-winformpadmargin.gif "VS\_WinFormPadMargin")  
  
 È disponibile supporto in fase di progettazione per questa funzionalità in Visual Studio.  Vedere anche [Procedura dettagliata: Disposizione di controlli Windows Form usando spaziatura, margini e la proprietà AutoSize](http://msdn.microsoft.com/library/3z3f9e8b\(v=vs.110\))  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.AutoSize%2A>   
 <xref:System.Windows.Forms.Control.Margin%2A>   
 <xref:System.Windows.Forms.Control.Padding%2A>   
 <xref:System.Windows.Forms.Control.LayoutEngine%2A>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 <xref:System.Windows.Forms.FlowLayoutPanel>
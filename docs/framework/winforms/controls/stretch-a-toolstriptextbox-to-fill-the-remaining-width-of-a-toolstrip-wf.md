---
title: "Procedura: allargare un oggetto ToolStripTextBox in modo da coprire tutta la larghezza di un elemento ToolStrip (Windows Form) | Microsoft Docs"
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
  - "caselle di testo, adattamento nel controllo ToolStrip [Windows Form]"
  - "ToolStrip (controllo) [Windows Form], adattamento di una casella di testo"
ms.assetid: 0e610fbf-85fe-414c-900c-9704a5dd5cc6
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: allargare un oggetto ToolStripTextBox in modo da coprire tutta la larghezza di un elemento ToolStrip (Windows Form)
Quando si imposta la proprietà <xref:System.Windows.Forms.ToolStrip.Stretch%2A> di un controllo <xref:System.Windows.Forms.ToolStrip> su `true`, il controllo occupa il proprio contenitore da un'estremità all'altra e si ridimensiona quando il contenitore si ridimensiona.  In questa configurazione può risultare utile allargare un elemento in un controllo, ad esempio <xref:System.Windows.Forms.ToolStripTextBox>, per occupare lo spazio disponibile e ridimensionarlo quando il controllo si ridimensiona.  Questa soluzione è utile, ad esempio, se si desidera ottenere un aspetto e un comportamento simili a quelli della barra degli indirizzi in Microsoft® Internet Explorer.  
  
## Esempio  
 Nell'esempio di codice seguente viene fornita una classe derivata da <xref:System.Windows.Forms.ToolStripTextBox> denominata `ToolStripSpringTextBox`.  Questa classe esegue l'override del metodo <xref:System.Windows.Forms.ToolStripTextBox.GetPreferredSize%2A> per calcolare la larghezza disponibile del controllo <xref:System.Windows.Forms.ToolStrip> padre dopo che è stata sottratta la larghezza combinata di tutti gli altri elementi.  Vengono inoltre fornite una classe <xref:System.Windows.Forms.Form> e una classe `Program` per illustrare il nuovo comportamento.  
  
 [!code-csharp[ToolStripSpringTextBox#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripSpringTextBox/cs/ToolStripSpringTextBox.cs#00)]
 [!code-vb[ToolStripSpringTextBox#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripSpringTextBox/vb/ToolStripSpringTextBox.vb#00)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStrip.Stretch%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripTextBox>   
 <xref:System.Windows.Forms.ToolStripTextBox.GetPreferredSize%2A?displayProperty=fullName>   
 [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [Procedura: utilizzare la proprietà Spring in modo interattivo in StatusStrip](../../../../docs/framework/winforms/controls/how-to-use-the-spring-property-interactively-in-a-statusstrip.md)
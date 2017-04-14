---
title: "Procedura: ridimensionare un controllo Label Windows Form in base al contenuto | Microsoft Docs"
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
  - "didascalie, ridimensionamento"
  - "Label (controllo) [Windows Form], adattamento al contenuto"
  - "etichette, adattamento al contenuto"
  - "dimensione, controlli"
  - "ridimensionamento dei controlli"
ms.assetid: 99648964-63b2-438c-980e-d24103ad602b
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: ridimensionare un controllo Label Windows Form in base al contenuto
Il controllo <xref:System.Windows.Forms.Label> Windows Form può essere a riga singola o a più righe, di dimensioni fisse oppure ridimensionabile automaticamente in base alla lunghezza della didascalia.  La proprietà <xref:System.Windows.Forms.Label.AutoSize%2A> consente di ridimensionare i controlli in modo che possano contenere didascalie di dimensioni variabili. Ciò risulta particolarmente utile se la didascalia subisce modifiche in fase di esecuzione.  
  
### Per consentire il ridimensionamento dinamico di un'etichetta per contenere la didascalia  
  
1.  Impostarne la proprietà <xref:System.Windows.Forms.Label.AutoSize%2A> su `true`.  
  
 Se la proprietà <xref:System.Windows.Forms.Label.AutoSize%2A> è impostata su `false`, le parole indicate nella proprietà <xref:System.Windows.Forms.Label.Text%2A> vanno a capo nella riga successiva, se possibile, ma le dimensioni del controllo non possono aumentare.  
  
## Vedere anche  
 [Procedura: creare tasti di scelta con i controlli Label di Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md)   
 [Cenni preliminari sul controllo Label](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)   
 [Controllo Label](../../../../docs/framework/winforms/controls/label-control-windows-forms.md)
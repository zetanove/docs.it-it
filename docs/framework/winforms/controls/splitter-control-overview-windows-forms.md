---
title: "Cenni preliminari sul controllo Splitter (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Splitter"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Splitter (controllo) [Windows Form], informazioni sul controllo Splitter"
ms.assetid: e2b6ab83-dfdd-40ec-9762-850702c82dcb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari sul controllo Splitter (Windows Form)
> [!IMPORTANT]
>  Benché il controllo <xref:System.Windows.Forms.SplitContainer> sostituisca il controllo <xref:System.Windows.Forms.Splitter> delle versioni precedenti aggiungendo funzionalità, il controllo <xref:System.Windows.Forms.Splitter> viene mantenuto per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
 I controlli <xref:System.Windows.Forms.Splitter> di Windows Form vengono utilizzati in fase di esecuzione per ridimensionare i controlli ancorati.  Il controllo <xref:System.Windows.Forms.Splitter> viene spesso utilizzato in form con controlli che devono presentare dati di lunghezza variabile, ad esempio in Esplora risorse, i cui riquadri contengono informazioni la cui lunghezza può cambiare in momenti diversi.  
  
## Utilizzo del controllo Splitter  
 Quando si posiziona il puntatore del mouse in corrispondenza del bordo non ancorato di un controllo che può essere ridimensionato con un controllo Splitter, l'aspetto del puntatore cambia per indicare che il controllo può essere ridimensionato.  Il controllo Splitter consente all'utente di ridimensionare il controllo ancorato immediatamente precedente.  Per consentire all'utente di ridimensionare un controllo ancorato in fase di esecuzione è quindi necessario ancorare il controllo da ridimensionare al bordo di un contenitore, quindi ancorare un controllo Splitter sullo stesso lato del contenitore.  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 [Procedura: ancorare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)
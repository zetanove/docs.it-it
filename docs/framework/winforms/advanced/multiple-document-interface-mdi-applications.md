---
title: "Applicazioni MDI (Interfaccia a documenti multipli, Multiple-Document Interface) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "form, MDI"
  - "MDI"
  - "Windows Form, MDI (applicazioni)"
  - "finestre, MDI"
ms.assetid: 599faf75-13cf-49cc-ad3c-255545e5cb97
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Applicazioni MDI (Interfaccia a documenti multipli, Multiple-Document Interface)
Le applicazioni con interfaccia a documenti multipli \(MDI, Multiple Document Interface\) consentono di visualizzare contemporaneamente più documenti, ciascuno in una finestra.  Nelle applicazioni MDI è spesso presente una voce del menu Finestra con sottomenu per passare da una finestra all'altra o da un documento all'altro.  
  
> [!NOTE]
>  Esistono alcune differenze di comportamento tra form MDI e finestre SDI \(Single Document Interface\) in Windows Form.  La proprietà `Opacity` non incide sull'aspetto dei form figlio MDI  e il metodo <xref:System.Windows.Forms.Form.CenterToParent%2A> non incide sul loro comportamento.  
  
## In questa sezione  
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)  
 Vengono fornite indicazioni per creare il contenitore di documenti multipli all'interno di un'applicazione MDI.  
  
 [Procedura: creare form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)  
 Vengono fornite indicazioni per creare una o più finestre che funzionano all'interno di un form padre MDI.  
  
 [Procedura: determinare il figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)  
 Vengono fornite indicazioni per verificare quale finestra figlio detiene lo stato attivo e per inviarne il contenuto agli Appunti.  
  
 [Procedura: inviare dati al figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)  
 Vengono fornite indicazioni per trasferire le informazioni alla finestra figlio attiva.  
  
 [Procedura: disporre i form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)  
 Vengono fornite indicazioni per affiancare, sovrapporre o disporre le finestre figlio di un'applicazione MDI.
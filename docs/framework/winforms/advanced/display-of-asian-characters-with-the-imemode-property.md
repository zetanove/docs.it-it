---
title: "Display of Asian Characters with the ImeMode Property | Microsoft Docs"
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
  - "Asian languages, displaying with ImeMode"
  - "Chinese characters, displaying with ImeMode"
  - "IME mode"
  - "Japanese characters, displaying with ImeMode"
  - "international applications [Windows Forms], character display"
  - "international characters"
  - "Korean characters"
  - "Asian languages"
  - "Input Method Editor (IME), mode"
  - "localization [Windows Forms], character sets"
  - "IMEMode property"
  - "globalization [Windows Forms], character sets"
ms.assetid: c60ae399-0dab-4f07-9dea-6dbfb15ec0ae
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Display of Asian Characters with the ImeMode Property
La proprietà <xref:System.Windows.Forms.Control.ImeMode%2A> viene utilizzata dai form e dai controlli per imporre una specifica modalità relativa a un editor del metodo di input \(IME, Input Method Editor\).  L'IME è un componente fondamentale per la creazione di script in lingua cinese, giapponese e coreana, poiché si tratta di sistemi di scrittura con più caratteri di quelli che possono essere codificati per una tastiera standard.  È ad esempio possibile consentire l'immissione soltanto di caratteri ASCII in una particolare casella di testo.  In tal caso è possibile impostare la proprietà <xref:System.Windows.Forms.Control.ImeMode%2A> su <xref:System.Windows.Forms.ImeMode>, in modo che gli utenti possano immettere nella casella di testo soltanto caratteri ASCII.  Il valore predefinito della proprietà <xref:System.Windows.Forms.Control.ImeMode%2A> è <xref:System.Windows.Forms.ImeMode>. Di conseguenza, se si imposta la proprietà per un form, tutti i controlli nel form erediteranno tale impostazione.  Per ulteriori informazioni, vedere [Proprietà Control.ImeMode](frlrfSystemWindowsFormsControlClassImeModeTopic) ed [Enumerazione ImeMode](frlrfSystemWindowsFormsImeModeClassTopic).  
  
## Vedere anche  
 [Globalizing Windows Forms](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)
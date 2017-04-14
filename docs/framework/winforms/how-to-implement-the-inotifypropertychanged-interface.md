---
title: "Procedura: implementare l&#39;interfaccia INotifyPropertyChanged | Microsoft Docs"
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
  - "INotifyPropertyChanged (interfaccia), implementazione"
ms.assetid: eac428af-b43b-46ac-80d9-1a5f88658725
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: implementare l&#39;interfaccia INotifyPropertyChanged
Nell'esempio di codice riportato di seguito viene illustrato come implementare l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  Implementare questa interfaccia negli oggetti business utilizzati nell'associazione dati dei Windows Form.  Se implementata, l'interfaccia consente di comunicare a un controllo associato le modifiche delle proprietà in un oggetto business.  
  
## Esempio  
 [!code-csharp[System.ComponentModel.IPropertyChangeExample#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.IPropertyChangeExample#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/VB/Form1.vb#1)]  
  
## Vedere anche  
 [Procedura: applicare il modello PropertyNameChanged](../../../docs/framework/winforms/how-to-apply-the-propertynamechanged-pattern.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Procedura: generare notifiche di modifica utilizzando un BindingSource e l'interfaccia INotifyPropertyChanged](../../../docs/framework/winforms/controls/raise-change-notifications--bindingsource.md)   
 [Notifica delle modifiche nell'associazione dati dei Windows Form](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)
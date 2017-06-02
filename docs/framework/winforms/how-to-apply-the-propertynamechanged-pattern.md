---
title: "Procedura: applicare il modello PropertyNameChanged | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], modifica delle proprietà (mediante il codice)"
  - "associazione dati, controlli personalizzati"
  - "PropertyNameChanged (modello), applicazione"
ms.assetid: aa47ddf6-5223-40c4-833f-a78992194836
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: applicare il modello PropertyNameChanged
Nell'esempio di codice seguente viene illustrato come applicare il modello *NomeProprietà*Changed a un controllo personalizzato.  Applicare questo modello quando si implementano i controlli personalizzati utilizzati con il modulo di associazione dati di Windows Form.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.ChangeNotification#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ChangeNotification/CS/Form1.cs#3)]
 [!code-vb[System.Windows.Forms.ChangeNotification#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ChangeNotification/VB/Form1.vb#3)]  
  
## Compilazione del codice  
 Per compilare l'esempio di codice precedente:  
  
-   Incollare il codice in un file di codice vuoto.  È necessario utilizzare il controllo personalizzato in un Windows Form contenente un metodo `Main`.  
  
## Vedere anche  
 [Procedura: implementare l'interfaccia INotifyPropertyChanged](../../../docs/framework/winforms/how-to-implement-the-inotifypropertychanged-interface.md)   
 [Notifica delle modifiche nell'associazione dati dei Windows Form](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)
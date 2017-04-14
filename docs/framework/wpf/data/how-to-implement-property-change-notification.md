---
title: "Procedura: implementare notifiche di modifiche alle propriet&#224; | Microsoft Docs"
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
  - "notifiche di modifica"
  - "associazione dati, notifiche delle modifiche alle proprietà"
  - "notifiche di modifica"
  - "proprietà, notifiche di modifica"
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: implementare notifiche di modifiche alle propriet&#224;
Per supportare l'associazione <xref:System.Windows.Data.BindingMode> o <xref:System.Windows.Data.BindingMode> in modo che le proprietà della [destinazione dell'associazione](GTMT) riflettano automaticamente le modifiche dinamiche dell'[origine dell'associazione](GTMT) \(ad esempio per indurre l'aggiornamento automatico del riquadro anteprima quando un utente modifica un form\), la classe deve fornire le notifiche di proprietà modificata appropriate.  In questo esempio viene illustrato come creare una classe che implementa <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
## Esempio  
 Per implementare <xref:System.ComponentModel.INotifyPropertyChanged>, è necessario dichiarare l'evento <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> e creare il metodo `OnPropertyChanged`.  Per ogni proprietà per la quale si desidera fornire una notifica di modifica, chiamare `OnPropertyChanged` ogni volta che la proprietà viene aggiornata.  
  
 [!code-csharp[SimpleBinding#PersonClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 Per un esempio di utilizzo della classe `Person` per supportare l'associazione <xref:System.Windows.Data.BindingMode>, vedere [Controllare il momento in cui il database di origine viene aggiornato dal testo di TextBox](../../../../docs/framework/wpf/data/how-to-control-when-the-textbox-text-updates-the-source.md).  
  
## Vedere anche  
 [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
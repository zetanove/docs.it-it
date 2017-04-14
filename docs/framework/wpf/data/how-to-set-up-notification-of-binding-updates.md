---
title: "Procedura: impostare notifiche relative ad aggiornamenti di associazioni | Microsoft Docs"
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
  - "associazione, aggiornamenti, notifiche"
  - "associazione dati, notifiche relative ad aggiornamenti di associazioni"
  - "notifiche, aggiornamenti di associazioni"
ms.assetid: 5673073e-dbe1-49da-980a-484a88f9595a
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare notifiche relative ad aggiornamenti di associazioni
In questo esempio vengono illustrate le impostazioni necessarie per ricevere notifiche al momento dell'aggiornamento della proprietà di [destinazione di associazione](GTMT) \(destinazione\) o [origine di associazione](GTMT) \(origine\) di un'associazione.  
  
## Esempio  
 In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] viene generato un evento di aggiornamento dati ogni volta che l'origine o la destinazione di associazione viene aggiornata.  Internamente, questo evento viene utilizzato per comunicare all'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] la necessità di aggiornamento, poiché i dati associati sono stati modificati.  Si noti che, per il corretto funzionamento di questi eventi e anche dell'associazione unidirezionale o bidirezionale, è necessario implementare la classe di dati utilizzando l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  Per ulteriori informazioni, vedere [Implementare la notifica di modifiche alle proprietà](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md).  
  
 Impostare la proprietà <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A> o <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A> \(o entrambe\) su `true` nell'associazione.  Il gestore fornito per restare in ascolto di questo evento deve essere collegato direttamente all'elemento per il quale si desidera essere informati delle modifiche oppure al contesto di dati complessivo se si intende essere informati della modifica di qualsiasi elemento nel contesto.  
  
 Nell'esempio riportato di seguito vengono illustrate le impostazioni necessarie per ricevere la notifica dell’aggiornamento di una proprietà di destinazione.  
  
 [!code-xml[DirectionalBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#2)]  
  
 È quindi possibile assegnare un gestore basato sul delegato EventHandler\<T\>, *OnTargetUpdated* in questo esempio, per gestire l'evento:  
  
 [!code-csharp[DirectionalBinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml.cs#3)]  
[!code-csharp[DirectionalBinding#EndEvent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml.cs#endevent)]  
  
 I parametri dell'evento possono essere utilizzati per stabilire i dettagli relativi alla proprietà che è stata modificata \(ad esempio il tipo o l'elemento specifico se lo stesso gestore è collegato a più elementi\), funzionalità utile nel caso in cui vi siano più proprietà associate a un solo elemento.  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
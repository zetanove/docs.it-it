---
title: "Procedura: generare notifiche di modifica utilizzando un BindingSource e l&#39;interfaccia INotifyPropertyChanged | Microsoft Docs"
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
  - "BindingSource (componente) [Windows Form], e IPropertyChange"
  - "BindingSource (componente) [Windows Form], esempi"
  - "notifiche di modifica"
  - "notifiche di modifica, generazione"
  - "origini dati, rilevamento modifiche"
  - "esempi [Windows Form], BindingSource (componente)"
  - "INotifyPropertyChanged (interfaccia), utilizzo con BindingSource"
ms.assetid: 7fa2cf51-c09f-4375-adf0-e36c5617f099
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: generare notifiche di modifica utilizzando un BindingSource e l&#39;interfaccia INotifyPropertyChanged
Il componente <xref:System.Windows.Forms.BindingSource> rileva automaticamente le modifiche in un'origine dati quando il tipo contenuto nell'origine dati implementa l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> e genera eventi <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> nel momento in cui il valore di una proprietà viene modificato.  Si tratta di una caratteristica utile perché i controlli associati al componente <xref:System.Windows.Forms.BindingSource> verranno aggiornati automaticamente al variare dei valori dell'origine dati.  
  
> [!NOTE]
>  Se l'origine dati implementa <xref:System.ComponentModel.INotifyPropertyChanged> e devono essere eseguite operazioni asincrone, non devono essere apportate modifiche all'origine dati in un thread in background.  In alternativa, è possibile leggere i dati in un thread in background e quindi unire i dati in un elenco nel thread dell'interfaccia utente.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrata una semplice implementazione dell'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  Viene inoltre descritto il modo in cui il componente <xref:System.Windows.Forms.BindingSource> passa automaticamente una modifica dell'origine dati a un controllo associato quando <xref:System.Windows.Forms.BindingSource> è associato a un elenco di tipo <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
 Se si usa l'attributo `CallerMemberName`, le chiamate al metodo `NotifyPropertyChanged` non devono specificare il nome della proprietà come argomento di tipo stringa.  Per altre informazioni, vedere [Informazioni sul chiamante](../Topic/Caller%20Information%20\(C%23%20and%20Visual%20Basic\).md).  
  
 [!code-csharp[System.ComponentModel.IPropertyChangeExample#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.IPropertyChangeExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Data, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.ComponentModel.INotifyPropertyChanged>   
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Procedura: generare notifiche di modifica utilizzando il metodo ResetItem di BindingSource](../../../../docs/framework/winforms/controls/how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)
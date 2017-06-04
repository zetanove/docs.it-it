---
title: "Procedura: eseguire l&#39;associazione a un metodo | Microsoft Docs"
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
  - "associazione, metodi"
  - "classi, ObjectDataProvider"
  - "associazione dati, associazione a metodi utilizzando ObjectDataProvider"
  - "metodi, associazione a"
  - "ObjectDataProvider (classe)"
ms.assetid: 5f55e71e-2182-42a0-88d1-700cc1427a7a
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: eseguire l&#39;associazione a un metodo
Nell'esempio riportato di seguito viene illustrato come eseguire l'associazione a un metodo utilizzando <xref:System.Windows.Data.ObjectDataProvider>.  
  
## Esempio  
 In questo esempio, `TemperatureScale` è una classe che dispone di un metodo `ConvertTemp` che accetta due parametri \(uno `double` e uno del tipo `enum` `TempType)` e converte il valore specificato da una scala della temperatura a un'altra.  Nell'esempio riportato di seguito, un oggetto <xref:System.Windows.Data.ObjectDataProvider> viene utilizzato per creare un'istanza dell'oggetto `TemperatureScale`.  Il metodo `ConvertTemp` viene chiamato con due parametri specificati.  
  
 [!code-xml[BindToMethod#WindowResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToMethod/CS/Window1.xaml#windowresources)]  
  
 Ora che il metodo è disponibile come risorsa, è possibile eseguire l'associazione ai risultati.  Nell'esempio riportato di seguito, la proprietà <xref:System.Windows.Controls.TextBox.Text%2A> di <xref:System.Windows.Controls.TextBox> e la proprietà <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> di <xref:System.Windows.Controls.ComboBox> sono associate ai due parametri del metodo.  In questo modo è possibile consentire agli utenti di specificare la temperatura da convertire e la scala della temperatura da cui eseguire la conversione.  Si noti che la proprietà <xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A> è impostata su `true` poiché viene eseguita l'associazione alla proprietà <xref:System.Windows.Data.ObjectDataProvider.MethodParameters%2A> dell'istanza <xref:System.Windows.Data.ObjectDataProvider> e non alle proprietà dell'oggetto incapsulate da <xref:System.Windows.Data.ObjectDataProvider> \(oggetto `TemperatureScale` \).  
  
 La proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> dell'ultimo oggetto <xref:System.Windows.Controls.Label> viene aggiornata quando l'utente modifica il contenuto di <xref:System.Windows.Controls.TextBox> o la selezione di <xref:System.Windows.Controls.ComboBox>.  
  
 [!code-xml[BindToMethod#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToMethod/CS/Window1.xaml#ui)]  
  
 Il convertitore `DoubleToString` accetta un valore double, lo converte in una stringa nella direzione del metodo <xref:System.Windows.Data.IValueConverter.Convert%2A> \(dall'[origine di associazione](GTMT) alla [destinazione di associazione](GTMT), rappresentata dalla proprietà <xref:System.Windows.Controls.TextBox.Text%2A>\) e converte un valore `string` in un valore `double` nella direzione del metodo <xref:System.Windows.Data.IValueConverter.ConvertBack%2A>.  
  
 `InvalidationCharacterRule` è un oggetto <xref:System.Windows.Controls.ValidationRule> che verifica la presenza di caratteri non validi.  Il modello di errori predefinito, rappresentato da un bordo rosso intorno a <xref:System.Windows.Controls.TextBox>, viene visualizzato per notificare agli utenti i casi in cui il valore di input non è double.  
  
## Vedere anche  
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [Eseguire l'associazione a un'enumerazione](../../../../docs/framework/wpf/data/how-to-bind-to-an-enumeration.md)
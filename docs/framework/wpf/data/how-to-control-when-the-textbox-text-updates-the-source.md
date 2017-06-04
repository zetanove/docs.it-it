---
title: "Procedura: controllare il momento in cui il database di origine viene aggiornato dal testo di TextBox | Microsoft Docs"
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
  - "associazione dati, intervallo degli aggiornamento dell'origine"
  - "aggiornamenti dell'origine, intervallo"
  - "intervallo degli aggiornamento dell'origine"
ms.assetid: ffb7b96a-351d-4c68-81e7-054033781c64
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: controllare il momento in cui il database di origine viene aggiornato dal testo di TextBox
In questo argomento viene descritto come utilizzare la proprietà <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> per controllare l'intervallo degli aggiornamenti dell'[origine di associazione](GTMT).  Nell'argomento viene utilizzato il controllo <xref:System.Windows.Controls.TextBox> come esempio.  
  
## Esempio  
 La proprietà <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A> dispone di un valore predefinito <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> di <xref:System.Windows.Data.UpdateSourceTrigger>.  In altri termini, se un'applicazione dispone di un oggetto <xref:System.Windows.Controls.TextBox> con una proprietà con associazione a dati <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A>, il testo digitato in <xref:System.Windows.Controls.TextBox> non aggiorna l'origine finché l'oggetto <xref:System.Windows.Controls.TextBox> perde lo stato attivo \(ad esempio, quando si fa clic al di fuori di <xref:System.Windows.Controls.TextBox>\).  
  
 Se si desidera che il database di origine venga aggiornato durante la digitazione, impostare l'oggetto <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> dell'associazione su <xref:System.Windows.Data.UpdateSourceTrigger>.  Nell'esempio seguente, le proprietà `Text` di entrambi gli oggetti <xref:System.Windows.Controls.TextBox> e <xref:System.Windows.Controls.TextBlock> vengono associate alla stessa proprietà di origine.  La proprietà <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> dell'associazione <xref:System.Windows.Controls.TextBox> viene impostata su <xref:System.Windows.Data.UpdateSourceTrigger>.  
  
 [!code-xml[SimpleBinding#USTHowTo](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml#usthowto)]  
  
 Di conseguenza, poiché il database di origine cambia, l'oggetto <xref:System.Windows.Controls.TextBlock> mostra lo stesso testo digitato dall'utente in <xref:System.Windows.Controls.TextBox>, come illustrato nella schermata seguente dell'esempio:  
  
 ![Schermata dell'esempio Simple Data Binding](../../../../docs/framework/wpf/data/media/databindingsimplebindingsample2.png "DataBindingSimpleBindingSample2")  
  
 Se si dispone di una finestra di dialogo o di un modulo modificabile dall'utente e si preferisce rimandare gli aggiornamenti del database di origine finché l'utente non abbia finito di modificare i campi e faccia clic su "OK", è possibile impostare il valore <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> delle associazioni su <xref:System.Windows.Data.UpdateSourceTrigger>, come nell'esempio seguente:  
  
 [!code-xml[UpdateSource#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml#2)]  
  
 Quando il valore <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> viene impostato su <xref:System.Windows.Data.UpdateSourceTrigger>, il valore di origine cambia solo quando l'applicazione chiama il metodo <xref:System.Windows.Data.BindingExpression.UpdateSource%2A>.  Nell'esempio riportato di seguito viene illustrato come chiamare <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> per `itemNameTextBox`:  
  
 [!code-csharp[UpdateSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml.cs#1)]
 [!code-vb[UpdateSource#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UpdateSource/VisualBasic/Window1.xaml.vb#1)]  
  
> [!NOTE]
>  È possibile utilizzare la stessa tecnica per le proprietà di altri controlli, ma tenere presente che la maggior parte delle altre proprietà hanno un valore predefinito <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> di <xref:System.Windows.Data.UpdateSourceTrigger>.  Per ulteriori informazioni, vedere la pagina delle proprietà <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>.  
  
> [!NOTE]
>  La proprietà <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> è relativa agli aggiornamenti del database di origine e quindi si applica solo alle associazioni <xref:System.Windows.Data.BindingMode> o <xref:System.Windows.Data.BindingMode>.  Affinché le associazioni <xref:System.Windows.Data.BindingMode> e <xref:System.Windows.Data.BindingMode> funzionino, è necessario che l'oggetto di origine fornisca le notifiche di modifica della proprietà.  Per ulteriori informazioni, è possibile fare riferimento agli esempi citati in questo argomento.  Inoltre, è possibile consultare [Implementare la notifica di modifiche alle proprietà](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md).  
  
## Vedere anche  
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
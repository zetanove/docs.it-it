---
title: "Event Handlers Overview (Windows Forms) | Microsoft Docs"
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
  - "Windows Forms, event handling"
  - "event handling, Windows Forms"
  - "event handlers, about event handlers"
ms.assetid: 228112e1-1711-42ee-8ffa-ff3555bffe66
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Event Handlers Overview (Windows Forms)
Un gestore eventi è un metodo che viene associato a un evento.  Quando viene generato l'evento, viene anche eseguito il codice all'interno del gestore eventi.  Ciascun gestore eventi fornisce due parametri che consentono di gestire correttamente l'evento.  Nell'esempio che segue viene mostrato un gestore per l'evento <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button>.  
  
```vb  
Private Sub button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles button1.Click  
  
End Sub  
  
```  
  
```csharp  
private void button1_Click(object sender, System.EventArgs e)   
{  
  
}  
  
```  
  
```cpp  
private:  
  void button1_Click(System::Object ^ sender,  
    System::EventArgs ^ e)  
  {  
  
  }  
```  
  
 Il primo parametro,`sender`, fornisce un riferimento all'oggetto che ha generato l'evento.  Il secondo parametro, `e` nell'esempio sopra riportato, passa un oggetto specifico all'evento che viene gestito.  Facendo riferimento alle proprietà dell'oggetto ed eventualmente ai relativi metodi, è possibile recuperare informazioni quali la posizione del mouse per gli eventi del mouse o i dati che vengono trasferiti durante gli eventi di trascinamento.  
  
 Ogni evento produce in genere un gestore eventi con un diverso tipo di oggetto dell'evento per il secondo parametro.  Alcuni gestori eventi, ad esempio quelli per gli eventi <xref:System.Windows.Forms.Control.MouseDown> e <xref:System.Windows.Forms.Control.MouseUp>, dispongono dello stesso tipo di oggetto per il secondo parametro.  Per questi tipi di eventi è possibile utilizzare lo stesso gestore.  
  
 È anche possibile utilizzare lo stesso gestore eventi per gestire il medesimo evento per controlli diversi.  Nel caso, ad esempio, di un gruppo di controlli <xref:System.Windows.Forms.RadioButton> in un form, è possibile creare un unico gestore eventi per l'evento <xref:System.Windows.Forms.Control.Click> e associare l'evento <xref:System.Windows.Forms.Control.Click> di ciascun controllo al singolo gestore eventi.  Per ulteriori informazioni, vedere [How to: Connect Multiple Events to a Single Event Handler in Windows Forms](../../../docs/framework/winforms/how-to-connect-multiple-events-to-a-single-event-handler-in-windows-forms.md).  
  
## Vedere anche  
 [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [Events Overview](../../../docs/framework/winforms/events-overview-windows-forms.md)
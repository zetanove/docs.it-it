---
title: "How to: Connect Multiple Events to a Single Event Handler in Windows Forms | Microsoft Docs"
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
  - "events [Windows Forms], connecting multiple to single event handler"
  - "event handlers [Windows Forms], connecting events to"
  - "menus, event-handling methods for multiple menu items"
  - "Windows Forms controls, events"
  - "menu items, multicasting event-handling methods"
ms.assetid: 5a20749a-41b5-4acc-8eb1-9e5040b0a2c4
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Connect Multiple Events to a Single Event Handler in Windows Forms
Nella progettazione dell'applicazione può essere necessario disporre di un singolo gestore per più eventi o di più eventi che eseguano la stessa procedura.  Un comando di menu che attiva lo stesso evento generato da un pulsante nel form, ad esempio, costituisce un notevole risparmio di tempo se entrambi espongono la stessa funzionalità.  Per ottenere questo risultato in C\# utilizzare la visualizzazione Eventi della finestra Proprietà mentre in Visual Basic utilizzare la parola chiave `Handles` e le caselle di riepilogo **Nome classe** e **Nome metodo del gestore del codice**.  
  
### Per connettere più eventi a un unico gestore eventi in Visual Basic  
  
1.  Fare clic con il pulsante destro del mouse sul form, quindi scegliere **Visualizza codice**.  
  
2.  Dalla casella di riepilogo **Nome classe** selezionare uno dei controlli che si desidera gestire con il gestore eventi.  
  
3.  Dalla casella di riepilogo **Nome metodo** selezionare uno degli eventi che si desidera gestire con il gestore eventi.  
  
4.  Verrà inserito il gestore eventi appropriato e il punto di inserimento verrà posto all'interno del metodo.  Nell'esempio qui di seguito si illustra questa procedura per l'evento <xref:System.Windows.Forms.Control.Click> relativo al controllo <xref:System.Windows.Forms.Button>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
5.  Aggiungere alla clausola `Handles` gli altri eventi che si desidera siano gestiti dal gestore.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click, Button2.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
6.  Aggiungere il codice appropriato nel gestore eventi.  
  
### Per connettere più eventi a un singolo gestore eventi in C\#  
  
1.  Selezionare il controllo a cui si desidera connettere un gestore eventi.  
  
2.  Nella finestra Proprietà fare clic sul pulsante **Eventi** \(![Pulsante Eventi](../../../docs/framework/winforms/media/vxeventsbutton-propertieswindow.png "vxEventsButton\_PropertiesWindow")\).  
  
3.  Fare clic sul nome dell'evento che si desidera gestire.  
  
4.  Nella sezione relativa al valore accanto al nome dell'evento fare clic sul pulsante a discesa, per visualizzare un elenco di gestori eventi esistenti che corrispondono alla firma del metodo dell'evento che si desidera gestire.  
  
5.  Selezionare il gestore eventi adatto dall'elenco.  
  
     Il codice verrà aggiunto al form per associare l'evento al gestore eventi esistente.  
  
## Vedere anche  
 [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [Event Handlers Overview](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)
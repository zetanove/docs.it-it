---
title: "How to: Create Event Handlers at Run Time for Windows Forms | Microsoft Docs"
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
  - "event handlers, creating"
  - "run time, creating event handlers at"
  - "examples [Windows Forms], event handling"
  - "Button control [Windows Forms], event handlers"
ms.assetid: 2e7c9e1a-61fe-444d-8113-3c5bacf1c8cb
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# How to: Create Event Handlers at Run Time for Windows Forms
Oltre a creare eventi tramite Progettazione Windows Form, è possibile creare un gestore eventi in fase di esecuzione.  Tale operazione consente la connessione di gestori eventi, in base a condizioni espresse nel codice, in fase di esecuzione anziché all'avvio del programma.  
  
### Per creare un gestore eventi in fase di esecuzione  
  
1.  Nell'editor del codice aprire il form a cui si desidera aggiungere un gestore eventi.  
  
2.  Aggiungere un metodo al form, utilizzando la firma del metodo per l'evento che si desidera gestire.  
  
     Se, ad esempio, si sta gestendo l'evento <xref:System.Windows.Forms.Control.Click> di un controllo, <xref:System.Windows.Forms.Button> creare un metodo analogo al seguente:  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)  
       ' Add event handler code here.  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)   
    {  
    // Add event handler code here.  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,   
          System::EventArgs ^ e)  
       {  
          // Add event handler code here.  
       }  
    ```  
  
3.  Aggiungere il codice al gestore eventi adatto all'applicazione.  
  
4.  Stabilire il form o il controllo per cui si desidera creare un gestore eventi.  
  
5.  In un metodo nella classe del form aggiungere codice per specificare il gestore eventi per l'evento.  Nel codice seguente, ad esempio, viene specificato che il gestore eventi `button1_Click` gestisce l'evento <xref:System.Windows.Forms.Control.Click> di un controllo <xref:System.Windows.Forms.Button>:  
  
    ```vb  
    AddHandler Button1.Click, AddressOf Button1_Click  
  
    ```  
  
    ```csharp  
    button1.Click += new EventHandler(button1_Click);  
  
    ```  
  
    ```cpp  
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
     Il metodo <xref:System.ComponentModel.EventHandlerList.AddHandler%2A> illustrato nel codice Visual Basic imposta un gestore eventi Click per il pulsante.  
  
## Vedere anche  
 [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [Event Handlers Overview](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)   
 [Troubleshooting Inherited Event Handlers in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)
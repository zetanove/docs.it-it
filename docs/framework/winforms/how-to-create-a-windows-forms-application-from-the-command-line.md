---
title: "How to: Create a Windows Forms Application from the Command Line | Microsoft Docs"
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
  - "Windows Forms, application development from command line"
  - "Windows Forms, getting started"
  - "Windows Forms, creating basic form"
ms.assetid: 45ad3f8b-1c26-4c9f-91a9-3bb0759a47a4
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Create a Windows Forms Application from the Command Line
Le seguenti procedure descrivono i passaggi di base che è necessario completare per creare ed eseguire un'applicazione Windows Form dalla riga di comando.  Esiste un supporto completo per queste procedure in Visual Studio.  Vedere anche [Procedura dettagliata: Creazione di un Windows Form semplice](http://msdn.microsoft.com/library/z9w2f38k\(v=vs.110\)).  
  
## Routine  
  
#### Per creare il form  
  
1.  In un file di codice vuoto digitare le istruzioni import o using seguenti:  
  
     [!code-csharp[System.Windows.Forms.BasicForm#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BasicForm#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#2)]  
  
2.  Dichiarare una classe denominata `Form1` che eredita dalla classe Form.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BasicForm#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#3)]  
  
3.  Creare un costruttore predefinito per `Form1`.  
  
     Si aggiungerà il resto del codice al costruttore in una procedura successiva.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.BasicForm#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#4)]  
  
4.  Aggiungere un metodo `Main` alla classe.  
  
    1.  Applicare <xref:System.STAThreadAttribute> al metodo `Main` per specificare che l'applicazione Windows Form è un apartment a thread singolo.  
  
    2.  Chiamare <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> per conferire all'applicazione l'aspetto di Windows XP.  
  
    3.  Creare un'istanza del form ed eseguirla.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.BasicForm#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#5)]  
  
#### Per compilare l'applicazione ed eseguirla  
  
1.  Al prompt dei comandi di .NET Framework passare alla directory creata per la classe `Form1`.  
  
2.  Compilare il form.  
  
    -   Se si usa C\#, digitare: `csc form1.cs`  
  
         `-oppure-`  
  
    -   Se si usa Visual Basic, digitare: `vbc form1.vb /r:system.dll,system.drawing.dll,system.windows.forms.dll`  
  
3.  Al prompt dei comandi digitare: `Form1.exe`.  
  
## Aggiunta di un controllo e gestione di un evento  
 I passaggi della precedente procedura hanno illustrato come creare un Windows Form di base che viene compilato ed eseguito.  La procedura successiva mostrerà come creare e aggiungere un controllo al form e come gestire un evento per il controllo.  Per altre informazioni sui controlli che è possibile aggiungere a Windows Form, vedere [Controlli per Windows Form](../../../docs/framework/winforms/controls/index.md).  
  
 Oltre a saper creare applicazioni Windows Form, è consigliabile conoscere la programmazione basata sugli eventi e come gestire l'input utente.  Per altre informazioni, vedere [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md) e [Gestione dell'input dell'utente](../../../docs/framework/winforms/controls/handling-user-input.md)  
  
#### Per dichiarare un pulsante e gestirne l'evento click  
  
1.  Dichiarare un pulsante denominato `button1`.  
  
2.  Nel costruttore creare il pulsante e impostarne le proprietà <xref:System.Windows.Forms.Control.Size%2A>, <xref:System.Windows.Forms.Control.Location%2A> e <xref:System.Windows.Forms.Control.Text%2A>.  
  
3.  Aggiungere il pulsante al form.  
  
     Nell'esempio di codice seguente viene illustrato come dichiarare il pulsante.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.FormWithButton#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#2)]  
  
4.  Creare un metodo per gestire l'evento <xref:System.Windows.Forms.Control.Click> per il pulsante.  
  
5.  Nel gestore dell'evento click visualizzare un oggetto <xref:System.Windows.Forms.MessageBox> con il messaggio "Hello World".  
  
     Nell'esempio di codice seguente viene illustrato come gestire l'evento click del pulsante.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.FormWithButton#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#3)]  
  
6.  Associare l'evento <xref:System.Windows.Forms.Control.Click> al metodo creato.  
  
     Nell'esempio di codice seguente viene illustrato come associare l'evento al metodo.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.FormWithButton#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#4)]  
  
7.  Compilare ed eseguire l'applicazione come descritto nella precedente procedura.  
  
## Esempio  
 L'esempio di codice seguente è l'esempio completo tratto dalle precedenti procedure.  
  
 [!code-csharp[System.Windows.Forms.FormWithButton#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.FormWithButton#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#1)]  
  
## Compilazione del codice  
  
-   Per compilare il codice, seguire le istruzioni disponibili nella procedura che descrive come compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Form>   
 <xref:System.Windows.Forms.Control>   
 [Changing the Appearance of Windows Forms](../../../docs/framework/winforms/changing-the-appearance-of-windows-forms.md)   
 [Enhancing Windows Forms Applications](../../../docs/framework/winforms/advanced/index.md)   
 [Getting Started with Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)
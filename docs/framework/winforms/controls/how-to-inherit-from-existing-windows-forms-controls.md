---
title: "Procedura: ereditare da controlli di Windows Form esistenti | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], ereditarietà"
  - "ereditarietà, Windows Form (controlli personalizzati)"
ms.assetid: 1e1fc8ea-c615-4cf0-a356-16d6df7444ab
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: ereditare da controlli di Windows Form esistenti
Per estendere la funzionalità di un controllo esistente, è possibile creare un controllo derivato da un controllo esistente mediante ereditarietà.  Da un controllo esistente si ereditano tutte le funzionalità e le proprietà visive del controllo.  Se si crea, ad esempio, un controllo che eredita da <xref:System.Windows.Forms.Button>, esso avrà lo stesso aspetto e la stessa funzione di un controllo <xref:System.Windows.Forms.Button> standard.  La funzionalità del nuovo controllo potrà essere estesa o modificata mediante l'implementazione di metodi e proprietà personalizzati.  In alcuni controlli è inoltre possibile modificare l'aspetto visivo del controllo ereditato mediante l'override del relativo metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un controllo ereditato  
  
1.  Creare un nuovo progetto **Applicazione Windows Form**.  
  
2.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento**.  
  
3.  Nella finestra di dialogo **Aggiungi nuovo elemento** fare doppio clic su **Controllo personalizzato**.  
  
     Un nuovo controllo personalizzato verrà aggiunto al progetto.  
  
4.  Se si utilizza Visual Basic, fare clic su **Mostra tutti i file** nella parte superiore di **Esplora soluzioni**.  Espandere CustomControl1.vb, quindi aprire CustomControl1.Designer.vb nell'editor di codice.  
  
5.  Se si utilizza C\#, aprire CustomControl1.cs nell'editor di codice.  
  
6.  Individuare la dichiarazione della classe che eredita da <xref:System.Windows.Forms.Control>.  
  
7.  Sostituire la classe di base con il controllo da cui si desidera ereditare.  
  
     Per ereditare da <xref:System.Windows.Forms.Button> modificare ad esempio la dichiarazione della classe come segue:  
  
    ```vb  
    Partial Class CustomControl1  
        Inherits System.Windows.Forms.Button  
    ```  
  
    ```csharp  
    public partial class CustomControl1 : System.Windows.Forms.Button  
    ```  
  
8.  Se si utilizza Visual Basic, salvare e chiudere CustomControl1.Designer.vb.  Aprire CustomControl1.vb nell'editor di codice.  
  
9. Implementare eventuali metodi o proprietà personalizzate da incorporare nel controllo.  
  
10. Per modificare l'aspetto grafico del controllo, eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
    > [!NOTE]
    >  L'override di <xref:System.Windows.Forms.Control.OnPaint%2A> non consente la modifica dell'aspetto di tutti i controlli.  Alcuni controlli il cui disegno viene eseguito completamente in Windows, come <xref:System.Windows.Forms.TextBox>, non chiamano mai il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> e, pertanto, non utilizzeranno il codice personalizzato.  Per verificare se il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> è disponibile, fare riferimento alla documentazione del controllo specifico che si desidera modificare.  Per un elenco dei controlli Windows Form, vedere [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md).  Se il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> di un controllo non viene elencato come metodo membro, non sarà possibile modificare l'aspetto del controllo mediante l'override di questo metodo.  Per ulteriori informazioni sul disegno personalizzato, vedere [Disegno e rendering di controlli personalizzati](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md).  
  
    ```vb  
    Protected Overrides Sub OnPaint(ByVal e As _  
       System.Windows.Forms.PaintEventArgs)  
       MyBase.OnPaint(e)  
       ' Insert code to do custom painting.   
       ' If you want to completely change the appearance of your control,  
       ' do not call MyBase.OnPaint(e).  
    End Sub  
  
    ```  
  
    ```csharp  
    protected override void OnPaint(PaintEventArgs pe)  
    {  
       base.OnPaint(pe);  
       // Insert code to do custom painting.  
       // If you want to completely change the appearance of your control,  
       // do not call base.OnPaint(pe).  
    }  
    ```  
  
11. Salvare ed eseguire il test del controllo.  
  
## Vedere anche  
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [Procedura: ereditare dalla classe Control](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [Procedura: ereditare dalla classe UserControl](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [Procedura: creare controlli per Windows Form](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [Troubleshooting Inherited Event Handlers in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)   
 [Procedura dettagliata: eredità da un controllo Windows Form con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [Procedura dettagliata: eredità da un controllo di Windows Form con Visual C\#](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
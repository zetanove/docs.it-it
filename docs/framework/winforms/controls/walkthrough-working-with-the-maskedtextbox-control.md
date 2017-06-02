---
title: "Procedura dettagliata: utilizzo del controllo MaskedTextBox | Microsoft Docs"
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
  - "input, controllo per verificare la validità"
  - "MaskedTextBox (controllo) [Windows Form], convalida"
  - "MaskedTextBox (controllo) [Windows Form], procedure dettagliate"
  - "testo, controlli per input"
  - "input utente, controllo"
ms.assetid: df60565e-5447-4110-92a6-be1f6ff5faa3
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura dettagliata: utilizzo del controllo MaskedTextBox
Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Inizializzazione del controllo <xref:System.Windows.Forms.MaskedTextBox>  
  
-   Utilizzo del gestore eventi <xref:System.Windows.Forms.MaskedTextBox.MaskInputRejected> per avvertire l'utente quando un carattere non è conforme alla maschera  
  
-   Assegnazione di un tipo alla proprietà <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> e utilizzo del gestore eventi <xref:System.Windows.Forms.MaskedTextBox.TypeValidationCompleted> per avvertire l'utente quando il valore di cui si sta tentando di eseguire il commit non è valido per il tipo  
  
## Creazione del progetto e aggiunta di un controllo  
  
#### Per aggiungere un controllo MaskedTextBox al form  
  
1.  Aprire il form in cui inserire il controllo <xref:System.Windows.Forms.MaskedTextBox>.  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.MaskedTextBox> dalla **Casella degli strumenti** nel form.  
  
3.  Fare clic con il pulsante destro del mouse sul controllo, quindi scegliere **Proprietà**.  Nella finestra **Proprietà** selezionare la proprietà **Mask** e fare clic sul pulsante con i puntini di sospensione accanto al nome della proprietà.  
  
4.  Nella finestra di dialogo **Maschera input** selezionare la maschera **Data breve** e fare clic su **OK**.  
  
5.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.MaskedTextBox.BeepOnError%2A> su `true`.  Questa proprietà prevede l'emissione di un breve segnale acustico ogni volta che l'utente tenta di immettere un carattere che viola la definizione della maschera.  
  
 Per un riepilogo dei caratteri supportati dalla proprietà Mask, vedere la sezione relativa alle osservazioni della proprietà <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>.  
  
## Segnalazione di errori di input  
  
#### Aggiungere una descrizione comandi per l'input di maschera rifiutato  
  
1.  Tornare alla **Casella degli strumenti** e aggiungere un controllo <xref:System.Windows.Forms.ToolTip> al form.  
  
2.  Creare un gestore eventi per l'evento <xref:System.Windows.Forms.MaskedTextBox.MaskInputRejected> che genera il controllo <xref:System.Windows.Forms.ToolTip> quando si verifica un errore di input.  La descrizione comandi resta visibile per cinque secondi o finché l'utente non la seleziona con un clic.  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        ... // Other initialization code  
        maskedTextBox1.Mask = "00/00/0000";  
        maskedTextBox1.MaskInputRejected += new MaskInputRejectedEventHandler(maskedTextBox1_MaskInputRejected)  
    }  
  
    void maskedTextBox1_MaskInputRejected(object sender, MaskInputRejectedEventArgs e)  
    {  
        toolTip1.ToolTipTitle = "Invalid Input";  
        toolTip1.Show("We're sorry, but only digits (0-9) are allowed in dates.", maskedTextBox1, maskedTextBox1.Location, 5000);  
    }  
    ```  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load  
        Me.ToolTip1.IsBalloon = True  
        Me.MaskedTextBox1.Mask = "00/00/0000"  
    End Sub  
  
    Private Sub MaskedTextBox1_MaskInputRejected(sender as Object, e as MaskInputRejectedEventArgs) Handles MaskedTextBox1.MaskInputRejected  
        ToolTip1.ToolTipTitle = "Invalid Input"  
        ToolTip1.Show("We're sorry, but only digits (0-9) are allowed in dates.", MaskedTextBox1, 5000)  
    End Sub  
  
    ```  
  
## Segnalazione di un tipo non valido  
  
#### Aggiungere una descrizione comandi per i tipi di dati non validi  
  
1.  Nel gestore eventi <xref:System.Windows.Forms.Form.Load> del form assegnare un oggetto <xref:System.Type> che rappresenta il tipo <xref:System.DateTime> alla proprietà <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> del controllo <xref:System.Windows.Forms.MaskedTextBox>:  
  
    ```csharp  
    private void Form1_Load(Object sender, EventArgs e)  
    {  
        // Other code  
        maskedTextBox1.ValidatingType = typeof(System.DateTime);  
        maskedTextBox1.TypeValidationCompleted += new TypeValidationEventHandler(maskedTextBox1_TypeValidationCompleted);  
    }  
    ```  
  
    ```vb  
    Private Sub Form1_Load(sender as Object, e as EventArgs)  
        // Other code  
        MaskedTextBox1.ValidatingType = GetType(System.DateTime)  
    End Sub  
    ```  
  
2.  Aggiungere un gestore eventi per l'evento <xref:System.Windows.Forms.MaskedTextBox.TypeValidationCompleted>:  
  
    ```csharp  
    public void maskedTextBox1_TypeValidationCompleted(object sender, TypeValidationEventArgs e)  
    {  
        if (!e.IsValidInput)  
        {  
           toolTip1.ToolTipTitle = "Invalid Date Value";  
           toolTip1.Show("We're sorry, but the value you entered is not a valid date. Please change the value.", maskedTextBox1, 5000);  
           e.Cancel = true;  
        }  
    }  
    ```  
  
    ```vb  
    Public Sub MaskedTextBox1_TypeValidationCompleted(sender as Object, e as TypeValidationEventArgs)  
        If Not e.IsValidInput Then  
           ToolTip1.ToolTipTitle = "Invalid Date Value"  
           ToolTip1.Show("We're sorry, but the value you entered is not a valid date. Please change the value.", maskedTextBox1, 5000)  
           e.Cancel = True  
        End If  
    End Sub  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.MaskedTextBox>   
 [Controllo MaskedTextBox](../../../../docs/framework/winforms/controls/maskedtextbox-control-windows-forms.md)
---
title: "International Fonts in Windows Forms and Controls | Microsoft Docs"
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
  - "fonts, international"
  - "international applications [Windows Forms], character display"
  - "fonts, globalization considerations"
  - "localization [Windows Forms], fonts"
  - "Windows Forms controls, labels"
  - "font fallback in Windows Forms"
  - "globalization [Windows Forms], character sets"
ms.assetid: 2c3066df-9bac-479a-82b2-79e484b346a3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# International Fonts in Windows Forms and Controls
Nelle applicazioni internazionali, il metodo consigliato per selezionare i tipi di carattere consiste nell'utilizzare il fallback dei tipi di carattere ove possibile.  Per fallback dei tipi di carattere si intende la determinazione nel sistema dello script a cui appartiene il carattere.  
  
## Utilizzo del fallback dei tipi di carattere  
 Per utilizzare questa funzionalità, non è necessario impostare la proprietà <xref:System.Drawing.Font> per il form o altri elementi.  Verrà utilizzato automaticamente il tipo di carattere predefinito del sistema, che è diverso in base alla lingua in cui è localizzato il sistema operativo.  Quando l'applicazione viene eseguita, il tipo di carattere corretto viene fornito automaticamente dal sistema in base alle impostazioni cultura selezionate nel sistema operativo.  
  
 È consentita un'eccezione alla regola che prevede di non impostare il tipo di carattere, che riguarda la modifica dello stile del carattere.  Questo tipo di modifica può risultare importante, ad esempio, nel caso di un'applicazione in cui, selezionando un pulsante, è possibile visualizzare in grassetto il testo contenuto in una casella di testo.  A tale scopo, è necessario creare una funzione per modificare lo stile del carattere nella casella di testo, indipendentemente dal tipo di carattere del form.  È importante chiamare questa funzione in due punti: nel gestore dell'evento <xref:System.Windows.Forms.Control.Click> del pulsante e nel gestore dell'evento <xref:System.Windows.Forms.Control.FontChanged>.  Se la funzione viene chiamata soltanto nel gestore dell'evento <xref:System.Windows.Forms.Control.Click> e il gruppo di caratteri dell'intero form viene modificato da altre parti di codice, la casella di testo non verrà modificata con il resto del form.  
  
```  
' Visual Basic  
Private Sub MakeBold()  
   ' Change the TextBox to a bold version of the form font  
   TextBox1.Font = New Font(Me.Font, FontStyle.Bold)  
End Sub  
  
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
   ' Clicking this button makes the TextBox bold  
   MakeBold()  
End Sub  
  
Private Sub Form1_FontChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.FontChanged  
   ' If the TextBox is already bold and the form's font changes,  
   ' change the TextBox to a bold version of the new form font  
   If (TextBox1.Font.Style = FontStyle.Bold) Then  
      MakeBold()  
   End If  
End Sub  
  
// C#  
private void button1_Click(object sender, System.EventArgs e)  
{  
   // Clicking this button makes the TextBox bold  
   MakeBold();  
}  
  
private void MakeBold()   
{  
   // Change the TextBox to a bold version of the form's font  
   textBox1.Font = new Font(this.Font, FontStyle.Bold);  
}  
  
private void Form1_FontChanged(object sender, System.EventArgs e)  
{  
   // If the TextBox is already bold and the form's font changes,  
   // change the TextBox to a bold version of the new form font  
   if (textBox1.Font.Style == FontStyle.Bold)   
   {  
      MakeBold();  
   }  
}  
```  
  
 Tuttavia, quando l'applicazione viene localizzata, il carattere in grassetto potrebbe essere visualizzato in maniera non corretta per alcune lingue.  In caso ciò rappresentasse un problema, è possibile consentire ai localizzatori di formattare il carattere da grassetto a testo normale.  Poiché in genere i localizzatori, a differenza degli sviluppatori, non hanno accesso al codice sorgente ma solo ai file di risorse, questa opzione deve essere impostata nei file di risorse.  A tale scopo è necessario impostare la proprietà <xref:System.Drawing.Font.Bold%2A> su `true`.  In questo modo l'impostazione del tipo di carattere verrà scritta nei file di risorse, dove potrà essere modificata.  Sarà quindi necessario scrivere il codice dopo il metodo `InitializeComponent` per reimpostare il tipo di carattere partendo dal carattere corrente del form, ma utilizzando lo stile specificato nel file di risorse.  
  
```  
' Visual Basic  
TextBox1.Font = New System.Drawing.Font(Me.Font, TextBox1.Font.Style)  
  
// C#  
textBox1.Font = new System.Drawing.Font(this.Font, textBox1.Font.Style);  
```  
  
## Vedere anche  
 [Globalizing Windows Forms](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)
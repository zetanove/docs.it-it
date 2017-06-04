---
title: "Procedura: disporre i form figlio MDI | Microsoft Docs"
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
  - "form figlio, disposizione"
  - "MDI, disposizione di form figlio"
ms.assetid: a0786378-3206-4ccc-898e-7d3b38cc5089
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: disporre i form figlio MDI
Le applicazioni hanno spesso dei comandi di menu per azioni quali Affianca, Sovrapponi e Disponi che controllano il layout dei form figlio MDI aperti.  È possibile usare il metodo <xref:System.Windows.Forms.Form.LayoutMdi%2A> con uno dei valori di enumerazione <xref:System.Windows.Forms.MdiLayout> per ridisporre i form figlio in un form padre MDI.  
  
 I valori di enumerazione <xref:System.Windows.Forms.MdiLayout> visualizzano i form figlio sovrapposti, affiancati orizzontalmente o verticalmente o sotto forma di icone disposte nella parte inferiore del form MDI.  Questi valori hanno lo stesso effetto dei comandi Windows corrispondenti, **Sovrapponi le finestre**, **Mostra le finestre affiancate**, **Mostra le finestre in pila** e **Mostra desktop**.  
  
 Spesso questi metodi vengono usati come gestori eventi chiamati da un evento della voce di menu <xref:System.Windows.Forms.Control.Click>.  In questo modo, una voce di menu con testo "Sovrapponi le finestre" può avere l'effetto desiderato sulle finestre figlio MDI.  
  
### Per disporre i form figlio  
  
1.  In un metodo usare il metodo <xref:System.Windows.Forms.Form.LayoutMdi%2A> per impostare l'enumerazione <xref:System.Windows.Forms.MdiLayout> per il form padre MDI.  Nel seguente esempio viene usato il valore di enumerazione <xref:System.Windows.Forms.MdiLayout?displayProperty=fullName> per le finestre figlio del form padre MDI \(`Form1`\).  L'enumerazione viene usata nel codice durante l'esecuzione del gestore eventi per l'evento <xref:System.Windows.Forms.Control.Click> della voce di menu **Sovrapponi le finestre**.  
  
    ```vb  
    Protected Sub CascadeWindows_Click(ByVal sender As System.Object, ByVal e As System.EventArgs)  
       Me.LayoutMdi(System.Windows.Forms.MdiLayout.Cascade)  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void CascadeWindows_Click(object sender, System.EventArgs e){  
       this.LayoutMdi(System.Windows.Forms.MdiLayout.Cascade);  
    }  
    ```  
  
    > [!NOTE]
    >  È anche possibile affiancare le finestre e disporle sotto forma di icona modificando i valori di enumerazione <xref:System.Windows.Forms.MdiLayout> usati.  
  
2.  Se si usa Visual C\#, inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
## Vedere anche  
 [Applicazioni MDI \(Interfaccia a documenti multipli, Multiple\-Document Interface\)](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)   
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [Procedura: creare form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [Procedura: determinare il figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)   
 [Procedura: inviare dati al figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)
---
title: "Procedura: impostare la maschera di input | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "net.ComponentModel.MaskPropertyEditor"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "MaskedTextBox (controllo) [Windows Form]"
ms.assetid: 779b3a12-cd74-4e58-b46e-04983bda5b2c
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: impostare la maschera di input
Il controllo casella di testo mascherata è un controllo casella di testo avanzato che supporta una sintassi dichiarativa per l'accettazione o il rifiuto dell'input dell'utente.  Impostando la proprietà Mask, è possibile specificare l'input dell'utente consentito senza che sia necessario scrivere nell'applicazione una logica di convalida personalizzata.  Per ulteriori informazioni, vedere la sezione relativa alle osservazioni della classe <xref:System.Windows.Forms.MaskedTextBox>.  
  
## Impostazione manuale della proprietà Mask  
 Se si ha dimestichezza con i caratteri supportati dalla proprietà Mask, è possibile immetterla manualmente.  Per un riepilogo dei caratteri supportati dalla proprietà Mask, vedere la sezione relativa alle osservazioni della proprietà <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>.  
  
#### Per impostare manualmente la proprietà Mask  
  
1.  Nella visualizzazione **Progettazione** selezionare un oggetto <xref:System.Windows.Forms.MaskedTextBox>.  
  
2.  Nella finestra **Proprietà** individuare la proprietà <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>.  
  
3.  Digitare la maschera desiderata.  Ad esempio, digitare `###`.  
  
## Utilizzo della finestra di dialogo Maschera di input  
 La finestra di dialogo Maschera di input fornisce alcune maschere di input predefinite.  È inoltre possibile modificare le maschere predefinite o immettere manualmente una maschera personalizzata.  
  
#### Per aprire la finestra di dialogo Maschera di input  
  
1.  Nella visualizzazione **Progettazione** selezionare un oggetto <xref:System.Windows.Forms.MaskedTextBox>.  
  
    1.  Fare clic sullo smart tag per aprire il riquadro **Attività MaskedTextBox**.  
  
    2.  Fare clic su **Imposta maschera**.  
  
     \- oppure \-  
  
    1.  Nella finestra **Proprietà** selezionare la proprietà <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>.  
  
    2.  Fare clic sul pulsante con i puntini di sospensione nella colonna relativa al valore della proprietà.  
  
     Verrà visualizzata la finestra di dialogo **Maschera di input**.  
  
#### Per utilizzare la finestra di dialogo Maschera di input  
  
1.  \(Facoltativo\) Fare clic su una delle maschere predefinite nell'elenco.  
  
2.  \(Facoltativo\) Modificare la maschera predefinita nella casella **Maschera**.  
  
3.  \(Facoltativo\) Digitare una nuova maschera nella casella **Maschera**.  In altri termini, non è necessario utilizzare una delle maschere predefinite.  
  
    > [!NOTE]
    >  Nella casella Anteprima vengono visualizzati i caratteri visibili all'utente nel controllo <xref:System.Windows.Forms.MaskedTextBox>.  Questi caratteri consentono all'utente di immettere i dati correttamente.  
  
4.  Selezionare o deselezionare la casella di controllo **Utilizza ValidatingType**.  La casella di controllo **Utilizza ValidatingType** specifica se un tipo di dati viene utilizzato per verificare l'immissione dei dati da parte dell'utente.   Per ulteriori informazioni, vedere la proprietà <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A>.  
  
5.  Scegliere **OK**.  
  
     La maschera viene immessa nella proprietà **Mask** della finestra **Proprietà**.  
  
## Vedere anche  
 [Procedura dettagliata: utilizzo del controllo MaskedTextBox](../../../../docs/framework/winforms/controls/walkthrough-working-with-the-maskedtextbox-control.md)
---
title: "Cenni preliminari sul controllo RadioButton (Windows Form) | Microsoft Docs"
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
  - "RadioButton"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "pulsanti di opzione, informazioni sui pulsanti di opzione"
  - "pulsanti di opzione, rilevamento stato"
  - "RadioButton (controllo) [Windows Form], informazioni sul controllo RadioButton"
  - "RadioButton (controllo) [Windows Form], rilevamento stato"
ms.assetid: cd11f0c2-d098-4022-adf9-1455bc166a13
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul controllo RadioButton (Windows Form)
I controlli <xref:System.Windows.Forms.RadioButton> Windows Form presentano all'utente un insieme di due o più opzioni in cui è possibile selezionare una sola opzione.  Nonostante possa apparire simile, il funzionamento dei pulsanti di opzione e delle caselle di controllo è fondamentalmente diverso. Se si seleziona un pulsante di opzione, non sarà infatti possibile selezionarne anche un altro all'interno dello stesso gruppo.  È invece possibile selezionare più di una casella di controllo.  Si crea un pulsante di opzione al fine di mostrare all'utente una serie di opzioni di cui è consentito selezionarne una sola.  
  
## Utilizzo del controllo  
 Quando si seleziona un controllo <xref:System.Windows.Forms.RadioButton>, la proprietà <xref:System.Windows.Forms.RadioButton.Checked%2A> viene impostata su `true` e viene richiamato il gestore dell'evento <xref:System.Windows.Forms.Control.Click>.  L'evento <xref:System.Windows.Forms.RadioButton.CheckedChanged> viene generato quando il valore della proprietà <xref:System.Windows.Forms.RadioButton.Checked%2A> viene modificato.  Se la proprietà <xref:System.Windows.Forms.RadioButton.AutoCheck%2A> è impostata su `true` \(impostazione predefinita\), quando si seleziona il pulsante di opzione tutti gli altri pulsanti all'interno del gruppo vengono automaticamente deselezionati.  Questa proprietà viene in genere impostata su `false` solo quando si utilizza del codice per verificare che il pulsante di opzione selezionato sia un'opzione disponibile.  Il testo visualizzato all'interno del controllo viene impostato con la proprietà <xref:System.Windows.Forms.Control.Text%2A>, che può contenere tasti di scelta rapida.  Un tasto di scelta consente di scegliere il controllo mediante la pressione del tasto ALT e del tasto assegnato.  Per ulteriori informazioni, vedere [Procedura: creare tasti di scelta per i controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md) e [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md).  
  
 Quando viene selezionato, il controllo <xref:System.Windows.Forms.RadioButton> viene visualizzato come un pulsante di comando attivato, se la proprietà <xref:System.Windows.Forms.RadioButton.Appearance%2A> è impostata su <xref:System.Windows.Forms.Appearance>.  I pulsanti di opzione possono inoltre visualizzare immagini utilizzando le proprietà <xref:System.Windows.Forms.ButtonBase.Image%2A> e <xref:System.Windows.Forms.ButtonBase.ImageList%2A>.  Per ulteriori informazioni, vedere [Procedura: impostare l'immagine visualizzata da un controllo Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-image-displayed-by-a-windows-forms-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.RadioButton>   
 [Cenni preliminari sul controllo Panel](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo GroupBox](../../../../docs/framework/winforms/controls/groupbox-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [Procedura: creare tasti di scelta per i controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)   
 [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [Procedura: raggruppare controlli RadioButton Windows Form in modo che funzionino come set](../../../../docs/framework/winforms/controls/how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md)   
 [Controllo RadioButton](../../../../docs/framework/winforms/controls/radiobutton-control-windows-forms.md)
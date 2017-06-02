---
title: "Procedura: consentire agli utenti di copiare pi&#249; celle negli Appunti dal controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "celle, copia negli Appunti"
  - "Appunti, copia di più celle"
  - "griglie dei dati, copia di più celle"
  - "DataGridView (controllo) [Windows Form], copia di più celle"
ms.assetid: fd0403b2-d0e3-4ae0-839c-0f737e1eb4a9
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: consentire agli utenti di copiare pi&#249; celle negli Appunti dal controllo DataGridView di Windows Form
Quando si attiva la copia delle celle, i dati contenuti nel controllo <xref:System.Windows.Forms.DataGridView> sono facilmente accessibili da altre applicazioni tramite la classe <xref:System.Windows.Forms.Clipboard>.  I valori delle celle selezionate vengono convertiti in stringhe e aggiunti negli Appunti sotto forma di valori di testo delimitato da tabulazioni, per consentirne l'inserimento in applicazioni quali Blocco note ed Excel, e sotto forma di una tabella in formato HTML, per consentirne l'inserimento in applicazioni come Word.  
  
 È possibile configurare la funzionalità di copia dalle celle in modo da copiare solo i valori delle celle, includere il testo della riga e dell'intestazione della colonna nei dati degli Appunti o includere il testo dell'intestazione solo quando gli utenti selezionano righe o colonne intere.  
  
 A seconda della modalità di selezione gli utenti possono selezionare più gruppi di celle scollegati.  Quando un utente copia le celle negli Appunti, le righe e le colonne in cui non è selezionata alcuna cella non vengono copiate.  Tutte le altre righe o colonne diventano righe o colonne nella tabella di dati copiati negli Appunti.   Le celle non selezionate in queste righe o colonne vengono copiate come segnaposto vuoti negli Appunti.  
  
### Per abilitare la copia delle celle  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A?displayProperty=fullName>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewClipboardDemo#15](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/CS/datagridviewclipboarddemo.cs#15)]
     [!code-vb[System.Windows.Forms.DataGridViewClipboardDemo#15](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/VB/datagridviewclipboarddemo.vb#15)]  
  
## Esempio  
 Nell'esempio di codice completo seguente viene illustrato come le celle vengono copiate negli Appunti.  In questo esempio è incluso un pulsante che consente di copiare le celle selezionate negli Appunti mediante il metodo <xref:System.Windows.Forms.DataGridView.GetClipboardContent%2A?displayProperty=fullName> e viene visualizzato il contenuto degli Appunti in una casella di testo.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewClipboardDemo#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/CS/datagridviewclipboarddemo.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewClipboardDemo#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/VB/datagridviewclipboarddemo.vb#00)]  
  
## Compilazione del codice  
 Per questo codice sono necessari i requisiti seguenti:  
  
-   Riferimenti agli assembly N:System e N:System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A>   
 <xref:System.Windows.Forms.DataGridView.GetClipboardContent%2A>   
 [Utilizzo della selezione e degli Appunti con il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)
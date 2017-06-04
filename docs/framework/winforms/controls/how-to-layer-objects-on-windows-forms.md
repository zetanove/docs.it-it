---
title: "Procedura: disporre oggetti su pi&#249; livelli in Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], sovrapposizione"
  - "controlli [Windows Form], posizionamento"
  - "controlli Windows Form, sovrapposizione"
  - "ordine z"
  - "ordine z"
ms.assetid: 1acc4281-2976-4715-86f4-bda68134baaf
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: disporre oggetti su pi&#249; livelli in Windows Form
Quando si crea un'interfaccia utente complessa o si utilizza un form con un'interfaccia a documenti multipli \(MDI\), è spesso necessario disporre su più livelli sia i controlli che i form figlio, in modo da creare interfacce utente più complesse.  Per spostare e tenere traccia di controlli e finestre all'interno del contesto del gruppo è necessario modificare l'ordine Z.  Si definisce *ordine Z* la disposizione visiva dei controlli su più livelli all'interno di un form, lungo l'asse z dello stesso form \(profondità\).  La finestra che si trova in cima all'ordine Z si sovrappone a tutte le altre finestre.  Tutte le altre finestre si sovrappongono alla finestra che si trova in fondo all'ordine Z.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per disporre su più livelli i controlli in fase di progettazione  
  
1.  Selezionare un controllo che si desidera disporre su più livelli.  
  
2.  Scegliere **Ordine** dal menu **Formato**, quindi **Porta in primo piano** o **Porta in secondo piano**.  
  
### Per disporre su più livelli i controlli a livello di codice  
  
-   Utilizzare i metodi <xref:System.Windows.Forms.Control.BringToFront%2A> e <xref:System.Windows.Forms.Control.SendToBack%2A> per modificare l'ordine Z dei controlli.  
  
     Se, ad esempio, un controllo <xref:System.Windows.Forms.TextBox>, `txtFirstName`, si trova al di sotto di un altro controllo e si desidera portarlo in primo piano, utilizzare il seguente codice:  
  
    ```vb  
    txtFirstName.BringToFront()  
  
    ```  
  
    ```csharp  
    txtFirstName.BringToFront();  
  
    ```  
  
    ```cpp  
    txtFirstName->BringToFront();  
    ```  
  
> [!NOTE]
>  Windows Form supporta il *contenimento dei controlli* che prevede l'inserimento di più controlli all'interno di un controllo, ad esempio un dato numero di controlli <xref:System.Windows.Forms.RadioButton> all'interno di un controllo <xref:System.Windows.Forms.GroupBox>.  Successivamente sarà possibile disporre i controlli su più livelli all'interno del controllo che li contiene.  Quando la casella di gruppo viene spostata, vengono spostati anche i controlli in essa contenuti.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)
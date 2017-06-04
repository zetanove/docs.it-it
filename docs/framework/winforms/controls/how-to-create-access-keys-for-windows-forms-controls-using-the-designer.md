---
title: "Procedura: creare tasti di scelta per i controlli di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "tasti di scelta, creazione per i controlli"
  - "tasti di scelta, Windows Form"
  - "ALT (tasto)"
  - "carattere e commerciale nel tasto di scelta rapida"
  - "Button (controllo) [Windows Form], tasti di scelta"
  - "controlli [Windows Form], tasti di scelta"
  - "controlli delle finestre di dialogo, tasti di scelta"
  - "esempi [Windows Form], controlli"
  - "tasti di scelta rapida, creazione per i controlli"
  - "tasti di scelta, aggiunta ai controlli delle finestre di dialogo"
  - "Text (proprietà), specifica di tasti di scelta per controlli"
  - "controlli Windows Form, tasti di scelta"
ms.assetid: 4c374c4c-4ca9-4a68-ac96-9dc3ab0f518a
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: creare tasti di scelta per i controlli di Windows Form utilizzando la finestra di progettazione
Un *tasto di scelta* corrisponde a un carattere sottolineato presente nel testo di un menu o di una voce di menu oppure nell'etichetta di un controllo, ad esempio di un pulsante.  La presenza di questo tasto consente di scegliere un pulsante premendo il tasto ALT in combinazione con il tasto di scelta predefinito.  Se ad esempio tramite un pulsante viene eseguita una routine per la stampa di un form e la relativa proprietà `Text` viene impostata su "Stampa", aggiungendo una e commerciale \(&\) prima della lettera "S", la lettera "S" del testo del pulsante risulterà sottolineata in fase di esecuzione.  L'utente può eseguire il comando associato al pulsante premendo ALT\+P.  Non è possibile associare un tasto di scelta a un controllo che non può ricevere lo stato attivo.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un tasto di scelta per un controllo  
  
1.  Nella finestra **Proprietà** impostare la proprietà `Text` su una stringa comprendente una e commerciale \(&\) prima della lettera che costituirà il tasto di scelta.  Per impostare la lettera "S" come tasto di scelta, ad esempio, digitare &Stampa nella griglia.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Button>   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
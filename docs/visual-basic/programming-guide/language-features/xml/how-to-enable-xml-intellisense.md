---
title: "How to: Enable XML IntelliSense in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML IntelliSense [Visual Basic]"
  - "XML [Visual Basic], IntelliSense"
  - "IntelliSense [Visual Basic], XML"
ms.assetid: af67d0ee-a4a6-4abf-9c07-5a8cfe80d111
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# How to: Enable XML IntelliSense in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

IntelliSense XML di Visual Basic consente il completamento delle parole per gli elementi definiti in XML Schema.  Per abilitare IntelliSense XML in Visual Basic è necessario eseguire le operazioni seguenti:  
  
1.  Ottenere il file o i file di schema XML \(XSD\) per i file XML su cui l'applicazione dovrà leggere o scrivere.  
  
2.  Includere i file di schema XML nel progetto.  
  
3.  Importare lo spazio o gli spazi dei nomi di destinazione nel file di codice o nel progetto.  Uno spazio dei nomi di destinazione è identificato dagli attributi `targetNamespace` o `tns` dello schema XSD.  
  
     Per importare uno spazio dei nomi di destinazione, utilizzare l'istruzione `Imports` o aggiungere uno spazio dei nomi per tutti i file di codice in un progetto utilizzando la pagina **Riferimenti** di Progettazione progetti.  
  
 Per ulteriori informazioni sulle funzionalità di IntelliSense XML in Visual Basic, vedere [XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md).  Per ulteriori informazioni sull'importazione degli spazi dei nomi XML, vedere [Imports Statement \(XML Namespace\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md) or [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic).  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
 ![Collegamento a video](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") Per una versione video di questo argomento, vedere [Procedura: abilitare IntelliSense XML in Visual Basic](http://go.microsoft.com/fwlink/?LinkId=102466) \(la pagina potrebbe essere in inglese\).  Per una dimostrazione video correlata, vedere la pagina relativa all'[abilitazione di IntelliSense XML e all'utilizzo dello spazio dei nomi XML](http://go.microsoft.com/fwlink/?LinkId=143035).  
  
## Abilitare IntelliSense XML in Visual Basic  
 Se si dispone di un file XML ma non del relativo file di schema XSD, in SP1 è possibile creare un file di schema XSD utilizzando la procedura guidata XML in schema.  In alternativa è possibile utilizzare l'inferenza di schemi nell'editor XML di Visual Studio.  
  
#### Per creare un file di schema XSD per un file XML utilizzando la procedura guidata XML in schema \(è richiesto SP1\)  
  
1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto** del progetto.  
  
2.  Selezionare il modello di elemento **XML in schema** dalle categorie di modello **Dati** o **Elementi comuni**.  
  
3.  Specificare un nome per uno o più file XSD in cui verrà archiviato l'insieme dello schema dedotto, quindi scegliere **Aggiungi**.  
  
4.  Nella finestra **Deduci insieme dello schema XML da documenti XML**, aggiungere uno o più documenti XML da cui dedurre l'insieme dello schema XML.  
  
    -   Per aggiungere file di testo contenenti documenti XML utilizzando Esplora file, scegliere **Aggiungi da file**.  
  
    -   Per aggiungere un documento XML da un indirizzo HTTP, fare clic su **Aggiungi da Web**.  
  
    -   Per copiare o digitare il contenuto di un documento XML nella procedura guidata, fare clic su **Digita o incolla XML**.  
  
5.  Una volta specificate tutte le origini di documento XML da cui dedurre l'insieme dello schema XML, scegliere **OK** per procedere.  L'insieme dello schema viene salvato nella cartella del progetto in uno o più file XSD.  Viene creato un file per ogni spazio dei nomi XML nello schema.  
  
#### Per creare un file di schema XSD per un file XML utilizzando l'inferenza di schemi nell'editor XML di Visual Studio  
  
1.  Modificare il file XML in Progettazione XML di Visual Studio.  
  
2.  Quando il cursore è posizionato all'interno del file XML, viene visualizzato il menu **XML**.  Scegliere **Crea schema** nel menu **XML**.  Viene creato un file XSD dallo schema XSD dedotto dal file XML.  
  
3.  Salvare il file di schema XSD.  
  
    > [!NOTE]
    >  Da documenti XML multipli che dovrebbero avere lo stesso schema potrebbero venire dedotti schemi XSD diversi.  Ciò può verificarsi, ad esempio, quando certi attributi ed elementi sono presenti in un file XML ma non in un altro, oppure quando gli elementi sono inclusi in ordine diverso.  Quando si utilizza l'inferenza di schemi XSD è necessario rivedere gli schemi XSD derivati per verificarne la completezza e l'accuratezza.  
  
#### Per includere un file di schema XSD  
  
-   Per impostazione predefinita, non è possibile vedere i file XSD nei progetti di Visual Basic..  Se il file XSD è già incluso nelle cartelle del progetto, fare clic sul pulsante **Mostra tutti i file** in **Esplora soluzioni**.  Individuare il file XSD in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file e scegliere **Includi nel progetto**.  
  
-   Se il file XSD non è già parte del progetto, in **Esplora soluzioni**fare clic con il pulsante destro del mouse sulla cartella nella quale si vuole archiviare il file XSD, scegliere **Aggiungi** e quindi fare clic **su Elemento esistente**.  Individuare il file XSD e quindi fare clic su **Aggiungi**.  
  
#### Per importare uno spazio dei nomi XML in un file di codice  
  
1.  Identificare lo spazio dei nomi di destinazione dallo schema XSD.  
  
2.  All'inizio del file di codice, aggiungere un'istruzione `Imports` per lo spazio dei nomi XML di destinazione, come mostrato nell'esempio seguente.  
  
     [!code-vb[VbXMLSamples#1](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-enable-xml-intell_1.vb)]  
  
     Per importare uno spazio dei nomi XML come spazio dei nomi predefinito, cioè lo spazio dei nomi da applicare agli elementi e attributi XML che non hanno un prefisso dello spazio dei nomi, aggiungere un'istruzione `Imports` per lo spazio dei nomi XML predefinito di destinazione.  Non specificare un prefisso dello spazio dei nomi.  Di seguito è riportato un esempio di istruzione `Imports`.  
  
     [!code-vb[VbXmlSamples#50](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-enable-xml-intell_2.vb)]  
  
#### Per importare uno spazio dei nomi XML per tutti i file in un progetto  
  
1.  Uno spazio dei nomi XML importato in un file di codice è valido solo per tale file di codice.  Per importare uno spazio dei nomi XML che sia valido per tutti i file di codice in un progetto, aprire Progettazione progetti facendo doppio clic su **Progetto** in **Esplora soluzioni**.  
  
2.  Nella scheda **Riferimenti**, nella casella **Spazi dei nomi importati** digitare lo spazio dei nomi XML di destinazione nel formato di una dichiarazione dello spazio dei nomi XML completa \(ad esempio, `<xmlns: ns="http://sampleNamespace">`\).  Se lo spazio dei nomi XML di destinazione non specifica un prefisso dello spazio dei nomi, lo spazio dei nomi sarà lo spazio dei nomi XML predefinito per il progetto.  
  
3.  Fare clic su **Aggiungi importazione utente**.  
  
## Vedere anche  
 [Imports Statement \(XML Namespace\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)   
 [XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)
---
title: 'Procedura: abilitare IntelliSense XML in Visual Basic | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- XML IntelliSense [Visual Basic]
- XML [Visual Basic], IntelliSense
- IntelliSense [Visual Basic], XML
ms.assetid: af67d0ee-a4a6-4abf-9c07-5a8cfe80d111
caps.latest.revision: 25
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 84af19189fa3fc510c8d4f8e408cbb2a393d8b8f
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-enable-xml-intellisense-in-visual-basic"></a>Procedura: abilitare IntelliSense XML in Visual Basic
IntelliSense XML in Visual Basic consente il completamento di word per gli elementi definiti in uno schema XML. Per abilitare IntelliSense XML in Visual Basic, è necessario eseguire le operazioni seguenti:  
  
1.  Ottenere i file XML schema (XSD) per i file XML che l'applicazione dovrà leggere o scrivere.  
  
2.  Includere i file di schema XML nel progetto.  
  
3.  Importare la destinazione dello spazio dei nomi o spazi dei nomi in un progetto o del file di codice. Uno spazio dei nomi di destinazione è identificato dal `targetNamespace` o `tns` dello schema XSD.  
  
     Per importare uno spazio dei nomi di destinazione, utilizzare il `Imports` istruzione oppure aggiungere uno spazio dei nomi per tutti i file di codice in un progetto usando il **riferimenti** pagina di progettazione.  
  
 Per ulteriori informazioni sulle funzionalità di IntelliSense XML in Visual Basic, vedere [IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md). Per ulteriori informazioni sull'importazione di spazi dei nomi XML, vedere [istruzione Imports (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md) o [pagina riferimenti, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
 ![collegamento a video](../../../../visual-basic/programming-guide/language-features/xml/media/playvideo.gif "PlayVideo") per una versione video di questo argomento, vedere [procedura: abilitare IntelliSense XML in Visual Basic](http://go.microsoft.com/fwlink/?LinkId=102466). Per una dimostrazione video correlata, vedere [come posso abilitare IntelliSense XML e spazi dei nomi XML utilizzare?](http://go.microsoft.com/fwlink/?LinkId=143035).  
  
## <a name="enable-xml-intellisense-in-visual-basic"></a>Abilitare IntelliSense XML in Visual Basic  
 Se si dispone di un file XML ma che non è un file di schema XSD, in SP1 è possibile creare un file di schema XSD utilizzando il XML Schema Wizard. È inoltre possibile utilizzare l'inferenza dello schema nell'Editor XML di Visual Studio.  
  
#### <a name="to-create-an-xsd-schema-file-for-an-xml-file-by-using-the-xml-to-schema-wizard-requires-sp1"></a>Per creare un file di schema XSD per un file XML utilizzando il XML Schema Wizard (richiede SP1)  
  
1.  Nel progetto, fare clic su **Aggiungi nuovo elemento** sul **progetto** menu.  
  
2.  Selezionare il **Xml in Schema** modello di elemento da una di **dati** o **elementi comuni** categorie dei modelli.  
  
3.  Specificare un nome di file per i file XSD che verranno archiviati in set di schemi derivati e quindi fare clic su **Aggiungi**.  
  
4.  Nel **del set di schemi XML dedurre da documenti XML** finestra, aggiungere uno o più documenti XML per dedurre lo schema XML da impostare.  
  
    -   Per aggiungere i file di testo che contengono documenti XML mediante Esplora File, fare clic su **Aggiungi da File**.  
  
    -   Per aggiungere un documento XML da un indirizzo HTTP, fare clic su **Aggiungi da Web**.  
  
    -   Per copiare o digitare il contenuto di un documento XML nella procedura guidata, fare clic su **digitare o incollare XML**.  
  
5.  Quando specificate tutte le origini di documento XML da cui dedurre il set di schemi XML, fare clic su **OK** di inferire lo schema XML impostato. Il set di schemi viene salvato nella cartella del progetto in uno o più file XSD. (Per ogni spazio dei nomi XML nello schema, viene creato un file.)  
  
#### <a name="to-create-an-xsd-schema-file-for-an-xml-file-by-using-schema-inference-in-the-visual-studio-xml-editor"></a>Per creare un file di schema XSD per un file XML con l'inferenza dello schema nell'Editor XML di Visual Studio  
  
1.  Modificare il file XML in Progettazione XML di Visual Studio.  
  
2.  Quando il cursore è posizionato all'interno del file XML, il **XML** verrà visualizzato il menu. Fare clic su **Create Schema** sul **XML** menu. Viene creato un file XSD dallo schema XSD dedotto dal file XML.  
  
3.  Salvare il file di schema XSD.  
  
    > [!NOTE]
    >  Schemi XSD diversi potrebbero essere dedotto da più documenti XML che devono avere lo stesso schema. Ciò può verificarsi quando vengono trovati determinati elementi e attributi in un file XML e non in un'altra o quando sono inclusi elementi in ordine diverso, ad esempio. Quando si utilizza l'inferenza dello schema XSD, è necessario rivedere gli schemi XSD derivati per completezza e accuratezza.  
  
#### <a name="to-include-an-xsd-schema-file"></a>Per includere un file di schema XSD  
  
-   Per impostazione predefinita, è possibile vedere i file XSD nei progetti Visual Basic. Se il file XSD è già incluso nelle cartelle per il progetto, fare clic su di **Mostra tutti i file** pulsante **Esplora**. Individuare il file XSD in **Esplora**, il file e fare clic su **includere File nel progetto**.  
  
-   Se il file XSD non è già parte del progetto, in **Esplora soluzioni**, fare clic sulla cartella in cui si desidera archiviare il file XSD, scegliere **Aggiungi**, quindi fare clic su **elemento esistente**. Individuare il file XSD e quindi fare clic su **Aggiungi**.  
  
#### <a name="to-import-an-xml-namespace-in-a-code-file"></a>Per importare uno spazio dei nomi XML in un file di codice  
  
1.  Identificare lo spazio dei nomi di destinazione dallo schema XSD.  
  
2.  All'inizio del file di codice, aggiungere un `Imports` istruzione per lo spazio dei nomi XML destinazione, come illustrato nell'esempio seguente.  
  
     [!code-vb[VbXMLSamples n.&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-enable-xml-intellisense_1.vb)]  
  
     Per importare uno spazio dei nomi XML come spazio dei nomi predefinito, ovvero lo spazio dei nomi che viene applicato agli elementi XML e attributi che non hanno un prefisso dello spazio dei nomi, aggiungere un `Imports` istruzione per lo spazio dei nomi XML predefinito di destinazione. Non specificare un prefisso dello spazio dei nomi. Di seguito è riportato un esempio di un `Imports` istruzione.  
  
     [!code-vb[&#50; VbXmlSamples](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-enable-xml-intellisense_2.vb)]  
  
#### <a name="to-import-an-xml-namespace-for-all-files-in-a-project"></a>Per importare uno spazio dei nomi XML per tutti i file in un progetto  
  
1.  Uno spazio dei nomi XML importato in un file di codice si applica solo tale file di codice. Per importare uno spazio dei nomi XML che si applica a tutti i file di codice in un progetto, aprire la finestra Progettazione progetti facendo doppio clic su **progetto** in **Esplora**.  
  
2.  Nel **riferimenti** nella scheda il **spazi dei nomi importati** digitare lo spazio dei nomi XML sotto forma di una dichiarazione dello spazio dei nomi XML completa (ad esempio, `<xmlns: ns="http://sampleNamespace">`). Se lo spazio dei nomi XML non specifica un prefisso dello spazio dei nomi, lo spazio dei nomi sarà lo spazio dei nomi XML predefinito per il progetto.  
  
3.  Fare clic su **Aggiungi importazione utente**.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Imports (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Riferimenti (pagina), Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)   
 [IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)


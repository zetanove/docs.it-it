---
title: XML per la procedura guidata Schema (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vb.XmlToSchemaWizard
dev_langs:
- VB
helpviewer_keywords:
- XML IntelliSense [Visual Basic]
- XML [Visual Basic], IntelliSense
- IntelliSense [Visual Basic], XML
- XML schemas, creating
ms.assetid: 98c495ba-8f37-4517-a0db-aa738611ab76
caps.latest.revision: 16
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d0c9c0247f3d9934ef973c7322cb098f9b445a5a
ms.lasthandoff: 03/13/2017

---
# <a name="xml-to-schema-wizard-visual-basic"></a>Procedura guidata XML in schema (Visual Basic)
Utilizzare il codice XML Schema guidata per creare un set di schemi XML che viene dedotto da uno o più documenti XML e includerlo nel progetto. È possibile utilizzare qualsiasi combinazione di documenti XML sotto forma di file di testo, XML provenienti da indirizzi HTTP Internet o XML che viene digitato o incollato nel XML Schema guidata.  
  
 Schemi XML vengono utilizzati per fornire IntelliSense per le proprietà XML in Visual Basic. Per ulteriori informazioni, vedere [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md) e [IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md).  
  
> [!NOTE]
>  Prima di eseguire il codice XML per una procedura guidata Schema, si consiglia di rimuovere i file XSD esistenti dal progetto che in precedenza sono stati generati dalla procedura guidata. La deduzione di un set di schemi XML che corrisponde a un set di schemi esistente, può verificarsi un conflitto e [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non sarà in grado di fornire IntelliSense per le proprietà XML.  
  
 XML Schema guidata utilizza la <xref:System.Xml.Schema.XmlSchemaInference>classe per creare lo schema per il XML fornito.</xref:System.Xml.Schema.XmlSchemaInference> Di conseguenza, è possibile creare più file di schema per il set di schemi. Per ogni spazio dei nomi XML nel codice XML fornito, viene creato un file Extensible Schema Definition (XSD). Per ulteriori informazioni, vedere il <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A>(metodo).</xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A>  
  
 Per accedere a XML Schema guidata, fare clic su **Aggiungi nuovo elemento** sul **progetto** menu e aggiungere un **XML in Schema** modello presente la **dati** o **elementi comuni** gruppo di modelli. Dopo che sono state incluse tutte le origini di documento XML per dedurre il set di schemi XML da, fare clic su **OK** per creare lo schema inferito set.  
  
 **Tipo di origine**  
 Questa colonna viene visualizzato il tipo di origine del documento XML: **File**, **URL**, o **XML**.  
  
 **Percorso del documento XML**  
 Questa colonna viene visualizzato il percorso del documento XML. Per i documenti XML digitati o incollati viene visualizzato il contenuto del documento XML.  
  
 **Aggiungi da File**  
 Fare clic su questo pulsante per aggiungere file di documento XML mediante Esplora File.  
  
 **Aggiungere da Web**  
 Fare clic su questo pulsante per fornire l'indirizzo HTTP di un documento XML.  
  
 **Digitare o incollare il XML**  
 Fare clic su questo pulsante per digitare o incollare un documento XML nella finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Schema.XmlSchemaInference></xref:System.Xml.Schema.XmlSchemaInference>   
 [IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)

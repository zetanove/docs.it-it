---
title: "XML to Schema Wizard (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlToSchemaWizard"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML IntelliSense [Visual Basic]"
  - "XML [Visual Basic], IntelliSense"
  - "IntelliSense [Visual Basic], XML"
  - "XML schemas, creating"
ms.assetid: 98c495ba-8f37-4517-a0db-aa738611ab76
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# XML to Schema Wizard (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Utilizzare la procedura guidata XML in schema per creare un insieme dello schema XML dedotto da uno o più documenti XML e includerlo nel progetto.  È possibile utilizzare qualsiasi combinazione di documenti XML sotto forma di file di testo, XML da indirizzi Internet HTTP o XML digitato o incollato nella procedura guidata XML in schema.  
  
 Gli schemi XML consentono di fornire IntelliSense per le proprietà XML in Visual Basic.  Per ulteriori informazioni, vedere [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md) e [XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md).  
  
> [!NOTE]
>  Prima di eseguire la procedura guidata XML in schema, si consiglia di rimuovere dal progetto eventuali file XSD esistenti generati in precedenza dalla procedura guidata.  La deduzione di un insieme dello schema XML corrispondente a un insieme dello schema esistente può dare luogo a un conflitto e impedire a [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] di fornire IntelliSense per le proprietà XML.  
  
 La procedura guidata XML in schema utilizza la classe <xref:System.Xml.Schema.XmlSchemaInference> per creare lo schema per l'XML fornito.  Di conseguenza, è possibile che vengano creati più file di schema per l'insieme dello schema.  Viene creato un file XSD \(Extensible Schema Definition\) per ogni spazio dei nomi XML nell'XML fornito.  Per ulteriori informazioni, vedere il metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A>.  
  
 Per accedere alla procedura guidata XML in schema, scegliere **Aggiungi nuovo elemento** dal menu **Progetto** e aggiungere un modello **XML in schema** dal gruppo di modelli **Dati** o **Elementi comuni**.  Una volta specificate tutte le origini di documento XML da cui dedurre l'insieme dello schema XML, scegliere **OK** per procedere.  
  
 **Tipo di origine**  
 In questa colonna viene visualizzato il tipo di origine del documento XML: **File**, **URL** o **XML**.  
  
 **Percorso dei documenti XML**  
 In questa colonna viene visualizzato il percorso dei documenti XML.  Per i documenti XML digitati o incollati viene visualizzato il relativo contenuto.  
  
 **Aggiungi da file**  
 Fare clic su questo pulsante per aggiungere i file di documenti XML utilizzando Esplora file.  
  
 **Aggiungere da Web**  
 Fare clic su questo pulsante per fornire l'indirizzo HTTP di un documento XML.  
  
 **Digita o incolla XML**  
 Fare clic su questo pulsante per digitare o incollare un documento XML nella finestra di dialogo.  
  
## Vedere anche  
 <xref:System.Xml.Schema.XmlSchemaInference>   
 [XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)
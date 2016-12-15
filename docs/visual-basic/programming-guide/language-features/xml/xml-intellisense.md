---
title: "XML IntelliSense in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, XML"
  - "XML IntelliSense [Visual Basic]"
  - "XML [Visual Basic], IntelliSense"
  - "IntelliSense [Visual Basic], XML"
ms.assetid: 59506ce9-d64e-417e-90fc-e9fe19f0a8fa
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML IntelliSense in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'editor di codice Visual Basic include funzionalità IntelliSense per XML che forniscono il completamento delle parole per gli elementi definiti in uno schema XML.  Se si include un file di definizione schema \(XML Schema Definition\) nel progetto e si importa lo spazio dei nomi di destinazione dello schema utilizzando l'istruzione `Imports`, l'editor di codice includerà elementi dallo schema XSD nell'elenco IntelliSense di variabili membro valide per gli oggetti <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XDocument>.  Nella figura seguente viene illustrato l'elenco dei membri IntelliSense per un oggetto <xref:System.Xml.Linq.XElement>.  
  
 ![IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/media/xml_intellisense.png "XML\_Intellisense")  
IntelliSense XML  
  
## Abilitare IntelliSense XML in Visual Basic  
 Per abilitare IntelliSense XML in Visual Basic è necessario includere un file di schema XSD nel progetto Visual Basic..  È necessario importare anche lo spazio dei nomi di destinazione per lo schema XSD nel file di codice utilizzando l'istruzione `Imports`.  In alternativa, è possibile aggiungere lo spazio dei nomi di destinazione all'elenco dello spazio dei nomi a livello di progetto utilizzando la pagina **Riferimenti** di Progettazione progetti di Visual Basic .  Per i relativi esempi, vedere [How to: Enable XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md).  Per ulteriori informazioni, vedere°[Imports Statement \(XML Namespace\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md) e [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic).  
  
 Notare che per impostazione predefinita non è possibile vedere i file di schema XSD nei progetti di Visual Basic..  È necessario fare clic sul pulsante **Mostra tutti i file** per selezionare un file XSD da includere nel progetto.  
  
### Generazione di un file di schema \(inferenza di schemi\)  
 È possibile creare uno schema XSD per un file XML esistente derivando lo schema XSD tramite gli strumenti XML di Visual Studio.  
  
-   A partire dal Service Pack 1 è possibile utilizzare la procedura guidata XML in schema per creare un insieme dello schema XML dedotto da uno o più documenti XML e includerlo nel progetto.  È possibile utilizzare qualsiasi combinazione di documenti XML sotto forma di file di testo, XML da indirizzi Internet HTTP o XML digitato o incollato nella procedura guidata XML in schema.  Per accedere alla procedura guidata XML in schema, scegliere **Aggiungi nuovo elemento** dal menu **Progetto** e aggiungere un modello **XML in schema** dal gruppo di modelli **Dati** o **Elementi comuni**.  Una volta specificate tutte le origini di documento XML da cui dedurre l'insieme dello schema XML, scegliere **OK** per procedere.  Per ulteriori informazioni, vedere [XML to Schema Wizard](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md).  
  
-   È inoltre possibile utilizzare l'editor XML di Visual Studio per dedurre un insieme dello schema XSD da un file XML.  Per creare un insieme dello schema XML mediante l'editor XML, aprire un file XML in Progettazione XML di Visual Studio e quindi fare clic su **Crea schema** nel menu **XML**.  Una volta creato l'insieme dello schema XSD, è possibile salvarlo in uno o più file XSD e includere i file nel progetto.  Per ulteriori informazioni, vedere la classe [How to: Enable XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md).  
  
 Si noti che da documenti XML multipli che dovrebbero avere lo stesso schema potrebbero venire dedotti insiemi degli schemi XSD diversi.  Ciò può verificarsi, ad esempio, quando certi attributi ed elementi sono presenti in un file XML ma non in un altro, oppure quando gli elementi sono inclusi in ordine diverso.  Quando si utilizza l'inferenza di schemi XSD è necessario verificare la completezza e l'accuratezza degli insiemi degli schemi XSD dedotti.  
  
## Elenco membri  
 Dopo aver digitato un punto \(.\) per delimitare un'istanza di un oggetto <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument> \(oppure un'istanza di `IEnumerable(Of XElement)` o `IEnumerable(Of XDocument)`\) IntelliSense di Visual Basic visualizza un elenco di possibili membri dell'oggetto.  L'elenco iniziale include tre opzioni che rappresentano le proprietà axis XML, come descritto nell'elenco seguente.  
  
|||  
|-|-|  
|Opzione|Descrizione|  
|**\< \>**|Selezionare questa opzione per visualizzare un elenco di possibili elementi figlio.  Per ulteriori informazioni, vedere [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) e il metodo <xref:System.Xml.Linq.XContainer.Elements%2A>.|  
|**@**|Selezionare questa opzione per visualizzare un elenco di possibili attributi.  Per ulteriori informazioni, vedere [XML Axis Properties](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md). Questa opzione è disponibile solo per oggetti di tipo <xref:System.Xml.Linq.XElement>.|  
|**…\< \>**|Selezionare questa opzione per visualizzare un elenco di possibili elementi discendenti.  Per ulteriori informazioni, vedere [How to: Access XML Descendant Elements](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md) e il metodo <xref:System.Xml.Linq.XContainer.Elements%2A>.|  
  
 Selezionare o iniziare a digitare una qualsiasi delle opzioni XML dell'elenco.  L'elenco dei membri visualizzerà quindi membri potenziali dallo schema XML che sono specifici all'opzione selezionata.  Se si dispone di spazi dei nomi XML importati che sono associati a un prefisso dello spazio dei nomi XML specifico, nell'elenco dei membri viene incluso un elenco di prefissi dello spazio dei nomi XML potenziali.  
  
 Si consideri ad esempio il seguente schema XSD:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema attributeFormDefault="unqualified"   
           elementFormDefault="qualified"   
           targetNamespace="http://SamplePurchaseOrder"   
           xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="PurchaseOrders">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="PurchaseOrder">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="Address" />  
              <xs:element name="Items" />  
              <xs:element name="Comment" />  
            </xs:sequence>  
            <xs:attribute name="PurchaseOrderNumber" type="xs:unsignedShort" use="required" />  
            <xs:attribute name="OrderDate" type="xs:string" use="required" />  
          </xs:complexType>  
        </xs:element>  
      </xs:sequence>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 L'XML valido per lo schema XSD sarà simile a questo.  
  
```  
<?xml version="1.0"?>  
<PurchaseOrders xmlns="http://SamplePurchaseOrder">  
  <PurchaseOrder PurchaseOrderNumber="12345" OrderDate="2000-1-1">  
    <Address />  
    <Items />  
    <Comment />  
  </PurchaseOrder>  
</PurchaseOrders>  
```  
  
 Se si include questo file di schema XSD in un progetto e si importa lo spazio dei nomi di destinazione dallo schema XSD nel file di codice o nel progetto, IntelliSense di Visual Basic visualizza i membri dallo schema durante la digitazione del codice Visual Basic.  Se lo spazio dei nomi di destinazione per lo schema XSD viene importato come spazio dei nomi predefinito e si digitano i seguenti elementi, IntelliSense visualizza un elenco di possibili elementi figlio per l'elemento XML `PurchaseOrder`.  
  
```  
Dim po = <PurchaseOrder />  
po.<  
```  
  
 L'elenco è costituito da elementi Indirizzo, Commento ed Elementi.  
  
### Livelli di certezza per gli elementi dell'elenco IntelliSense  
 La determinazione del tipo XSD da utilizzare per IntelliSense non può avvenire in modo completamente esatto.  Di conseguenza, IntelliSense XML spesso visualizza un elenco espanso di possibili membri.  Per facilitare la scelta di un elemento dall'elenco membri di IntelliSense, gli elementi vengono visualizzati con un'indicazione del livello di certezza che IntelliSense XML attribuisce a un particolare membro.  
  
 A volte IntelliSense XML può identificare un tipo specifico dallo schema XSD.  In tali casi, vengono visualizzati i possibili elementi figlio, gli attributi, o gli elementi discendenti per quel tipo XSD con un livello di certezza alto.  Questi elementi sono identificati con un segno di spunta.  
  
 Tuttavia, altre volte IntelliSense XML non è in grado di identificare un tipo specifico dallo schema XSD.  In questo caso viene visualizzato un elenco espanso di possibili elementi figlio, attributi o elementi discendenti dallo schema XSD per il progetto, con un livello di certezza basso.  Questi elementi sono identificati con un punto interrogativo.  
  
## Vedere anche  
 [How to: Enable XML IntelliSense in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)   
 [XML to Schema Wizard](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md)   
 [Imports Statement \(XML Namespace\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Attribute Axis Property](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)   
 [XML Descendant Axis Property](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)   
 [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)
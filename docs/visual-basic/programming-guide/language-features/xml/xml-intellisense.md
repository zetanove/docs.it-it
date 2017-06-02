---
title: IntelliSense XML in Visual Basic | Documenti di Microsoft
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
- Visual Basic code, XML
- XML IntelliSense [Visual Basic]
- XML [Visual Basic], IntelliSense
- IntelliSense [Visual Basic], XML
ms.assetid: 59506ce9-d64e-417e-90fc-e9fe19f0a8fa
caps.latest.revision: 27
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
ms.openlocfilehash: 8c43db3d2010e4fa92eebeec8a973c50052b1340
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="xml-intellisense-in-visual-basic"></a>IntelliSense XML in Visual Basic
L'Editor di codice Visual Basic include funzionalità di IntelliSense per XML che forniscono il completamento delle parole per gli elementi definiti in uno schema XML. Se si include un file XML Schema Definition (XSD) nel progetto e importare lo spazio dei nomi di destinazione dello schema utilizzando il `Imports` istruzione, l'Editor di codice includerà elementi dallo schema XSD nell'elenco IntelliSense di variabili membro valide per <xref:System.Xml.Linq.XElement>e <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> La figura seguente mostra l'elenco dei membri di IntelliSense per un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement>  
  
 ![IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/media/xml_intellisense.png "XML_Intellisense")  
IntelliSense XML  
  
## <a name="enabling-xml-intellisense-in-visual-basic"></a>L'abilitazione di IntelliSense XML in Visual Basic  
 Per abilitare IntelliSense XML in Visual Basic, è necessario includere un file di schema XSD nel progetto di Visual Basic. È inoltre necessario importare lo spazio dei nomi di destinazione per lo schema XSD nel file di codice utilizzando il `Imports` istruzione. In alternativa, è possibile aggiungere lo spazio dei nomi all'elenco di nomi a livello di progetto utilizzando il **riferimenti** pagina della finestra di progettazione di progetto Visual Basic. Per esempi, vedere [procedura: abilitare IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md). Per ulteriori informazioni, vedere [istruzione Imports (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md) e [pagina riferimenti, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic).  
  
 Si noti che per impostazione predefinita è possono vedere i file di schema XSD nei progetti Visual Basic. È necessario scegliere il **Mostra tutti i file** per selezionare un file XSD da includere nel progetto.  
  
### <a name="generating-a-schema-file-schema-inference"></a>Generazione di un File di Schema (inferenza dello Schema)  
 È possibile creare uno schema XSD per un file XML esistente per l'inferenza dello schema XSD utilizzando gli strumenti XML di Visual Studio.  
  
-   A partire da SP1, è possibile utilizzare il codice XML Schema guidata per creare un set di XML Schema che viene dedotto da uno o più documenti XML e includerlo nel progetto. È possibile utilizzare qualsiasi combinazione di documenti XML sotto forma di file di testo, XML provenienti da indirizzi HTTP Internet o XML che viene digitato o incollato nel XML Schema guidata. Per accedere a XML Schema guidata, fare clic su **Aggiungi nuovo elemento** sul **progetto** menu e aggiungere un **XML in Schema** modello presente la **dati** o **elementi comuni** gruppo di modelli. Dopo che sono state incluse tutte le origini di documento XML per dedurre il set di XML Schema da, fare clic su **OK** per creare lo schema inferito set. Per ulteriori informazioni, vedere [procedura guidata Schema XML in](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md).  
  
-   È inoltre possibile utilizzare l'Editor XML di Visual Studio per inferire uno schema XSD impostato da un file XML. Per creare un insieme utilizzando l'Editor XML dello schema XML, aprire un file XML in Progettazione XML di Visual Studio e quindi fare clic su **Create Schema** sul **XML** menu. Dopo aver creato il set di schemi XSD, è possibile salvare il set di schema creato in uno o più file XSD e includerli nel progetto. Per ulteriori informazioni, vedere[procedura: abilitare IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md).  
  
 Si noti che nel set di schemi XSD diversi potrà essere dedotto da più documenti XML che devono avere lo stesso schema. Ciò può verificarsi quando vengono trovati determinati elementi e attributi in un file XML e non in un'altra o quando sono inclusi elementi in ordine diverso, ad esempio. Quando si utilizza l'inferenza dello schema XSD, è opportuno esaminare derivato nel set di schemi XSD per completezza e accuratezza.  
  
## <a name="member-list"></a>Elenco dei membri  
 Dopo aver digitato un punto (.) per delimitare un'istanza di un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>oggetto (o un'istanza di `IEnumerable(Of XElement)` o `IEnumerable(Of XDocument)`), IntelliSense di Visual Basic viene visualizzato un elenco di membri dell'oggetto possibili.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> L'elenco iniziale include tre opzioni che rappresentano le proprietà axis XML, come descritto nell'elenco seguente.  
  
|Opzione|Descrizione|  
|---|---|  
|**\< >**|Selezionare questa opzione per visualizzare un elenco di possibili figlio di elementi. Per ulteriori informazioni, vedere [letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) e <xref:System.Xml.Linq.XContainer.Elements%2A>metodo.</xref:System.Xml.Linq.XContainer.Elements%2A>|  
|**@**|Selezionare questa opzione per visualizzare un elenco di attributi possibili. Per ulteriori informazioni, vedere [proprietà Axis XML](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md). Questa opzione è disponibile solo per gli oggetti di tipo <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>|  
|**…\< >**|Selezionare questa opzione per visualizzare un elenco di possibili elementi discendenti. Per ulteriori informazioni, vedere [procedura: accedere agli elementi discendenti XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md) e <xref:System.Xml.Linq.XContainer.Elements%2A>metodo.</xref:System.Xml.Linq.XContainer.Elements%2A>|  
  
 Selezionare o digitare le opzioni XML dall'elenco. L'elenco dei membri visualizzerà quindi membri potenziali dallo schema XML che sono specifici dell'opzione selezionata. Se si dispone di spazi dei nomi XML importato associati a uno specifico prefisso dello spazio dei nomi XML, un elenco di potenziali prefissi di spazio dei nomi XML è incluso nell'elenco dei membri.  
  
 Ad esempio, si consideri il seguente schema XSD.  
  
```xml  
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
  
 XML valido per lo schema XSD sarà simile alla seguente.  
  
```xml  
<?xml version="1.0"?>  
<PurchaseOrders xmlns="http://SamplePurchaseOrder">  
  <PurchaseOrder PurchaseOrderNumber="12345" OrderDate="2000-1-1">  
    <Address />  
    <Items />  
    <Comment />  
  </PurchaseOrder>  
</PurchaseOrders>  
```  
  
 Se si include questo file di schema XSD in un progetto e importa lo spazio dei nomi di destinazione dallo schema XSD in un progetto o del file di codice, IntelliSense di Visual Basic Visualizza membri dallo schema durante la digitazione del codice Visual Basic. Se lo spazio dei nomi di destinazione per lo schema XSD viene importato come spazio dei nomi predefinito e si digita quanto segue, IntelliSense visualizza un elenco di possibili elementi figlio per il `PurchaseOrder` (elemento XML).  
  
```  
Dim po = <PurchaseOrder />  
po.<  
```  
  
 L'elenco è costituito da elementi di indirizzo, commento e gli elementi.  
  
### <a name="certainty-levels-for-intellisense-list-items"></a>Livelli di attendibilità per gli elementi dell'elenco di IntelliSense  
 Determinazione del tipo XSD da utilizzare per IntelliSense non è esatta. Di conseguenza, IntelliSense XML spesso Visualizza un elenco di possibili membri espanso. Per facilitare la selezione di un elemento dall'elenco dei membri IntelliSense, gli elementi vengono visualizzati con l'indicazione del livello di certezza che dispone di IntelliSense XML per un particolare membro.  
  
 A volte IntelliSense XML può identificare un tipo specifico dallo schema XSD. In questi casi, verrà visualizzato possibili elementi figlio, attributi o gli elementi discendenti di tale tipo XSD con un elevato livello di attendibilità. Questi elementi vengono identificati con un segno di spunta.  
  
 Tuttavia, a volte IntelliSense XML non è in grado di identificare un tipo specifico dallo schema XSD. In questi casi, visualizzerà un elenco espanso di possibili elementi figlio, attributi o elementi discendenti dallo schema XSD per il progetto con un livello di certezza basso. Questi elementi vengono identificati con un punto interrogativo.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: abilitare IntelliSense XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)   
 [Procedura guidata Schema XML in](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md)   
 [Istruzione Imports (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Valore letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Proprietà axis dell'attributo XML](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)   
 [Proprietà Axis Descendant XML](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)   
 [Pagina Riferimenti, Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)

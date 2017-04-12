---
title: Contenuto valido di XElement e XDocument Objects2 | Documenti di Microsoft
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
ms.assetid: 400bb692-478a-40b6-ac1b-4ccbb4cbbd02
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f752ae346167709b95e758d15c1785ba7b6fcc5f
ms.lasthandoff: 03/13/2017

---
# <a name="valid-content-of-xelement-and-xdocument-objects"></a>Contenuto valido di oggetti XElement e XDocument
In questo argomento vengono illustrati gli argomenti validi che è possibile passare a costruttori e i metodi usati per aggiungere contenuto a elementi e documenti.  
  
## <a name="valid-content"></a>Contenuto valido  
 Le query spesso restituiscono <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>o <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XAttribute>.</xref:System.Xml.Linq.XAttribute> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> È possibile passare raccolte di <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XAttribute>gli oggetti per il <xref:System.Xml.Linq.XElement>costruttore.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> Pertanto è comodo passare i risultati di una query come contenuto in metodi e costruttori usati per popolare alberi XML.  
  
 Quando si aggiunge contenuto semplice, è possibile passare diversi tipi a questo metodo. I tipi validi sono i seguenti:  
  
-   <xref:System.String></xref:System.String>  
  
-   <xref:System.Double></xref:System.Double>  
  
-   <xref:System.Single></xref:System.Single>  
  
-   <xref:System.Decimal></xref:System.Decimal>  
  
-   <xref:System.Boolean></xref:System.Boolean>  
  
-   <xref:System.DateTime></xref:System.DateTime>  
  
-   <xref:System.TimeSpan></xref:System.TimeSpan>  
  
-   <xref:System.DateTimeOffset></xref:System.DateTimeOffset>  
  
-   Qualsiasi tipo che implementa `Object.ToString`.  
  
-   Qualsiasi tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>.</xref:System.Collections.Generic.IEnumerable%601>  
  
 Quando si aggiunge contenuto complesso, è possibile passare diversi tipi a questo metodo:  
  
-   <xref:System.Xml.Linq.XObject></xref:System.Xml.Linq.XObject>  
  
-   <xref:System.Xml.Linq.XNode></xref:System.Xml.Linq.XNode>  
  
-   <xref:System.Xml.Linq.XAttribute>  
  
-   Qualsiasi tipo che implementa<xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>  
  
 Se un oggetto implementa <xref:System.Collections.Generic.IEnumerable%601>, la raccolta nell'oggetto viene enumerata e vengono aggiunti tutti gli elementi nella raccolta.</xref:System.Collections.Generic.IEnumerable%601> Se la raccolta contiene <xref:System.Xml.Linq.XNode>o <xref:System.Xml.Linq.XAttribute>oggetti, ogni elemento nella raccolta viene aggiunto separatamente.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XNode> Se la raccolta contiene testo (oppure oggetti convertiti in testo), il testo della raccolta viene concatenato e aggiunto come un unico nodo di tipo text.  
  
 Se il contenuto è `null`, non viene aggiunto nulla. Quando si passa una raccolta, gli elementi della raccolta possono essere `null`. Un elemento `null` della raccolta non ha effetto sull'albero.  
  
 Un attributo aggiunto deve includere un nome univoco nell'elemento che lo contiene.  
  
 Quando si aggiunge <xref:System.Xml.Linq.XNode>o <xref:System.Xml.Linq.XAttribute>oggetti, se il nuovo contenuto non ha elementi padre, quindi gli oggetti vengono semplicemente collegati all'albero XML.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XNode> Se invece il nuovo contenuto include già elementi padre e fa parte di un altro albero XML, viene duplicato e quindi collegato all'albero XML.  
  
## <a name="valid-content-for-documents"></a>Contenuto valido per documenti  
 Non è possibile aggiungere attributi e contenuto semplice a un documento.  
  
 Non sono presenti molti scenari che è necessario creare un <xref:System.Xml.Linq.XDocument>.</xref:System.Xml.Linq.XDocument> Al contrario, in genere è possibile creare strutture ad albero XML con un <xref:System.Xml.Linq.XElement>nodo radice.</xref:System.Xml.Linq.XElement> A meno che non si dispone di un requisito specifico per creare un documento (ad esempio perché è necessario creare istruzioni di elaborazione e commenti al primo livello o supportare tipi di documento), è spesso più conveniente utilizzare <xref:System.Xml.Linq.XElement>come nodo radice.</xref:System.Xml.Linq.XElement>  
  
 Il contenuto valido per un documento è il seguente:  
  
-   Zero o uno <xref:System.Xml.Linq.XDocumentType>oggetti.</xref:System.Xml.Linq.XDocumentType> I tipi di documento devono essere inseriti prima dell'elemento.  
  
-   Zero o un elemento.  
  
-   Zero o più commenti.  
  
-   Zero o più istruzioni di elaborazione.  
  
-   Zero o più nodi di tipo text che contengono solo spazi vuoti.  
  
## <a name="constructors-and-functions-that-allow-adding-content"></a>Costruttori e funzioni che consentono l'aggiunta di contenuto  
 I metodi seguenti consentono di aggiungere contenuto figlio a un <xref:System.Xml.Linq.XElement>o un <xref:System.Xml.Linq.XDocument>:</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.%23ctor%2A></xref:System.Xml.Linq.XElement.%23ctor%2A>|Costruisce un <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XDocument.%23ctor%2A></xref:System.Xml.Linq.XDocument.%23ctor%2A>|Costruisce un <xref:System.Xml.Linq.XDocument>.</xref:System.Xml.Linq.XDocument>|  
|<xref:System.Xml.Linq.XContainer.Add%2A></xref:System.Xml.Linq.XContainer.Add%2A>|Aggiunge alla fine del contenuto figlio <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A></xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Aggiunge contenuto dopo la <xref:System.Xml.Linq.XNode>.</xref:System.Xml.Linq.XNode>|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A></xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Aggiunge contenuto prima di <xref:System.Xml.Linq.XNode>.</xref:System.Xml.Linq.XNode>|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A></xref:System.Xml.Linq.XContainer.AddFirst%2A>|Aggiunge contenuto all'inizio del contenuto figlio dell'elemento <xref:System.Xml.Linq.XContainer>.</xref:System.Xml.Linq.XContainer>|  
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A></xref:System.Xml.Linq.XElement.ReplaceAll%2A>|Sostituisce tutto il contenuto (nodi figlio e attributi) di un <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A></xref:System.Xml.Linq.XElement.ReplaceAttributes%2A>|Sostituisce gli attributi di un <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A></xref:System.Xml.Linq.XContainer.ReplaceNodes%2A>|Sostituisce i nodi figlio con nuovo contenuto.|  
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A></xref:System.Xml.Linq.XNode.ReplaceWith%2A>|Sostituisce un nodo con nuovo contenuto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)

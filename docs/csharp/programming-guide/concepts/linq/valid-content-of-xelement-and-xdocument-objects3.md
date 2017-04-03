---
title: Contenuto valido di oggetti XElement e XDocument3 | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 0d253586-2b97-459f-b1a7-f30f38f3ed9f
caps.latest.revision: 5
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3db6b15d2b95016db0814f202143ec198425e2ad
ms.lasthandoff: 03/13/2017

---
# <a name="valid-content-of-xelement-and-xdocument-objects"></a>Contenuto valido di oggetti XElement e XDocument
In questo argomento vengono illustrati gli argomenti validi che è possibile passare a costruttori e i metodi usati per aggiungere contenuto a elementi e documenti.  
  
## <a name="valid-content"></a>Contenuto valido  
 Le query spesso restituiscono <xref:System.Collections.Generic.IEnumerable%601> di <xref:System.Xml.Linq.XElement> o <xref:System.Collections.Generic.IEnumerable%601> di <xref:System.Xml.Linq.XAttribute>. È possibile passare raccolte di oggetti <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XAttribute> al costruttore <xref:System.Xml.Linq.XElement>. Pertanto è comodo passare i risultati di una query come contenuto in metodi e costruttori usati per popolare alberi XML.  
  
 Quando si aggiunge contenuto semplice, è possibile passare diversi tipi a questo metodo. I tipi validi sono i seguenti:  
  
-   <xref:System.String>  
  
-   <xref:System.Double>  
  
-   <xref:System.Single>  
  
-   <xref:System.Decimal>  
  
-   <xref:System.Boolean>  
  
-   <xref:System.DateTime>  
  
-   <xref:System.TimeSpan>  
  
-   <xref:System.DateTimeOffset>  
  
-   Qualsiasi tipo che implementa `Object.ToString`.  
  
-   Qualsiasi tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>.  
  
 Quando si aggiunge contenuto complesso, è possibile passare diversi tipi a questo metodo:  
  
-   <xref:System.Xml.Linq.XObject>  
  
-   <xref:System.Xml.Linq.XNode>  
  
-   <xref:System.Xml.Linq.XAttribute>  
  
-   Qualsiasi tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>  
  
 Se un oggetto implementa <xref:System.Collections.Generic.IEnumerable%601>, la raccolta nell'oggetto viene enumerata e vengono aggiunti tutti gli elementi della raccolta. Se la raccolta contiene oggetti <xref:System.Xml.Linq.XNode> o <xref:System.Xml.Linq.XAttribute>, ogni elemento della raccolta viene aggiunto separatamente. Se la raccolta contiene testo (oppure oggetti convertiti in testo), il testo della raccolta viene concatenato e aggiunto come un unico nodo di tipo text.  
  
 Se il contenuto è `null`, non viene aggiunto nulla. Quando si passa una raccolta, gli elementi della raccolta possono essere `null`. Un elemento `null` della raccolta non ha effetto sull'albero.  
  
 Un attributo aggiunto deve includere un nome univoco nell'elemento che lo contiene.  
  
 Quando si aggiungono oggetti <xref:System.Xml.Linq.XNode> o <xref:System.Xml.Linq.XAttribute>, se il nuovo contenuto non ha un padre, gli oggetti vengono semplicemente collegati all'albero XML. Se invece il nuovo contenuto include già elementi padre e fa parte di un altro albero XML, viene duplicato e quindi collegato all'albero XML.  
  
## <a name="valid-content-for-documents"></a>Contenuto valido per documenti  
 Non è possibile aggiungere attributi e contenuto semplice a un documento.  
  
 Non sono molti gli scenari in cui è richiesta la creazione di un oggetto <xref:System.Xml.Linq.XDocument>. In genere, è invece possibile creare alberi XML con un nodo radice <xref:System.Xml.Linq.XElement>. A meno di particolari esigenze che richiedono la creazione di un documento, ad esempio perché è necessario creare istruzioni di elaborazione e commenti al primo livello o supportare tipi di documento, è consigliabile usare <xref:System.Xml.Linq.XElement> come nodo radice.  
  
 Il contenuto valido per un documento è il seguente:  
  
-   Zero o un oggetto <xref:System.Xml.Linq.XDocumentType>. I tipi di documento devono essere inseriti prima dell'elemento.  
  
-   Zero o un elemento.  
  
-   Zero o più commenti.  
  
-   Zero o più istruzioni di elaborazione.  
  
-   Zero o più nodi di tipo text che contengono solo spazi vuoti.  
  
## <a name="constructors-and-functions-that-allow-adding-content"></a>Costruttori e funzioni che consentono l'aggiunta di contenuto  
 I metodi seguenti consentono di aggiungere contenuto figlio a <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>:  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.%23ctor%2A>|Costruisce un oggetto <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XDocument.%23ctor%2A>|Costruisce un oggetto <xref:System.Xml.Linq.XDocument>.|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|Aggiunge alla fine del contenuto figlio di <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>.|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Aggiunge contenuto dopo <xref:System.Xml.Linq.XNode>.|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Aggiunge contenuto prima di <xref:System.Xml.Linq.XNode>.|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|Aggiunge contenuto all'inizio del contenuto figlio di <xref:System.Xml.Linq.XContainer>.|  
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A>|Sostituisce tutto il contenuto (nodi figlio e attributi) di un oggetto <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A>|Sostituisce gli attributi di <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A>|Sostituisce i nodi figlio con nuovo contenuto.|  
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A>|Sostituisce un nodo con nuovo contenuto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)

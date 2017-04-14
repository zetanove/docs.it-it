---
title: "Modello DOM (Document Object Model) XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b5e52844-4820-47c0-a61d-de2da33e9f54
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Modello DOM (Document Object Model) XML
La classe DOM \(Document Object Model\) XML è una rappresentazione in memoria di un documento XML.  Il modello DOM consente di leggere e modificare un documento XML a livello di codice.  Anche la classe **XmlReader** è in grado di leggere un documento XML, tuttavia essa fornisce un accesso non memorizzato nella cache, di tipo forward\-only e di sola lettura.  Questo significa che con **XmlReader** non sono disponibili funzionalità per la modifica dei valori di un attributo o del contenuto di un elemento, né per l'inserimento e la rimozione di nodi.  La modifica è la funzione primaria del DOM.  È il modo comune e strutturato in cui i dati XML vengono rappresentati nella memoria, sebbene i dati XML effettivi siano archiviati in modo lineare all'interno di un file o quando provengono da un altro oggetto.  Di seguito sono riportati i dati XML.  
  
## Input  
  
```  
<?xml version="1.0"?>  
  <books>  
    <book>  
        <author>Carson</author>  
        <price format="dollar">31.95</price>  
        <pubdate>05/01/2001</pubdate>  
    </book>  
    <pubinfo>  
        <publisher>MSPress</publisher>  
        <state>WA</state>  
    </pubinfo>  
  </books>   
```  
  
 Nella figura seguente viene illustrato come è strutturata la memoria quando questi dati XML vengono letti nella struttura del DOM.  
  
 ![Struttura del documento XML](../../../../docs/standard/data/xml/media/xml-to-domtree.gif "XML\_To\_DOMTree")  
Struttura del documento XML  
  
 All'interno della struttura del documento XML, ogni cerchio di questa figura rappresenta un nodo, denominato oggetto **XmlNode**,  che costituisce l'oggetto di base nell'albero DOM.  La classe **XmlDocument**, che estende **XmlNode**, supporta i metodi per l'esecuzione di operazioni sul documento nella sua totalità, ad esempio il caricamento del documento in memoria o il salvataggio del documento XML in un file.  **XmlDocument** costituisce inoltre un modo per visualizzare e modificare i nodi nell'intero documento XML.  **XmlNode** e **XmlDocument** sono stati entrambi migliorati dal punto di vista delle prestazioni e dell'usabilità e dispongono di metodi e proprietà per:  
  
-   Accedere e apportare modifiche ai nodi specifici del DOM, ad esempio ai nodi degli elementi, ai nodi di riferimento all'entità e così via.  
  
-   Recuperare interi nodi, oltre alle informazioni contenute nel nodo, quali il testo in un nodo di elemento.  
  
    > [!NOTE]
    >  Se la struttura e le funzionalità di modifica del DOM non sono richieste da un'applicazione, le classi **XmlReader** e **XmlWriter** forniscono un accesso al flusso XML non memorizzato nella cache e di tipo forward\-only.  Per altre informazioni, vedere <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter>.  
  
 Gli oggetti **Node** dispongono di un set di metodi e proprietà, oltre a caratteristiche di base ben definite.  Di seguito sono riportate alcune di queste caratteristiche.  
  
-   I nodi presentano un singolo nodo padre, ovvero quello al livello immediatamente superiore.  Gli unici nodi che non presentano nodi padre sono al livello radice del documento, in quanto si tratta dei nodi di primo livello contenenti il documento stesso e i frammenti di documento.  
  
-   La maggior parte dei nodi può presentare più nodi figlio, ovvero quelli al livello immediatamente inferiore.  Di seguito viene riportato un elenco di tipi di nodi che possono contenere nodi figlio.  
  
    -   **Documento**  
  
    -   **DocumentFragment**  
  
    -   **EntityReference**  
  
    -   **Elemento**  
  
    -   **Attributo**  
  
     I nodi **XmlDeclaration**, **Notation**, **Entity**, **CDATASection**, **Text**, **Comment**, **ProcessingInstruction**  e **DocumentType** non contengono nodi figlio.  
  
-   I nodi che si trovano allo stesso livello, rappresentati nel diagramma dai nodi **book** e **pubinfo,** sono nodi di pari livello.  
  
 Una caratteristica del DOM è rappresentata dalla gestione degli attributi.  Gli attributi non sono nodi che fanno parte delle relazioni tra nodi padre, nodi figlio o nodi di pari livello,  ma sono considerati una proprietà del nodo dell'elemento e sono costituiti da una coppia composta da nome e valore.  Se, ad esempio, si dispone di dati XML costituiti da `format="dollar`" associato all'elemento `price`, il termine `format` è il nome, mentre il valore dell'attributo `format` è `dollar`.  Per recuperare l'attributo `format="dollar"` del nodo **price**, è necessario chiamare il metodo **GetAttribute** quando il cursore si trova in corrispondenza del nodo dell'elemento `price`.  Per altre informazioni, vedere [Accesso agli attributi nel DOM](../../../../docs/standard/data/xml/accessing-attributes-in-the-dom.md).  
  
 Man mano che l'XML viene letto in memoria, vengono creati dei nodi.  Non tutti i nodi, tuttavia, sono dello stesso tipo.  Le regole e la sintassi di un elemento dell'XML sono diverse da quelle di un'istruzione di elaborazione.  Pertanto, mentre avviene la lettura di vari dati, viene assegnato un tipo di nodo a ogni nodo.  In base al tipo di nodo, vengono determinate le caratteristiche e la funzionalità del nodo.  
  
 Per altre informazioni sui tipi di nodi generati in memoria, vedere [Tipi di nodi XML](../../../../docs/standard/data/xml/types-of-xml-nodes.md).  Per altre informazioni sugli oggetti creati nell'albero dei nodi, vedere [Mapping della gerarchia di oggetti in dati XML](../../../../docs/standard/data/xml/mapping-the-object-hierarchy-to-xml-data.md).  
  
 Le API disponibili nelle raccomandazioni W3C DOM Level 1 e Level 2 sono state estese per facilitare l'uso dei documenti XML.  Le classi, i metodi e le proprietà aggiuntive, oltre a supportare completamente gli standard W3C, aggiungono ulteriori funzionalità rispetto a quelle presenti nel modello DOM XML di W3C.  Grazie alle nuove classi è possibile accedere ai dati relazionali e usufruire di metodi per la sincronizzazione con i dati ADO.NET, esponendo simultaneamente i dati come XML.  Per altre informazioni, vedere [Sincronizzazione di un DataSet con un XmlDataDocument](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md).  
  
 Il DOM è particolarmente utile per la lettura dei dati XML in memoria per modificarne la struttura, per aggiungere o rimuovere nodi o per modificare i dati appartenenti a un nodo come nel testo contenuto da un elemento.  Tuttavia, sono disponibili altre classi che sono più rapide del DOM in altri scenari.  Per ottenere accesso al flusso XML di tipo forward\-only e non memorizzato nella cache, usare **XmlReader** e **XmlWriter**.  Se invece è necessario un accesso casuale con un modello a cursore e **XPath**, usare la classe **XPathNavigator**.  
  
## Vedere anche  
 [Tipi di nodi XML](../../../../docs/standard/data/xml/types-of-xml-nodes.md)   
 [Mapping della gerarchia di oggetti in dati XML](../../../../docs/standard/data/xml/mapping-the-object-hierarchy-to-xml-data.md)
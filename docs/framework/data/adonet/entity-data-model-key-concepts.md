---
title: "Concetti chiave di Entity Data Model | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c635a16d-6674-45aa-9344-dcb7df992bab
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Concetti chiave di Entity Data Model
In EDM \(Entity Data Model\) si usano tre concetti chiave per descrivere la struttura di dati: *tipo di entità*, *tipo di associazione* e *proprietà*.  Si tratta dei concetti più importanti nella descrizione della struttura di dati in qualsiasi implementazione di EDM.  
  
## Tipo di entità  
 Il [tipo di entità](../../../../docs/framework/data/adonet/entity-type.md) è il blocco predefinito fondamentale per la descrizione della struttura di dati con Entity Data Model.  In un modello concettuale, i tipi di entità vengono costruiti dalle [proprietà](../../../../docs/framework/data/adonet/property.md) e descrivono la struttura di concetti di livello superiore, ad esempio i clienti e gli ordini in un'applicazione aziendale.  Esattamente come una definizione di classe in un programma informatico è un modello per le istanze della classe, un tipo di entità è un modello per le entità.  Un'entità rappresenta un oggetto specifico \(ad esempio un cliente o un ordine specifico\).  Ogni entità deve disporre di una [chiave di entità](../../../../docs/framework/data/adonet/entity-key.md) univoca all'interno di un [set di entità](../../../../docs/framework/data/adonet/entity-set.md).  Un set di entità è una raccolta di istanze di un tipo di entità specifico.  I set di entità \(e i [set di associazioni](../../../../docs/framework/data/adonet/association-set.md)\) sono raggruppati logicamente in un [contenitore di entità](../../../../docs/framework/data/adonet/entity-container.md).  
  
 L'ereditarietà è supportata con i tipi di entità, ovvero un tipo di entità può essere derivato da un altro.  Per altre informazioni, vedere [Entity Data Model: ereditarietà](../../../../docs/framework/data/adonet/entity-data-model-inheritance.md).  
  
## Tipo di associazione  
 Un [tipo di associazione](../../../../docs/framework/data/adonet/association-type.md) \(detto anche associazione\) è il blocco predefinito fondamentale per la descrizione delle relazioni in Entity Data Model.  In un modello concettuale, un'associazione rappresenta una relazione tra due tipi di entità \(ad esempio, Customer e Order\).  Ogni associazione dispone di due [entità finali dell'associazione](../../../../docs/framework/data/adonet/association-end.md) che specificano i tipi di entità coinvolti nell'associazione.  Ogni entità finale dell'associazione specifica inoltre una [molteplicità di entità finale dell'associazione](../../../../docs/framework/data/adonet/association-end-multiplicity.md) che indica il numero di entità che possono trovarsi a tale entità finale dell'associazione.  Una molteplicità di entità finale dell'associazione può disporre di un valore pari a uno \(1\), zero o uno \(0..1\) o molti \(\*\).  Le entità in corrispondenza di un'entità finale di un'associazione sono accessibili attraverso [proprietà di navigazione](../../../../docs/framework/data/adonet/navigation-property.md) o chiavi esterne se sono esposte in un tipo di entità.  Per altre informazioni, vedere [proprietà di chiave esterna](../../../../docs/framework/data/adonet/foreign-key-property.md).  
  
 In un'applicazione, un'istanza di un'associazione rappresenta un'associazione specifica \(ad esempio, un'associazione tra un'istanza relativa al cliente e istanze relative all'ordine\).  Le istanze dell'associazione sono raggruppate logicamente in un [set di associazioni](../../../../docs/framework/data/adonet/association-set.md).  I set di associazioni \(e i [set di entità](../../../../docs/framework/data/adonet/entity-set.md)\) sono raggruppati logicamente in un [contenitore di entità](../../../../docs/framework/data/adonet/entity-container.md).  
  
## Proprietà  
 I [tipi di entità](../../../../docs/framework/data/adonet/entity-type.md) contengono [proprietà](../../../../docs/framework/data/adonet/property.md) che ne definiscono la struttura e le caratteristiche.  È, ad esempio, possibile che un tipo di entità Customer disponga di proprietà quali CustomerId, Name e Address.  
  
 Le proprietà in un modello concettuale sono analoghe alle proprietà definite su una classe in un programma informatico.  Nello stesso modo in cui le proprietà su una classe definiscono la forma della classe e forniscono informazioni su oggetti, le proprietà in un modello concettuale definiscono la forma di un tipo di entità e forniscono informazioni su istanze del tipo di entità.  
  
 Una proprietà può contenere dati primitivi \(ad esempio una stringa, un Integer o un valore booleano\) o dati strutturati \(ad esempio un tipo complesso\).  Per altre informazioni, vedere [Entity Data Model: tipi di dati primitivi](../../../../docs/framework/data/adonet/entity-data-model-primitive-data-types.md).  
  
## Rappresentazioni di un modello concettuale  
 Un *modello concettuale* è una rappresentazione specifica della struttura di alcuni dati come entità e relazioni.  È possibile rappresentare un modello concettuale tramite un diagramma.  Nel diagramma seguente viene rappresentato un modello concettuale con tre tipi di entità \(`Book`, `Publisher` e `Author`\) e due associazioni \(`PublishedBy` e `WrittenBy`\):  
  
 ![Modello con le proprietà di navigazione](../../../../docs/framework/data/adonet/media/modelwithnavprops.gif "ModelWithNavProps")  
  
 Questa rappresentazione, tuttavia, presenta alcuni difetti quando è necessario illustrare alcuni dettagli relativi al modello.  Le informazioni sul tipo di proprietà e sul set di entità, ad esempio, non sono illustrate nel diagramma.  La ricchezza di un modello concettuale può essere illustrata più chiaramente con un linguaggio specifico di dominio.  [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio basato su XML detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(*Conceptual Schema Definition Language*\) per definire i modelli concettuali.  Di seguito è riportata la definizione CSDL del modello concettuale nel diagramma precedente:  
  
 [!code-xml[EDM_Example_Model#EDMExampleCSDL](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#edmexamplecsdl)]  
  
## Vedere anche  
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)
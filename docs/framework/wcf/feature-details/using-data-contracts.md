---
title: "Uso di contratti dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Classe DataContractAttribute"
  - "WCF, dati"
  - "contratti dati [WCF]"
ms.assetid: a3ae7b21-c15c-4c05-abd8-f483bcbf31af
caps.latest.revision: 38
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 38
---
# Uso di contratti dati
Un *contratto dati* è un accordo formale tra un servizio e un client che descrive astrattamente i dati da scambiare. Per comunicare, non è necessario che il client e il servizio condividano gli stessi tipi, ma solo gli stessi contratti dati. Un contratto dati definisce con precisione, per ogni parametro o tipo restituito, i dati serializzati \(trasformati in XML\) che verranno scambiati.  
  
## Nozioni fondamentali dei contratti dati  
 Per impostazione predefinita in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene utilizzato un motore di serializzazione denominato serializzatore dei contratti dati per serializzare e deserializzare i dati \(convertendoli in\/da XML\). Ogni tipo primitivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], ad esempio numeri interi e stringhe, nonché alcuni tipi trattati come primitivi, ad esempio <xref:System.DateTime> e <xref:System.Xml.XmlElement>, può essere serializzato senza ulteriore preparazione ed è considerato in possesso di contratti dati predefiniti. I tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], inoltre, dispongono di contratti dati esistenti. Per un elenco completo dei tipi serializzabili, vedere [Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md).  
  
 Per poter essere serializzabili, è necessario che i nuovi tipi complessi creati dispongano di un contratto dati appositamente definito. Per impostazione predefinita, tramite <xref:System.Runtime.Serialization.DataContractSerializer> viene dedotto il contratto dati e vengono serializzati tutti i tipi visibili pubblicamente. Vengono serializzati i campi e le proprietà di lettura\/scrittura pubblici del tipo. È possibile rifiutare esplicitamente i membri per la serializzazione tramite <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>. È inoltre possibile creare in modo esplicito un contratto dati utilizzando gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute>. Ciò viene di norma realizzato applicando l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> al tipo. Questo attributo può essere applicato a classi, strutture ed enumerazioni. L'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> deve quindi essere applicato a ogni membro del tipo di contratto dati per indicare che si tratta di un *membro dati*, ovvero che deve essere serializzato.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Tipi serializzabili](../../../../docs/framework/wcf/feature-details/serializable-types.md).  
  
### Esempio  
 Nell'esempio seguente viene illustrato un contratto di servizio \(un'interfaccia\) a cui sono stati applicati in modo esplicito gli attributi <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute>. Nell'esempio viene mostrato che i tipi primitivi non richiedono un contratto dati, diversamente da un tipo complesso.  
  
 [!code-csharp[C_DataContract#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#1)]
 [!code-vb[C_DataContract#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#1)]  
  
 Nell'esempio seguente viene illustrato come creare un contratto dati per il tipo `MyTypes.PurchaseOrder` creato applicando gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> alla classe e ai relativi membri.  
  
 [!code-csharp[C_DataContract#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#2)]
 [!code-vb[C_DataContract#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#2)]  
  
### Note  
 Nelle note seguenti sono contenuti gli elementi da tenere presenti durante la creazione di contratti dati:  
  
-   L'attributo <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> viene accettato solo se utilizzato con tipi non contrassegnati. Sono inclusi i tipi non contrassegnati con uno degli attributi <xref:System.Runtime.Serialization.DataContractAttribute>, <xref:System.SerializableAttribute>, <xref:System.Runtime.Serialization.CollectionDataContractAttribute> o <xref:System.Runtime.Serialization.EnumMemberAttribute> oppure contrassegnati come serializzabili in qualsiasi altro modo \(ad esempio <xref:System.Xml.Serialization.IXmlSerializable>\).  
  
-   È possibile applicare l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> a campi e proprietà.  
  
-   I livelli di accessibilità ai membri \(interno, privato, protetto o pubblico\) non influiscono in alcun modo sul contratto dati.  
  
-   L'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> viene ignorato se applicato a membri statici.  
  
-   Durante la serializzazione il codice della proprietà get viene chiamato per i membri dati della proprietà per ottenere il valore delle proprietà da serializzare.  
  
-   Durante la deserializzazione viene prima creato un oggetto non inizializzato, senza chiamare alcun costruttore per il tipo, quindi vengono deserializzati tutti i membri dati.  
  
-   Durante la deserializzazione il codice della proprietà set viene chiamato per i membri dati della proprietà per impostare le proprietà sul valore in fase di deserializzazione.  
  
-   Perché un contratto dati sia valido, deve essere possibile serializzare tutti i relativi membri dati. Per un elenco completo dei tipi serializzabili, vedere [Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md).  
  
     I tipi generici sono gestiti esattamente nello stesso modo dei tipi non generici. Non vi sono requisiti speciali per i parametri generici. Si consideri ad esempio il tipo seguente:  
  
 [!code-csharp[C_DataContract#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#3)]
 [!code-vb[C_DataContract#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#3)]  
  
 Il tipo è serializzabile indipendentemente dal fatto che il tipo utilizzato per il parametro di tipo generico \(`T`\) sia serializzabile o meno. Poiché deve essere possibile serializzare tutti i membri dati, il tipo seguente è serializzabile solo se il parametro di tipo generico è anch'esso serializzabile, come indicato nel codice seguente.  
  
 [!code-csharp[C_DataContract#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#4)]
 [!code-vb[C_DataContract#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#4)]  
  
 Per un esempio di codice completo di un servizio WCF che definisce un contratto dati, vedere l'esempio [Contratto dati di base](../../../../docs/framework/wcf/samples/basic-data-contract.md).  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 [Tipi serializzabili](../../../../docs/framework/wcf/feature-details/serializable-types.md)   
 [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md)   
 [Equivalenza dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Ordine dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-order.md)   
 [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)   
 [Controllo delle versioni dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)   
 [Callback di serializzazione a tolleranza di versione](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)   
 [Valori predefiniti dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-default-values.md)   
 [Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)   
 [Procedura: creare un contratto dati di base per una classe o una struttura](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)
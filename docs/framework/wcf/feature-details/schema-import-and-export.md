---
title: "Importazione ed esportazione degli schemi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, importazione ed esportazione di schemi"
  - "Classe XsdDataContractExporter"
  - "Classe XsdDataContractImporter"
ms.assetid: 0da32b50-ccd9-463a-844c-7fe803d3bf44
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Importazione ed esportazione degli schemi
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]include un nuovo motore di serializzazione, la <xref:System.Runtime.Serialization.DataContractSerializer>. `DataContractSerializer` esegue la conversione tra oggetti [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] e XML in entrambe direzioni. Oltre al serializzatore, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono inoltre inclusi meccanismi di importazione ed esportazione degli schemi associati. *Schema* è una descrizione formale, precisa e leggibile dal computer della forma del XML prodotto dal serializzatore o di cui il deserializzatore può accedere. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene utilizzato il linguaggio XSD (XML Schema Definition Language) W3C (World Wide Web Consortium) come rappresentazione dello schema, che è ampiamente interoperabile con numerose piattaforme di terze parti.  
  
 Il componente per l'importazione dello schema, <xref:System.Runtime.Serialization.XsdDataContractImporter>, considera un documento di schema XSD e genera [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] classi (generalmente classi del contratto dati) in modo che i formati serializzati corrispondano al determinato schema.  
  
 Si consideri ad esempio il frammento di schema seguente:  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
 genera il tipo seguente (leggermente semplificato per una migliore leggibilità)  
  
 [!code-csharp[c_SchemaImportExport#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#1)]
 [!code-vb[c_SchemaImportExport#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#1)]  
  
 Si noti che il tipo generato segue diverse procedure consigliate del contratto dati (trovato [le procedure consigliate: controllo delle versioni del contratto dati](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)):  
  
-   Il tipo implementa il <xref:System.Runtime.Serialization.IExtensibleDataObject> interfaccia. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][I contratti di dati compatibile](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
-   I membri dati vengono implementati come proprietà pubbliche che incapsulano campi privati.  
  
-   La classe è una classe parziale e le aggiunte possono essere eseguite senza modificare il codice generato.  
  
 Il <xref:System.Runtime.Serialization.XsdDataContractExporter> consente di eseguire l'operazione inversa, ovvero considera i tipi siano con il `DataContractSerializer` e genera un documento di Schema XSD.  
  
## <a name="fidelity-is-not-guaranteed"></a>Fedeltà non garantita   
 Non è garantito che lo schema o i tipi eseguano un round trip con fedeltà assoluta (A *round trip* significa che importare uno schema per creare un set di classi e l'esportazione del risultato per creare nuovamente uno schema.) È possibile che non venga restituito lo stesso schema. Anche per l'inversione del processo non è garantito il mantenimento della fedeltà (quando si esporta un tipo per generare lo schema e quindi si importa di nuovo il tipo, è improbabile che venga restituito lo stesso tipo).  
  
## <a name="supported-types"></a>Tipi supportati  
 Il modello del contratto dati supporta solo un sottoinsieme limitato dello schema WC3. Qualsiasi schema che non è conforme a tale sottoinsieme genererà un'eccezione durante il processo di importazione. Ad esempio, non esiste alcun sistema per specificare che un membro dati di un contratto dati debba essere serializzato come attributo XML. Di conseguenza, gli schemi che richiedono l'utilizzo di attributi XML non sono supportati e verranno generate eccezioni durante l'importazione, poiché è impossibile generare un contratto dati con la proiezione XML corretta.  
  
 Ad esempio, non è possibile importare il frammento di schema seguente utilizzando le impostazioni di importazione predefinite.  
  
 <!-- TODO: review snippet reference [!code[c_SchemaImportExport#9](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#9)]  -->  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Riferimento allo Schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md). Se un schema non è conforme alle regole del contratto dati, utilizzare un motore di serializzazione diverso. Ad esempio, il <xref:System.Xml.Serialization.XmlSerializer> utilizza un proprio meccanismo di importazione dello schema separato. È inoltre disponibile una modalità di importazione speciale in cui l'intervallo dello schema supportato viene espanso. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]la sezione sulla generazione <xref:System.Xml.Serialization.IXmlSerializable> tipi [importazione dello Schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md).  
  
 La classe `XsdDataContractExporter` supporta tutti i tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che possono essere serializzati con `DataContractSerializer`. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md). Si noti che lo schema generato utilizzando il `XsdDataContractExporter` è solitamente di dati validi che il `XsdDataContractImporter` possibile utilizzare (a meno che il <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> viene utilizzato per personalizzare lo schema).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]utilizzo di <xref:System.Runtime.Serialization.XsdDataContractImporter>, vedere [importazione dello Schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]utilizzo di <xref:System.Runtime.Serialization.XsdDataContractExporter>, vedere [l'esportazione di schemi dalle classi](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 <xref:System.Runtime.Serialization.XsdDataContractExporter>   
 [Importazione dello Schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)   
 [Esportazione di schemi dalle classi](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)
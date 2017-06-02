---
title: "Esportazione di schemi dalle classi | Microsoft Docs"
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
  - "schemi [WCF], esportazione da classi"
  - "schemi [WCF]"
  - "Classe XsdDataContractExporter"
  - "Classe XsdDataContractImporter"
ms.assetid: bb57b962-70c1-45a9-93d5-e721e340a13f
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Esportazione di schemi dalle classi
Per generare schemi XSD \(XML Schema Definition Language\) dalle classi usate nel modello del contratto dati, usare la classe <xref:System.Runtime.Serialization.XsdDataContractExporter>. In questo argomento viene illustrato il processo di creazione degli schemi.  
  
## Processo di esportazione  
 Il processo di esportazione degli schemi ha inizio con uno o più tipi e produce una classe <xref:System.Xml.Schema.XmlSchemaSet> che descrive la proiezione XML di questi tipi.  
  
 La classe `XmlSchemaSet` fa parte del modello SOM \(Schema Object Model\) di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che rappresenta un set di documenti dello schema XSD. Per creare documenti XSD da una classe `XmlSchemaSet`, usare la raccolta di schemi dalla proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> della classe `XmlSchemaSet`. Quindi serializzare ogni oggetto <xref:System.Xml.Schema.XmlSchema> usando <xref:System.Xml.Serialization.XmlSerializer>.  
  
#### Per esportare gli schemi  
  
1.  Creare un'istanza di <xref:System.Runtime.Serialization.XsdDataContractExporter>.  
  
2.  Parametro facoltativo. Passare una classe <xref:System.Xml.Schema.XmlSchemaSet> nel costruttore. In questo caso, lo schema generato durante l'esportazione dello schema viene aggiunto a questa istanza di <xref:System.Xml.Schema.XmlSchemaSet> anziché iniziare con un'istanza di <xref:System.Xml.Schema.XmlSchemaSet> vuota.  
  
3.  Parametro facoltativo. Chiamare uno dei metodi <xref:System.Runtime.Serialization.XsdDataContractExporter.CanExport%2A>. Il metodo determina se il tipo specificato può essere esportato. Il metodo presenta gli stessi overload del metodo `Export` nel passaggio successivo.  
  
4.  Chiamare uno dei metodi <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A>. Sono disponibili tre overload che accettano un <xref:System.Type>, un <xref:System.Collections.Generic.List%601> di oggetti `Type` o un <xref:System.Collections.Generic.List%601> di oggetti <xref:System.Reflection.Assembly>. Nell'ultimo caso, tutti i tipi degli assembly specificati vengono esportati.  
  
     Più chiamate al metodo `Export` determinano l'aggiunta di più elementi alla stessa classe `XmlSchemaSet`. Se esiste già un tipo in `XmlSchemaSet`, non ne viene generato un altro. Pertanto, è preferibile eseguire più chiamate a `Export` sulla stessa classe `XsdDataContractExporter` rispetto alla creazione di più istanze della classe `XsdDataContractExporter`. In questo modo non vengono generati tipi di schema duplicati.  
  
    > [!NOTE]
    >  Se si verifica un errore durante l'esportazione, lo stato della classe `XmlSchemaSet` sarà imprevedibile.  
  
5.  Accedere a <xref:System.Xml.Schema.XmlSchemaSet> mediante la proprietà <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A>.  
  
## Opzioni di esportazione  
 È possibile impostare la proprietà <xref:System.Runtime.Serialization.XsdDataContractExporter.Options%2A> di <xref:System.Runtime.Serialization.XsdDataContractExporter> su un'istanza della classe <xref:System.Runtime.Serialization.ExportOptions> per controllare vari aspetti del processo di esportazione. In particolare, è possibile impostare le opzioni seguenti:  
  
-   <xref:System.Runtime.Serialization.ExportOptions.KnownTypes%2A>. Questa raccolta di `Type` rappresenta i tipi noti per i tipi da esportare.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md). Questi tipi noti vengono esportati con ogni chiamata a `Export` in aggiunta ai tipi passati al metodo `Export`.  
  
-   <xref:System.Runtime.Serialization.ExportOptions.DataContractSurrogate%2A>. Un'interfaccia <xref:System.Runtime.Serialization.IDataContractSurrogate> può essere fornita tramite questa proprietà per personalizzare il processo di esportazione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Surrogati del contratto dati](../../../../docs/framework/wcf/extending/data-contract-surrogates.md). Per impostazione predefinita, non viene usato alcun surrogato.  
  
## Metodi helper  
 Oltre al ruolo principale di esportare gli schemi, `XsdDataContractExporter` fornisce molti utili metodi helper che forniscono informazioni sui tipi. tra cui:  
  
-   Metodo <xref:System.Runtime.Serialization.XsdDataContractExporter.GetRootElementName%2A>. Questo metodo accetta un `Type` e restituisce un <xref:System.Xml.XmlQualifiedName> che rappresenta il nome e lo spazio dei nomi dell'elemento principale che verrebbero usati se questo tipo venisse serializzato come oggetto principale.  
  
-   Metodo <xref:System.Runtime.Serialization.XsdDataContractExporter.GetSchemaTypeName%2A>. Questo metodo accetta un `Type` e restituisce un <xref:System.Xml.XmlQualifiedName> che rappresenta il nome dello schema XSD che verrebbe usato se questo tipo venisse esportato nello schema. Per i tipi <xref:System.Xml.Serialization.IXmlSerializable> rappresentati come tipi anonimi nello schema, questo metodo restituisce `null`.  
  
-   Metodo <xref:System.Runtime.Serialization.XsdDataContractExporter.GetSchemaType%2A>. Questo metodo funziona solo con i tipi <xref:System.Xml.Serialization.IXmlSerializable> rappresentati come tipi anonimi nello schema e restituisce `null` per tutti gli altri tipi. Per i tipi anonimi, questo metodo restituisce un <xref:System.Xml.Schema.XmlSchemaType> che rappresenta un determinato `Type`.  
  
 Le opzioni di esportazione influiscono su tutti questi metodi.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 <xref:System.Runtime.Serialization.XsdDataContractExporter>   
 [Importazione ed esportazione degli schemi](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md)   
 [Importazione dello schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)
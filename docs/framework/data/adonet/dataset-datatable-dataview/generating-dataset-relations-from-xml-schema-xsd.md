---
title: "Generazione delle relazioni del DataSet da XML Schema (XSD) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c9a1413-c0d2-4447-88ba-9a2b0cbc0aa8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Generazione delle relazioni del DataSet da XML Schema (XSD)
In un tipo <xref:System.Data.DataSet> è possibile stabilire un'associazione tra due o più colonne creando una relazione padre\-figlio.  Una relazione **DataSet** può essere rappresentata all'interno di uno schema XSD \(XML Schema Definition Language\) in tre modi diversi:  
  
-   Specificare tipi complessi annidati.  
  
-   Usare l'annotazione **msdata:Relationship**.  
  
-   Specificare un **xs:keyref** senza l'annotazione **msdata:ConstraintOnly**.  
  
## Tipi complessi annidati  
 Le definizioni di tipi complessi annidati in uno schema indicano le relazioni padre\-figlio degli elementi.  Nel seguente frammento di XML Schema viene mostrato che **OrderDetail** è un elemento figlio dell'elemento **Order**.  
  
```  
<xs:element name="Order">  
  <xs:complexType>  
     <xs:sequence>          
       <xs:element name="OrderDetail" />  
           <xs:complexType>               
           </xs:complexType>  
     </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 Il processo di mapping di XML Schema consente di creare nel **DataSet** tabelle corrispondenti ai tipi complessi annidati dello schema  e di creare colonne aggiuntive, usate come colonne padre**\-**figlio per le tabelle generate.  Notare che tali colonne padre**\-**figlio consentono di specificare relazioni, il che non equivale a specificare vincoli di chiave primaria\/chiave esterna.  
  
## Annotazione msdata:Relationship  
 L'annotazione **msdata:Relationship** consente di specificare esplicitamente relazioni padre\-figlio tra gli elementi non annidati di uno schema.  Nell'esempio seguente viene mostrata la struttura dell'elemento **Relationship**.  
  
```  
  
  <msdata:Relationship name="CustOrderRelationship"    
msdata:parent=""    
msdata:child=""    
msdata:parentkey=""    
msdata:childkey="" />  
```  
  
 Gli attributi dell'annotazione **msdata:Relationship** consentono di identificare gli elementi coinvolti in una relazione padre\-figlio, oltre agli elementi **parentkey** e **childkey** e gli attributi coinvolti nella relazione.  Queste informazioni vengono usate dal processo di mapping per generare tabelle nel **DataSet** e creare relazioni di chiave primaria\/chiave esterna tra tali tabelle.  
  
 Ad esempio, il seguente frammento di schema specifica gli elementi **Order** e **OrderDetail** allo stesso livello \(non annidati\).  Lo schema specifica un'annotazione **msdata:Relationship**, che a sua volta specifica la relazione padre\-figlio tra i due elementi.  In questo caso è necessario specificare una relazione esplicita mediante l'annotazione **msdata:Relationship**.  
  
```  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
        <xs:element name="OrderDetail">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
       <xs:element name="Order">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
    </xs:choice>  
  </xs:complexType>  
</xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrdDetailRelation"  
          msdata:parent="Order"  
          msdata:child="OrderDetail"   
          msdata:parentkey="OrderNumber"  
          msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
  
```  
  
 L'elemento **Relationship** viene usato dal processo di mapping per creare una relazione padre\-figlio tra la colonna **OrderNumber** della tabella **Order** e la colonna **OrderNo** della tabella **OrderDetail** nel **DataSet**.  Il processo di mapping consente solo di specificare la relazione. Non specifica automaticamente alcun vincolo sui valori di tali colonne, a differenza di quanto avviene mediante i vincoli di chiave primaria\/chiave esterna nei database relazionali.  
  
### Contenuto della sezione  
 [Mappare relazioni implicite tra elementi annidati dello schema](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-implicit-relations-between-nested-schema-elements.md)  
 Vengono descritti i vincoli e le relazioni creati implicitamente in un **DataSet** quando in XML Schema sono presenti elementi annidati.  
  
 [Mappare le relazioni specificate per gli elementi annidati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-relations-specified-for-nested-elements.md)  
 Viene descritto come impostare esplicitamente le relazioni in un **DataSet** per gli elementi annidati di XML Schema.  
  
 [Definire relazioni tra elementi non annidati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/specify-relations-between-elements-with-no-nesting.md)  
 Viene descritta la creazione di relazioni in un **DataSet** tra elementi non annidati di XML Schema.  
  
### Sezioni correlate  
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Viene descritta la struttura relazionale, o schema, di un **DataSet** creata da uno schema XSD \(XML Schema Definition Language\).  
  
 [Mapping dei vincoli di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Vengono descritti gli elementi di XML Schema usati per creare vincoli univoci e per chiavi esterne in un **DataSet**.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
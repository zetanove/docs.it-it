---
title: "Derivazione della struttura relazionale di un DataSet da XML Schema (XSD) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f6cd04d-6197-4bc4-9096-8c51c7e4acae
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Derivazione della struttura relazionale di un DataSet da XML Schema (XSD)
Questa sezione fornisce una panoramica della compilazione dello schema relazionale di un tipo <xref:System.Data.DataSet> da un documento basato sullo schema XSD \(XML Schema Definition Language\).  In genere, per ogni elemento figlio **complexType** di un elemento dello schema viene generata una tabella nel **DataSet**.  La struttura della tabella è determinata dalla definizione del tipo complesso.  Nel **DataSet** vengono create tabelle per gli elementi di livello principale dello schema.  Tuttavia, una tabella viene creata per un elemento **complexType** di livello principale solo se tale elemento è annidato all'interno di un altro elemento **complexType**. In questo caso, viene eseguito il mapping dell'elemento **complexType** annidato a un oggetto <xref:System.Data.DataTable> nell'oggetto **DataSet**.  
  
 Per altre informazioni su XSD, vedere le raccomandazioni World Wide Web Consortium \(W3C\) XML Schema Part 0: Primer, XML Schema Part 1: Structures e XML Schema Part 2: Datatypes all'indirizzo [http:\/\/www.w3.org\/](http://www.w3.org/TR/).  
  
 Nell'esempio seguente viene illustrato un XML Schema in cui `customers` rappresenta l'elemento figlio dell'elemento `MyDataSet`, che è un elemento del **DataSet**.  
  
```  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element name="customers" >   
           <xs:complexType >  
             <xs:sequence>  
               <xs:element name="CustomerID" type="xs:integer"   
                            minOccurs="0" />  
               <xs:element name="CompanyName" type="xs:string"   
                            minOccurs="0" />  
               <xs:element name="Phone" type="xs:string" />  
             </xs:sequence>  
           </xs:complexType>  
          </xs:element>  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 L'elemento `customers` nell'esempio precedente è un elemento di tipo complesso.  La definizione di tipo complesso viene quindi analizzata e la tabella seguente viene creata dal processo di mapping.  
  
```  
Customers (CustomerID , CompanyName, Phone)  
```  
  
 Il tipo di dati relativo a ogni colonna della tabella viene derivato dal tipo di XML Schema relativo al corrispondente elemento o attributo specificato.  
  
> [!NOTE]
>  Se l'elemento `customers` è di un tipo di dati di XML Schema semplice, quale **integer**, non verrà generata alcuna tabella.  Le tabelle vengono create solo per gli elementi di livello principale di tipo complesso.  
  
 Nell'XML Schema seguente all'elemento **Schema** sono associati due elementi figlio, `InStateCustomers` e `OutOfStateCustomers`.  
  
```  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="InStateCustomers" type="customerType" />  
   <xs:element name="OutOfStateCustomers" type="customerType" />  
    <xs:complexType name="customerType" >  
  
     </xs:complexType>  
  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element ref="customers" />  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 Entrambi gli elementi figlio `InStateCustomers` e `OutOfStateCustomers` sono elementi di tipo complesso \(`customerType`\).  Di conseguenza, nel **DataSet** vengono generate le due tabelle identiche seguenti.  
  
```  
InStateCustomers (CustomerID , CompanyName, Phone)  
OutOfStateCustomers (CustomerID , CompanyName, Phone)  
```  
  
## In questa sezione  
 [Mapping dei vincoli di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Vengono descritti gli elementi di XML Schema usati per creare vincoli univoci e per chiavi esterne in un **DataSet**.  
  
 [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 Vengono descritti gli elementi di XML Schema usati per creare relazioni tra le colonne delle tabelle in un **DataSet**.  
  
 [Vincoli e relazioni di XML Schema](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/xml-schema-constraints-and-relationships.md)  
 Viene descritta la creazione implicita delle relazioni quando si usano gli elementi di XML Schema per creare vincoli in un **DataSet**.  
  
## Sezioni correlate  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 Viene descritto come caricare e mantenere la struttura relazionale e i dati in un **DataSet** come dati XML.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
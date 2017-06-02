---
title: "Mappare i vincoli di XML Schema (XSD) keyref ai vincoli del DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Mappare i vincoli di XML Schema (XSD) keyref ai vincoli del DataSet
L'elemento **keyref** consente di stabilire collegamenti tra gli elementi all'interno di un documento.  Questo elemento ha quindi una funzione simile a quella della relazione di chiave esterna in un database relazionale.  Se in uno schema viene specificato l'elemento **keyref**, durante il processo di mapping dello schema l'elemento viene convertito in un vincolo di chiave esterna corrispondente per le colonne delle tabelle del tipo <xref:System.Data.DataSet>.  Per impostazione predefinita, una relazione viene generata anche dall'elemento **keyref** e le proprietà **ParentTable**, **ChildTable**, **ParentColumn** e **ChildColumn** vengono specificate per tale relazione.  
  
 Nella tabella seguente vengono brevemente descritti gli attributi **msdata** che è possibile specificare per l'elemento **keyref**.  
  
|Nome attributo|Descrizione|  
|--------------------|-----------------|  
|**msdata:ConstraintOnly**|Se **ConstraintOnly\="true"** è specificato nell'elemento **keyref** dello schema, verrà creato un vincolo ma non verrà creata alcuna relazione.  Se questo attributo non viene specificato \(o è impostato su **False**\), nel **DataSet** vengono creati sia il vincolo che la relazione.|  
|**msdata:ConstraintName**|Se l'attributo **ConstraintName** è specificato, il relativo valore viene usato come nome del vincolo.  In caso contrario, il nome del vincolo nel **DataSet** viene fornito dall'attributo **name** dell'elemento **keyref** dello schema.|  
|**msdata:UpdateRule**|Se l'attributo **UpdateRule** viene specificato nell'elemento **keyref** dello schema, il relativo valore viene assegnato alla proprietà di vincolo **UpdateRule** nel **DataSet**.  In caso contrario, la proprietà **UpdateRule** viene impostata su **Cascade**.|  
|**msdata:DeleteRule**|Se l'attributo **DeleteRule** viene specificato nell'elemento **keyref** dello schema, il relativo valore viene assegnato alla proprietà di vincolo **DeleteRule** nel **DataSet**.  In caso contrario, la proprietà **DeleteRule** viene impostata su **Cascade**.|  
|**msdata:AcceptRejectRule**|Se l'attributo **AcceptRejectRule** viene specificato nell'elemento **keyref** dello schema, il relativo valore viene assegnato alla proprietà di vincolo **AcceptRejectRule** nel **DataSet**.  In caso contrario, la proprietà **AcceptRejectRule** viene impostata su **None**.|  
  
 Nell'esempio seguente viene riportato uno schema in cui vengono specificate le relazioni **key** e **keyref** tra l'elemento figlio **OrderNumber** dell'elemento **Order** e l'elemento figlio **OrderNo** dell'elemento **OrderDetail**.  
  
 Nell'esempio, l'elemento figlio **OrderNumber** dell'elemento **OrderDetail** fa riferimento all'elemento chiave figlio **OrderNo** dell'elemento **Order**.  
  
```  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 Il processo di mapping dello schema XSD \(XML Schema Definition Language\) consente di generare il seguente **DataSet** con due tabelle:  
  
```  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 Nel **DataSet** vengono inoltre definiti i seguenti vincoli:  
  
-   Un vincolo univoco nella tabella **Order**.  
  
    ```  
  
              Table: Order  
    Columns: OrderNumber   
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
-   Una relazione tra le tabelle **Order** e **OrderDetail**.  La proprietà **Nested** viene impostata su **False**, poiché i due elementi non sono annidate nello schema.  
  
    ```  
  
              ParentTable: Order  
    ParentColumns: OrderNumber   
    ChildTable: OrderDetail  
    ChildColumns: OrderNo   
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
-   Un vincolo di chiave esterna nella tabella **OrderDetail**.  
  
    ```  
  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo   
    RelatedTable: Order  
    RelatedColumns: OrderNumber   
    ```  
  
## Vedere anche  
 [Mapping dei vincoli di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
---
title: "Mappare relazioni implicite tra elementi annidati dello schema | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6b25002a-352e-4d9b-bae3-15129458a355
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Mappare relazioni implicite tra elementi annidati dello schema
È possibile che in uno schema XSD \(XML Schema Definition Language\) siano presenti tipi complessi annidati uno all'interno dell'altro.  In questo caso, le impostazioni di mapping predefinite vengono applicate dal processo di mapping e nel tipo <xref:System.Data.DataSet> vengono creati i seguenti elementi:  
  
-   Una tabella per ogni tipo complesso \(padre e figlio\).  
  
-   Se nell'elemento padre non è presente alcun vincolo univoco, in ogni definizione di tabella viene inclusa una colonna di chiave primaria aggiuntiva denominata *TableName*\_Id dove *TableName* rappresenta il nome della tabella padre.  
  
-   Un vincolo di chiave primaria nella tabella padre che consenta di identificare la colonna aggiuntiva come chiave primaria \(mediante l'impostazione della proprietà **IsPrimaryKey** su **True**\).  Il vincolo viene denominato Constraint*\#*, dove *\#* rappresenta 1, 2, 3 e così via.  Il nome predefinito del primo vincolo, ad esempio, è Constraint1.  
  
-   Un vincolo di chiave esterna nella tabella figlio che consenta di identificare la colonna aggiuntiva come chiave esterna contenente riferimenti alla chiave primaria della tabella padre.  Il vincolo viene denominato *ParentTable\_ChildTable*, dove *ParentTable* rappresenta il nome della tabella padre e *ChildTable* il nome della tabella figlio.  
  
-   Una relazione di dati tra le tabelle padre e figlio.  
  
 Nell'esempio seguente viene riportato uno schema in cui **OrderDetail** è un elemento figlio di **Order**.  
  
```  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
   <xs:complexType>  
     <xs:choice maxOccurs="unbounded">  
       <xs:element name="Order">  
         <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:string" />  
            <xs:element name="EmpNumber" type="xs:string" />  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:string" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
         </xs:complexType>  
       </xs:element>  
     </xs:choice>  
   </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 Il processo di mapping di XML Schema consente di creare nel **DataSet** i seguenti elementi:  
  
-   Una tabella **Order** e una tabella **OrderDetail**.  
  
    ```  
    Order(OrderNumber, EmpNumber, Order_Id)  
    OrderDetail(OrderNo, ItemNo, Order_Id)  
    ```  
  
-   Un vincolo univoco nella tabella **Order**.  Notare che la proprietà **IsPrimaryKey** è impostata su **True**.  
  
    ```  
    ConstraintName: Constraint1  
    Type: UniqueConstraint  
    Table: Order  
    Columns: Order_Id   
    IsPrimaryKey: True  
    ```  
  
-   Un vincolo di chiave esterna nella tabella **OrderDetail**.  
  
    ```  
    ConstraintName: Order_OrderDetail  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: Order_Id   
    RelatedTable: Order  
    RelatedColumns: Order_Id   
    ```  
  
-   Una relazione tra le tabelle **Order** e **OrderDetail**.  La proprietà **Nested** per questa relazione viene impostata su **True**, poiché gli elementi **Order** e **OrderDetail** sono annidati nello schema.  
  
    ```  
    ParentTable: Order  
    ParentColumns: Order_Id   
    ChildTable: OrderDetail  
    ChildColumns: Order_Id   
    ParentKeyConstraint: Constraint1  
    ChildKeyConstraint: Order_OrderDetail  
    RelationName: Order_OrderDetail  
    Nested: True  
    ```  
  
## Vedere anche  
 [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [Mapping dei vincoli di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
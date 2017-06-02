---
title: "Vincoli e relazioni di XML Schema | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Vincoli e relazioni di XML Schema
Nello schema XSD \(XML Schema Definition Language\) è possibile specificare vincoli \(univoci, key e keyref\) e relazioni \(mediante l'annotazione **msdata:Relationship**\).  In questo argomento viene spiegato come vengono interpretati i vincoli e le relazioni specificati in XML Schema per generare il tipo <xref:System.Data.DataSet>.  
  
 In genere, in XML Schema l'annotazione **msdata:Relationship** viene specificata solo se si desidera generare relazioni nell'oggetto **DataSet**.  Per altre informazioni, vedere [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md).  I vincoli \(univoci, key e keyref\) vengono specificati se si desidera generare vincoli nel **DataSet**.  Notare che i vincoli key e keyref vengono usati anche per generare relazioni, come spiegato successivamente in questo argomento.  
  
## Generazione di una relazione dai vincoli key e keyref  
 Anziché specificare l'annotazione **msdata:Relationship**, è possibile specificare i vincoli key e keyref, usati durante il processo di mapping di XML Schema per la generazione non solo dei vincoli ma anche delle relazioni nel **DataSet**.  Se tuttavia si specifica `msdata:ConstraintOnly="true"` nell'elemento **keyref**, nel **DataSet** saranno inclusi solo i vincoli e non verrà inclusa la relazione.  
  
 Nell'esempio seguente viene illustrato un XML Schema in cui sono inclusi gli elementi non annidati **Order** e **OrderDetail**.  Nello schema vengono specificati anche i vincoli key e keyref.  
  
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
  
 Nel **DataSet** generato durante il processo di mapping di XML Schema sono incluse le tabelle **Order** e **OrderDetail**.  Nel **DataSet** sono inoltre inclusi i vincoli e le relazioni.  Nell'esempio seguente vengono illustrati tali vincoli e relazioni.  Notare che nello schema non viene specificata l'annotazione **msdata:Relationship**. Per generare la relazione vengono infatti usati i vincoli key e keyref.  
  
```  
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 Gli elementi **Order** e **OrderDetail** del precedente esempio di schema non sono annidati.  Nell'esempio di schema seguente tali elementi sono annidati.  Tuttavia, non viene specificata alcuna annotazione **msdata:Relationship**, quindi si presuppone una relazione implicita.  Per altre informazioni, vedere [Mappare relazioni implicite tra elementi annidati dello schema](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-implicit-relations-between-nested-schema-elements.md).  Nello schema vengono specificati anche i vincoli key e keyref.  
  
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
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
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
  
 Nel **DataSet** risultante dal processo di mapping di XML Schema sono incluse due tabelle:  
  
```  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 Nel **DataSet** sono inoltre incluse le due relazioni \(una basata sull'annotazione **msdata:relationship** e l'altra basata sui vincoli key e keyref\) e diversi vincoli.  Nell'esempio seguente vengono illustrati i vincoli e le relazioni.  
  
```  
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 Se in un vincolo keyref che fa riferimento a una tabella annidata è contenuta un'annotazione **msdata:IsNested\="true"**, nel **DataSet** verrà creata un'unica relazione annidata basata sul vincolo keyref e sul vincolo univoco\/key correlato.  
  
## Vedere anche  
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
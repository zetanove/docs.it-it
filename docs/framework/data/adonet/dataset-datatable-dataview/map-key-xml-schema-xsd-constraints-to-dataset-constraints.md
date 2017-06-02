---
title: "Mappare i vincoli key di XML Schema (XSD) ai vincoli del DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Mappare i vincoli key di XML Schema (XSD) ai vincoli del DataSet
In uno schema è possibile specificare un vincolo key per un elemento o un attributo mediante l'elemento **key**.  È necessario che nell'elemento o nell'attributo per cui viene specificato il vincolo siano presenti valori univoci in qualsiasi istanza dello schema e che non sia presente alcun valore null.  
  
 Il vincolo key è simile al vincolo univoco, ma nella colonna per cui viene specificato un vincolo key non sono consentiti valori null.  
  
 Nella tabella seguente vengono brevemente descritti gli attributi **msdata** che è possibile specificare per l'elemento **key**.  
  
|Nome attributo|Descrizione|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|Se questo attributo viene specificato, il relativo valore viene usato come nome del vincolo.  In caso contrario, il valore per il nome del vincolo viene fornito dall'attributo **name**.|  
|**msdata:PrimaryKey**|Se `PrimaryKey="true"` è presente, la proprietà del vincolo **IsPrimaryKey** viene impostata su **true**, trasformando la colonna in chiave primaria.  La proprietà di colonna **AllowDBNull** viene impostata su **false** poiché nelle chiavi primarie non sono consentiti valori null.|  
  
 Durante la conversione di uno schema in cui è specificato un vincolo key, un vincolo univoco viene creato dal processo di mapping per la tabella la cui proprietà di colonna **AllowDBNull** è impostata su **false** per ogni colonna del vincolo.  A meno che non si specifichi `msdata:PrimaryKey="true"` per l'elemento **key**, anche la proprietà **IsPrimaryKey** del vincolo univoco viene impostata su **false**.  Queste impostazioni sono identiche a quelle di un vincolo univoco nello schema in cui `PrimaryKey="true"`.  
  
 Nell'esempio di schema seguente il vincolo key viene specificato dall'elemento **key** per l'elemento **CustomerID**.  
  
```  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>   
```  
  
 L'elemento **key** consente di specificare che è necessario che i valori dell'elemento figlio **CustomerID** dell'elemento **Customers** siano univoci e che non sono consentiti valori null.  Durante la conversione dello schema XSD \(XML Schema Definition Language\), la seguente tabella viene creata dal processo di mapping:  
  
```  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 Il mapping di XML Schema consente inoltre di creare un oggetto **UniqueConstraint** nella colonna **CustomerID**, come illustrato nell'oggetto <xref:System.Data.DataSet> seguente.  Per semplicità vengono mostrate solo le proprietà rilevanti.  
  
```  
  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID   
      IsPrimaryKey: True  
```  
  
 Nell'oggetto **DataSet** generato la proprietà **IsPrimaryKey** di **UniqueConstraint** viene impostata su **true**, poiché nello schema viene specificato `msdata:PrimaryKey="true"` nell'elemento **key**.  
  
 Il valore della proprietà **ConstraintName** di **UniqueConstraint** nel **DataSet** corrisponde al valore dell'attributo **msdata:ConstraintName** specificato nell'elemento **key** dello schema.  
  
## Vedere anche  
 [Mapping dei vincoli di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
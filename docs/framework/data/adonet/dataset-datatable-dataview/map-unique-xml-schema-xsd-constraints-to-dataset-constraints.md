---
title: "Mappare i vincoli univoci di XML Schema (XSD) ai vincoli del DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56da90bf-21d3-4d1a-8bb8-de908866b78d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Mappare i vincoli univoci di XML Schema (XSD) ai vincoli del DataSet
In uno schema XSD \(XML Schema Definition Language\), l'elemento **unique** consente di specificare il vincolo di univocità su un elemento o un attributo.  Durante il processo di conversione di un XML Schema in uno schema relazionale, viene eseguito il mapping del vincolo univoco specificato su un elemento o un attributo dell'XML Schema a un vincolo univoco del tipo <xref:System.Data.DataTable> nel tipo <xref:System.Data.DataSet> corrispondente generato.  
  
 Nella tabella seguente vengono brevemente descritti gli attributi **msdata** che è possibile specificare per l'elemento **unique**.  
  
|Nome attributo|Descrizione|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|Se questo attributo viene specificato, il relativo valore viene usato come nome del vincolo.  In caso contrario, il valore per il nome del vincolo viene fornito dall'attributo **name**.|  
|**msdata:PrimaryKey**|Se `PrimaryKey="true"` è presente nell'elemento **unique**, viene creato un vincolo univoco la cui proprietà **IsPrimaryKey** è impostata su **true**.|  
  
 Nell'esempio seguente viene illustrato un XML Schema in cui l'elemento **unique** viene usato per specificare un vincolo di univocità.  
  
```  
<xs:schema id="SampleDataSet"   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:integer"   
           minOccurs="0"/>  
        <xs:element name="CompanyName" type="xs:string"   
           minOccurs="0"/>  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
  
 <xs:element name="SampleDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:unique      
msdata:ConstraintName="UCustID"      
name="UniqueCustIDConstr" >        
<xs:selector xpath=".//Customers" />        
<xs:field xpath="CustomerID" />      
</xs:unique>  
</xs:element>  
</xs:schema>  
```  
  
 L'elemento **unique** dello schema consente di specificare che è necessario che il valore dell'elemento figlio **CustomerID** sia univoco per tutti gli elementi **Customers** in un'istanza del documento.  Durante la compilazione dell'oggetto **DataSet**, lo schema viene letto dal processo di mapping, che genera la seguente tabella:  
  
```  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 Il processo di mapping consente inoltre di creare un vincolo univoco nella colonna **CustomerID**, come illustrato nel seguente **DataSet**.  Per semplicità vengono mostrate solo le proprietà rilevanti.  
  
```  
  
      DataSetName: MyDataSet  
TableName: Customers  
  ColumnName: CustomerID  
      AllowDBNull: True  
      Unique: True  
  ConstraintName: UcustID  
      Type: UniqueConstraint  
      Table: Customers  
      Columns: CustomerID   
      IsPrimaryKey: False  
```  
  
 Nel **DataSet** generato la proprietà **IsPrimaryKey** viene impostata su **False** per il vincolo univoco.  La proprietà **unique** per la colonna indica che è necessario che i valori della colonna **CustomerID** siano univoci, ma per tali valori sono consentiti riferimenti null, come specificato nella proprietà **AllowDBNull** della colonna.  
  
 Se si modifica lo schema e si imposta il valore dell'attributo facoltativo **msdata:PrimaryKey** su **True**, verrà creato il vincolo univoco per la tabella.  La proprietà **AllowDBNull** della colonna viene impostata su **False** e la proprietà **IsPrimaryKey** del vincolo viene impostata su **True**, rendendo quindi la colonna **CustomerID** una colonna di chiave primaria.  
  
 È possibile specificare un vincolo univoco per una combinazione di elementi o attributi nell'XML Schema.  Nell'esempio seguente viene illustrato come specificare che è necessario che una combinazione di valori **CustomerID** e **CompanyName** sia univoca per tutti gli elementi **Customers** in qualsiasi istanza mediante l'aggiunta di un elemento **xs:field** nello schema.  
  
```  
  
      <xs:unique     
         msdata:ConstraintName="SomeName"    
         name="UniqueCustIDConstr" >   
  <xs:selector xpath=".//Customers" />   
  <xs:field xpath="CustomerID" />   
  <xs:field xpath="CompanyName" />   
</xs:unique>  
```  
  
 Di seguito viene riportato il vincolo creato nell'oggetto **DataSet** risultante.  
  
```  
ConstraintName: SomeName  
  Table: Customers  
  Columns: CustomerID CompanyName   
  IsPrimaryKey: False  
```  
  
## Vedere anche  
 [Mapping dei vincoli di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
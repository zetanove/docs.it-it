---
title: "Guida di riferimento rapido a Entity SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: e53dad9e-5e83-426e-abb4-be3e78e3d6dc
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Guida di riferimento rapido a Entity SQL
In questo argomento viene fornita una guida di riferimento rapido alle query [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  Le query incluse in questo argomento sono basate sul modello Sales di AdventureWorks.  
  
## Valori letterali  
  
### String  
 I valori letterali carattere di tipo String possono essere Unicode e non Unicode.  Alle stringhe Unicode viene anteposta una N,  Ad esempio `N'hello'`.  
  
 Di seguito è illustrato un esempio di valore letterale stringa Non\-Unicode:  
  
```  
'hello'  
--same as  
"hello"  
```  
  
 Output:  
  
|Valore|  
|------------|  
|hello|  
  
### DateTime  
 Nei valori letterali di tipo DateTime sono obbligatorie sia la parte relativa alla data che quella relativa all'ora.  Non sono previsti valori predefiniti.  
  
 Esempio:  
  
```  
DATETIME '2006-12-25 01:01:00.000'   
--same as  
DATETIME '2006-12-25 01:01'  
```  
  
 Output:  
  
|Valore|  
|------------|  
|12\/25\/2006 1:01:00 AM|  
  
### Integer  
 I valori letterali Integer possono essere di tipo Int32 \(123\), UInt32 \(123U\), Int64 \(123L\) e UInt64 \(123UL\).  
  
 Esempio:  
  
```  
--a collection of integers  
{1, 2, 3}  
```  
  
 Output:  
  
|Valore|  
|------------|  
|1|  
|2|  
|3|  
  
### Altro  
 Gli altri valori letterali supportati da [!INCLUDE[esql](../../../../../../includes/esql-md.md)] sono Guid, Binary, Float\/Double, Decimal e `null`.  I valori letterali Null in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] sono considerati compatibili con tutti i tipi ne modello concettuale.  
  
## Costruttori di tipo  
  
### ROW  
 [ROW](../../../../../../docs/framework/data/adonet/ef/language-reference/row-entity-sql.md) consente di costruire un valore \(record\) strutturalmente tipizzato anonimo, come in: `ROW(1 AS myNumber, ‘Name’ AS myName).`  
  
 Esempio:  
  
```  
SELECT VALUE row (product.ProductID as ProductID, product.Name   
    as ProductName) FROM AdventureWorksEntities.Product AS product  
```  
  
 Output:  
  
|ProductID|Nome|  
|---------------|----------|  
|1|Adjustable Race|  
|879|All\-Purpose Bike Stand|  
|712|AWC Logo Cap|  
|...|...|  
  
### MULTISET  
 [MULTISET](../../../../../../docs/framework/data/adonet/ef/language-reference/multiset-entity-sql.md) consente di costruire raccolte, ad esempio:  
  
 `MULTISET(1,2,2,3)` `--same as`\-`{1,2,2,3}.`  
  
 Esempio:  
  
```  
SELECT VALUE product FROM AdventureWorksEntities.Product AS product WHERE product.ListPrice IN MultiSet (125, 300)  
```  
  
 Output:  
  
|ProductID|Nome|ProductNumber|…|  
|---------------|----------|-------------------|-------|  
|842|Touring\-Panniers, Large|PA\-T100|…|  
  
### Oggetto  
 [Costruttore di tipo denominato](../../../../../../docs/framework/data/adonet/ef/language-reference/named-type-constructor-entity-sql.md) consente di costruire oggetti definiti dall'utente \(denominati\), ad esempio `person("abc", 12)`.  
  
 Esempio:  
  
```  
SELECT VALUE AdventureWorksModel.SalesOrderDetail (o.SalesOrderDetailID, o.CarrierTrackingNumber, o.OrderQty,   
o.ProductID, o.SpecialOfferID, o.UnitPrice, o.UnitPriceDiscount,   
o.rowguid, o.ModifiedDate) FROM AdventureWorksEntities.SalesOrderDetail   
AS o  
```  
  
 Output:  
  
|SalesOrderDetailID|CarrierTrackingNumber|OrderQty|ProductID|...|  
|------------------------|---------------------------|--------------|---------------|---------|  
|1|4911\-403C\-98|1|776|...|  
|2|4911\-403C\-98|3|777|...|  
|...|...|...|...|...|  
  
## Riferimenti  
  
### REF  
 [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md) consente di creare un riferimento a un'istanza di un tipo di entità.  La query seguente restituisce ad esempio i riferimenti a ogni entità Order nel set di entità Orders:  
  
```  
SELECT REF(o) AS OrderID FROM Orders AS o  
```  
  
 Output:  
  
|Valore|  
|------------|  
|1|  
|2|  
|3|  
|...|  
  
 Nell'esempio seguente viene usato l'operatore di estrazione delle proprietà \(.\) per accedere a una proprietà di un'entità.  Quando viene usato l'operatore di estrazione delle proprietà, il riferimento viene automaticamente dereferenziato.  
  
 Esempio:  
  
```  
SELECT VALUE REF(p).Name FROM   
    AdventureWorksEntities.Product as p  
```  
  
 Output:  
  
|Valore|  
|------------|  
|Adjustable Race|  
|All\-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### DEREF  
 [DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md) consente di dereferenziare un valore di riferimento e di produrre il risultato di tale operazione.  La query seguente restituisce ad esempio le entità Order per ogni oggetto Order nel set di entità Orders: `SELECT DEREF(o2.r) FROM (SELECT REF(o) AS r FROM LOB.Orders AS o) AS o2`.  
  
 Esempio:  
  
```  
SELECT VALUE DEREF(REF(p)).Name FROM   
    AdventureWorksEntities.Product as p  
```  
  
 Output:  
  
|Valore|  
|------------|  
|Adjustable Race|  
|All\-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### CREATEREF e KEY  
 [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md) consente di creare un riferimento passando una chiave.  [KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md) consente di estrarre la parte relativa alla chiave da un'espressione con un riferimento a un tipo.  
  
 Esempio:  
  
```  
SELECT VALUE Key(CreateRef(AdventureWorksEntities.Product, row(p.ProductID)))   
    FROM AdventureWorksEntities.Product as p  
```  
  
 Output:  
  
|ProductID|  
|---------------|  
|980|  
|365|  
|771|  
|...|  
  
## Funzioni  
  
### Canoniche  
 Lo spazio dei nomi per le [funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md) è Edm, come in `Edm.Length("string")`.  Non è necessario specificare lo spazio dei nomi a meno che non venga importato un altro spazio dei nomi contenente una funzione con lo stesso nome della funzione canonica.  Se due spazi dei nomi includono la stessa funzione, l'utente deve specificare il nome completo.  
  
 Esempio:  
  
```  
SELECT Length(c. FirstName) As NameLen FROM   
    AdventureWorksEntities.Contact AS c   
    WHERE c.ContactID BETWEEN 10 AND 12  
```  
  
 Output:  
  
|NameLen|  
|-------------|  
|6|  
|6|  
|5|  
  
### Specifiche del provider Microsoft  
 Le [funzioni specifiche del provider Microsoft](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md) sono incluse nello spazio dei nomi di `SqlServer`.  
  
 Esempio:  
  
```  
SELECT SqlServer.LEN(c.EmailAddress) As EmailLen FROM   
    AdventureWorksEntities.Contact AS c WHERE   
    c.ContactID BETWEEN 10 AND 12  
```  
  
 Output:  
  
|EmailLen|  
|--------------|  
|27|  
|27|  
|26|  
  
## Spazi dei nomi  
 [USING](../../../../../../docs/framework/data/adonet/ef/language-reference/using-entity-sql.md) specifica gli spazi dei nomi usati in un'espressione di query.  
  
 Esempio:  
  
```  
using SqlServer; LOWER('AA');  
```  
  
 Output:  
  
|Valore|  
|------------|  
|aa|  
  
## Paging  
 Il paging può essere espresso dichiarando le sottoclausole [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md) e [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md) nella clausola [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md).  
  
 Esempio:  
  
```  
SELECT c.ContactID as ID, c.LastName as Name FROM   
    AdventureWorks.Contact AS c ORDER BY c.ContactID SKIP 9 LIMIT 3;  
```  
  
 Output:  
  
|ID|Nome|  
|--------|----------|  
|10|Adina|  
|11|Agcaoili|  
|12|Aguilar|  
  
## Raggruppamento  
 [GROUPING BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md) specifica i gruppi nei quali devono essere inseriti gli oggetti restituiti da un'espressione \([SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)\) di query.  
  
 Esempio:  
  
```  
SELECT VALUE name FROM AdventureWorksEntities.Product as P   
    GROUP BY P.Name HAVING MAX(P.ListPrice) > 5  
```  
  
 Output:  
  
|name|  
|----------|  
|LL Mountain Seat Assembly|  
|ML Mountain Seat Assembly|  
|HL Mountain Seat Assembly|  
|...|  
  
## Navigazione  
 L' operatore di navigazione delle relazioni consente di eseguire la navigazione in una relazione da un'entità \(entità finale di origine\) a un'altra \(entità finale di destinazione\).  [NAVIGATE](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md) accetta il tipo di relazione qualificato come \<spazio dei nomi\>.\<nome del tipo di relazione\>.  NAVIGATE restituisce Ref\<T\> se la cardinalità dell'entità finale è 1.  Se la cardinalità dell'entità finale è n, viene restituito Collection\<Ref\<T\>\>  
  
 Esempio:  
  
```  
SELECT a.AddressID, (SELECT VALUE DEREF(v) FROM   
    NAVIGATE(a, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS v)   
    FROM AdventureWorksEntities.Address AS a  
```  
  
 Output:  
  
|AddressID|  
|---------------|  
|1|  
|2|  
|3|  
|...|  
  
## SELECT VALUE e SELECT  
  
### SELECT VALUE  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce la clausola SELECT VALUE per consentire di ignorare la costruzione di riga implicita.  In una clausola SELECT VALUE può essere specificato un solo elemento.  Quando viene usata questa clausola, non viene costruito alcun wrapper di riga intorno agli elementi nella clausola SELECT e può essere prodotta una raccolta della forma desiderata, ad esempio `SELECT VALUE a`.  
  
 Esempio:  
  
```  
SELECT VALUE p.Name FROM AdventureWorksEntities.Product as p  
```  
  
 Output:  
  
|Nome|  
|----------|  
|Adjustable Race|  
|All\-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### SELECT  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce inoltre il costruttore ROW per la costruzione di righe arbitrarie.  SELECT accetta uno o più elementi nella proiezione e restituisce un record di dati con campi, ad esempio `SELECT a, b, c`.  
  
 Esempio:  
  
 SELECT p.Name, p.ProductID FROM AdventureWorksEntities.Product as p Output:  
  
|Nome|ProductID|  
|----------|---------------|  
|Adjustable Race|1|  
|All\-Purpose Bike Stand|879|  
|AWC Logo Cap|712|  
|...|...|  
  
## Espressione CASE  
 L'[espressione CASE](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md) valuta un set di espressioni booleane per determinare il risultato.  
  
 Esempio:  
  
```  
CASE WHEN AVG({25,12,11}) < 100 THEN TRUE ELSE FALSE END  
```  
  
 Output:  
  
|Valore|  
|------------|  
|TRUE|  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)
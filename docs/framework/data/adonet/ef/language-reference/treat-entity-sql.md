---
title: "TREAT (Entity SQL) | Microsoft Docs"
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
  - "ESQL"
ms.assetid: 5b77f156-55de-4cb4-8154-87f707d4c635
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# TREAT (Entity SQL)
Consente di trattare un oggetto di un tipo di base particolare come oggetto del tipo derivato specificato.  
  
## Sintassi  
  
```  
  
TREAT (expression as type)  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione di query valida che restituisce un'entità.  
  
> [!NOTE]
>  Il tipo dell'espressione specificata deve essere un sottotipo del tipo di dati specificato oppure il tipo di dati deve essere un sottotipo del tipo di espressione.  
  
 `type`  
 Tipo di entità. Il tipo deve essere qualificato da uno spazio dei nomi.  
  
> [!NOTE]
>  L'espressione specificata deve essere un sottotipo del tipo di dati specificato oppure il tipo di dati deve essere un sottotipo dell'espressione.  
  
## Valore restituito  
 Valore del tipo di dati specificato.  
  
## Note  
 TREAT viene usato per eseguire l'upcast tra classi correlate. Se, ad esempio, `Employee` deriva da `Person` e p è di tipo `Person`, `TREAT(p AS NamespaceName.Employee)` consente di eseguire l'upcast di un'istanza generica di `Person` a `Employee`, ovvero consente di trattare p come `Employee`.  
  
 TREAT viene usato negli scenari di ereditarietà dove è possibile eseguire una query simile alla seguente:  
  
```  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)   
```  
  
 Questa query consente di eseguire l'upcast delle entità `Person` al tipo `Employee`. Se il valore di p non è di tipo `Employee`, l'espressione restituisce il valore `null`.  
  
> [!NOTE]
>  L'espressione specificata```Employee``` deve essere un sottotipo del tipo di dati specificato `Person` oppure il tipo di dati deve essere un sottotipo dell'espressione. In caso contrario, l'espressione comporterà la generazione di un errore in fase di compilazione.  
  
 Nella tabella seguente viene illustrato il comportamento di TREAT su alcuni modelli tipici e su alcuni modelli meno comuni. Tutte le eccezioni vengono generate sul lato client prima che il provider venga richiamato:  
  
|Criterio|Comportamento|  
|--------------|-------------------|  
|`TREAT (null AS EntityType)`|Restituisce `DbNull`.|  
|`TREAT (null AS ComplexType)`|Genera un'eccezione.|  
|`TREAT (null AS RowType)`|Genera un'eccezione\/|  
|`TREAT (EntityType AS EntityType)`|Restituisce `EntityType` o `null`.|  
|`TREAT (ComplexType AS ComplexType)`|Genera un'eccezione.|  
|`TREAT (RowType AS RowType)`|Genera un'eccezione.|  
  
## Esempio  
 Nella query [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguente viene usato l'operatore TREAT per convertire un oggetto del tipo Course in una raccolta di oggetti del tipo OnsiteCourse. La query è basata sul [modello School](http://msdn.microsoft.com/it-it/859a9587-81ea-4a45-9bc0-f8d330e1adac).  
  
 [!code-csharp[DP EntityServices Concepts 2#TREAT_ISOF](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#treat_isof)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Tipi strutturati nullable](../../../../../../docs/framework/data/adonet/ef/language-reference/nullable-structured-types-entity-sql.md)
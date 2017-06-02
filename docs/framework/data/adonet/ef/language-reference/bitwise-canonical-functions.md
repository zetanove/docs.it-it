---
title: "Funzioni canoniche bit per bit | Microsoft Docs"
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
ms.assetid: 993868ca-16e3-47b6-9915-c29cd63b0a21
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Funzioni canoniche bit per bit
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] include funzioni canoniche bit per bit.  
  
## Note  
 Nella tabella seguente sono illustrate le funzioni canoniche bit per bit [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  Queste funzioni restituiscono `Null` se viene specificato l'input `Null`.  Il tipo restituito delle funzioni sarà uguale ai tipi di argomenti.  Gli argomenti devono essere dello stesso tipo, se la funzione ne accetta più di uno.  Per eseguire operazioni bit per bit tra tipi diversi, è necessario eseguire il cast in modo esplicito sullo stesso tipo.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|`BitWiseAnd (` `value1` `,`  `value2` `)`|Restituisce la congiunzione bit per bit di `value1` e `value2` come tipo di `value1` e `value2`.<br /><br /> **Argomenti**<br /><br /> `Byte`, `Int16`, `Int32` e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 1.`<br /><br /> `BitWiseAnd(1,3)`|  
|`BitWiseNot (` `value` `)`|Restituisce la negazione bit per bit di `value`.<br /><br /> **Argomenti**<br /><br /> `Byte`, `Int16`, `Int32` e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns -4.`<br /><br /> `BitWiseNot(3)`|  
|`BitWiseOr (` `value1` `,`  `value2` `)`|Restituisce la disgiunzione bit per bit di `value1` e `value2` come tipo di `value1` e `value2`.<br /><br /> **Argomenti**<br /><br /> `Byte`, `Int16`, `Int32` e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 3.`<br /><br /> `BitWiseOr(1,3)`|  
|`BitWiseXor (` `value1` `,`  `value2` `)`|Restituisce la disgiunzione esclusiva bit per bit di `value1` e `value2` come tipo di `value1` e `value2`.<br /><br /> **Argomenti**<br /><br /> `Byte`, `Int16`, `Int32` e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 2.`<br /><br /> `BitWiseXor (1,3)`|  
  
## Vedere anche  
 [Funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
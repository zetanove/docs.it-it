---
title: "Clausola Group By (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.QueryGroupByInto"
  - "vb.QueryGroupBy"
  - "vb.QueryGroupRef"
  - "vb.QueryGroupInto"
  - "vb.QueryGroup"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "query [Visual Basic], Group By"
  - "Group By (istruzione)"
  - "clausola Group By"
ms.assetid: b1b5dcea-6654-473b-a2db-01f7e4c265d7
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Clausola Group By (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Raggruppa gli elementi di un risultato della query. Può essere usata anche per applicare funzioni di aggregazione a ogni gruppo. L'operazione di raggruppamento è basata su una o più chiavi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Group [ listField1 [, listField2 [...] ] By keyExp1 [, keyExp2 [...] ]  
  Into aggregateList  
```  
  
## <a name="parts"></a>Parti  
  
-   `listField1`, `listField2`  
  
     Parametro facoltativo. Uno o più campi della variabile o delle variabili di query che identificano in modo esplicito i campi da includere nel risultato raggruppato. Se non sono specificati campi, tutti i campi della variabile o delle variabili di query vengono inclusi nel risultato raggruppato.  
  
-   `keyExp1`  
  
     Obbligatorio. Espressione che identifica la chiave da usare per determinare i gruppi di elementi. È possibile specificare più di una chiave per specificare una chiave composta.  
  
-   `keyExp2`  
  
     Facoltativo. Uno o più tasti aggiuntivi che vengono combinati con `keyExp1` per creare una chiave composta.  
  
-   `aggregateList`  
  
     Obbligatorio. Una o più espressioni che identificano come vengono aggregati i gruppi. Per identificare un nome di membro per i risultati raggruppati, usare la parola chiave `Group` , che può essere in uno dei seguenti formati:  
  
    ```  
    Into Group  
    ```  
  
     -oppure-  
  
    ```  
    Into <alias> = Group  
    ```  
  
     È anche possibile includere funzioni di aggregazione da applicare al gruppo.  
  
## <a name="remarks"></a>Note  
 È possibile usare la clausola `Group By` per suddividere i risultati di una query in gruppi. Il raggruppamento è basato su una chiave o una chiave composta costituita da più chiavi. Gli elementi associati ai valori della chiave corrispondenti vengono inclusi nello stesso gruppo.  
  
 Per identificare il nome del membro che viene usato per fare riferimento al gruppo, usare il parametro `aggregateList` della clausola `Into` e la parola chiave `Group` . È anche possibile includere funzioni di aggregazione nella clausola `Into` per calcolare i valori per gli elementi raggruppati. Per un elenco di funzioni di aggregazione standard, vedere [Aggregate Clause](../../../visual-basic/language-reference/queries/aggregate-clause.md).  
  
## <a name="example"></a>Esempio  
 L'esempio di codice seguente raggruppa un elenco di clienti in base alla località (paese) e fornisce un conteggio dei clienti in ogni gruppo. I risultati vengono ordinati in base al nome del paese. I risultati raggruppati vengono ordinati in base al nome della città.  
  
 [!code-vb[VbSimpleQuerySamples#11](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/group-by-clause_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Query](../../../visual-basic/language-reference/queries/queries.md)   
 [Clausola SELECT](../../../visual-basic/language-reference/queries/select-clause.md)   
 [Clausola FROM](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Clausola Order By](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Clausola Aggregate](../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Clausola Group Join](../../../visual-basic/language-reference/queries/group-join-clause.md)
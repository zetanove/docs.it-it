---
title: "ReDim Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ReDim"
  - "vb.Preserve"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "fixed-length strings, declaring"
  - "ReDim statement, syntax"
  - "dynamic arrays, ReDim statement"
  - "arrays [Visual Basic], reallocating"
  - "arrays [Visual Basic], reinitializing"
  - "arrays [Visual Basic], dimensions"
  - "scalars, and arrays"
  - "scalars"
  - "declarations, dynamic arrays"
  - "variables [Visual Basic], scalar"
  - "ReDim statement"
  - "data types [Visual Basic], assigning"
  - "As keyword, in ReDim statement"
  - "To keyword, ReDim statement"
  - "arrays [Visual Basic], declaring"
  - "Preserve keyword, ReDim statement"
  - "storage, allocating"
  - "arrays [Visual Basic], and scalars"
  - "declaration statements"
  - "scalar variables"
ms.assetid: ad1c5e07-dcd7-4ae1-a79e-ad3f2dcc2083
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# ReDim Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Rialloca lo spazio di archiviazione per una variabile di matrice.  
  
## Sintassi  
  
```  
ReDim [ Preserve ] name(boundlist) [ ,  name(boundlist) [, ... ] ]  
```  
  
## Parti  
  
|Termine|Definizione|  
|-------------|-----------------|  
|`Preserve`|Parametro facoltativo.  Modificatore utilizzato per conservare i dati nella matrice esistente quando si modifica soltanto la grandezza dell'ultima dimensione.|  
|`name`|Necessario.  Nome della variabile di matrice.  Vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`boundlist`|Necessario.  Elenco di limiti relativi a ogni dimensione della matrice ridefinita.|  
  
## Note  
 È possibile utilizzare l'istruzione `ReDim` per modificare una o più dimensioni di una matrice che è stata già dichiarata.  Se si dispone di una matrice di grandi dimensioni e alcuni degli elementi di questa non sono più necessari, `ReDim` consente di liberare memoria riducendo le dimensioni della matrice.  D’altra parte, se la matrice necessita di più elementi, `ReDim` è in grado di aggiungerli.  
  
 L'istruzione `ReDim` è destinata solo alle matrici.  Non è valida per valori scalari \(variabili che contengono un unico valore\), raccolte o strutture.  Tenere presente che se l'utente dichiara che una variabile è di tipo `Array`, l'istruzione `ReDim` non dispone di sufficienti informazioni sulla tipologia e non può creare la nuova matrice.  
  
 Si può usare `ReDim` solo a livello di routine.  Pertanto, il contesto della dichiarazione relativo alla variabile deve essere una routine. Di conseguenza, non può essere un file di origine, uno spazio dei nomi, un'interfaccia, una classe, una struttura, un modulo o un blocco.  Per altre informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
## Regole  
  
-   **Variabili multiple.** È possibile ridimensionare numerose variabili di matrice nella stessa istruzione di dichiarazione e specificare i componenti `name` e `boundlist` per ogni variabile.  Nel caso di più variabili, è possibile separarle mediante virgole.  
  
-   **Limiti di matrice.** Ogni voce in `boundlist` è in grado di specificare i limiti inferiori e superiori di tale dimensione.  Il limite inferiore è sempre pari a 0 \(zero\).  Il limite superiore rappresenta il valore di indice più alto possibile per la dimensione, non la lunghezza della dimensione \(vale a dire, il limite superiore più uno\).  L'indice di ogni dimensione può variare tra 0 e il relativo valore di limite superiore.  
  
     Il numero di dimensioni in `boundlist` deve corrispondere al numero originale di dimensioni \(livello\) della matrice.  
  
-   **Tipi di dati.** L'istruzione `ReDim` non è in grado di modificare il tipo di dati di una variabile di matrice oppure i relativi elementi.  
  
-   **Inizializzazione.** L'istruzione `ReDim` non può fornire nuovi valori di inizializzazione per gli elementi della matrice.  
  
-   **Classifica.** L'istruzione `ReDim` non può modificare la classificazione \(numero di dimensioni\) della matrice.  
  
-   **Ridimensionamento con Preserve.** Se si utilizza `Preserve`, è possibile ridimensionare solo l'ultima dimensione della matrice.  Per ogni dimensione, è necessario specificare il limite della matrice esistente.  
  
     Ad esempio, se la matrice contiene solo una dimensione, è possibile ridimensionarla e mantenere tutto il contenuto della matrice, poiché si sta modificando l'ultima e unica dimensione.  Tuttavia, se la matrice dispone di due o più dimensioni e si utilizza `Preserve`, è possibile modificare i valori soltanto per l'ultima dimensione.  
  
-   **Proprietà.** È possibile utilizzare `ReDim` su una proprietà che contiene una matrice di valori.  
  
## Comportamento  
  
-   **Sostituzione della matrice** `ReDim` rilascia la matrice esistente e crea una nuova matrice con la stessa classificazione.  La nuova matrice sostituisce quella rilasciata nella variabile di matrice.  
  
-   **Inizializzazione senza Preserve.** Se non si specifica `Preserve`, `ReDim` inizializza gli elementi della nuova matrice utilizzando il valore predefinito per i loro tipi di dati.  
  
-   **Inizializzazione con Preserve.** Se si specifica `Preserve`, Visual Basic copia gli elementi dalla matrice esistente in quella nuova.  
  
## Esempio  
 Nell'esempio seguente viene aumentata la grandezza dell'ultima dimensione di una matrice dinamica senza perdere i dati presenti nella matrice; in seguito, viene ridotta la dimensione con perdita di dati parziali.  Infine, viene ridotta la dimensione del relativo valore originale e vengono inizializzati di nuovo tutti gli elementi della matrice.  
  
 [!code-vb[VbVbalrStatements#52](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/redim-statement_1.vb)]  
  
 L'istruzione `Dim` crea una nuova matrice con tre dimensioni.  Ogni dimensione viene dichiarata con un limite pari a 10. In questo modo l'indice della matrice per ogni dimensione può essere compreso tra 0 e 10.  Nella seguente discussione, si fa riferimento alle tre dimensioni come livello, riga e colonna.  
  
 La prima `ReDim` crea una nuova matrice che sostituisce quella esistente nella `intArray` di variabile.  `ReDim` copia tutti gli elementi dalla matrice esistente in quella nuova.  Inoltre, consente di aggiungere altre 10 colonne alla fine di ogni riga di tutti i livelli e consente di inizializzare gli elementi in queste nuove colonne su 0 \(valore predefinito\) di `Integer`, ovvero il tipo di elemento della matrice.  
  
 La seconda `ReDim` crea una nuova matrice e copia tutti gli elementi adeguati.  Tuttavia, cinque colonne vengono perse alla fine di ogni riga relativa a ogni livello.  Ciò non rappresenta un problema se l'utente non ha più la necessità di utilizzare tali colonne.  La riduzione delle dimensioni di una grande matrice può liberare memoria che non è più necessaria.  
  
 La terza `ReDim` crea una nuova matrice e rimuove altre cinque colonne dalla fine di ogni riga relativa a ogni livello.  Questa volta non copia gli elementi esistenti.  Questa istruzione consente di ripristinare le dimensioni originali della matrice.  Dal momento che l'istruzione non include il modificatore `Preserve`, imposta i valori predefiniti originali di tutti gli elementi della matrice.  
  
 Per ulteriori esempi, vedere [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## Vedere anche  
 <xref:System.IndexOutOfRangeException>   
 [Const Statement](../../../visual-basic/language-reference/statements/const-statement.md)   
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Erase Statement](../../../visual-basic/language-reference/statements/erase-statement.md)   
 [Nothing](../../../visual-basic/language-reference/nothing.md)   
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)
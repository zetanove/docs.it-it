---
title: "Using Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.using"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "resource disposal"
  - "Try...Catch...Finally statements, equivalent to Using statement"
  - "resources [Visual Basic], disposing"
  - "Using statement"
ms.assetid: 665d1580-dd54-4e96-a9a9-6be2a68948f1
caps.latest.revision: 36
caps.handback.revision: 36
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Using Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara l'inizio di un blocco `Using` e facoltativamente acquisisce le risorse di sistema controllate dal blocco.  
  
## Sintassi  
  
```  
Using { resourcelist | resourceexpression }  
    [ statements ]  
End Using  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`resourcelist`|Obbligatoria se non viene fornito il parametro `resourceexpression`.  Elenco di una o più risorse di sistema che controlli di questo blocco `Using`, separati da virgole.|  
|`resourceexpression`|Obbligatoria se non viene fornito il parametro `resourcelist`.  Variabile di riferimento o espressione che fa riferimento a una risorsa di sistema che questo blocco `Using` deve controllare.|  
|`statements`|Opzionale.  Blocco di istruzioni eseguite dal blocco `Using`.|  
|`End Using`|Necessario.  Termina la definizione del blocco `Using` ed elimina tutte le risorse che esso controlla.|  
  
 La sintassi delle singole risorse di `resourcelist` utilizza le parti seguenti:  
  
 `resourcename As New resourcetype [ ( [ arglist ] ) ]`  
  
 In alternativa  
  
 `resourcename As resourcetype = resourceexpression`  
  
## Parti di resourcelist  
  
|||  
|-|-|  
|Termine|Definizione|  
|`resourcename`|Necessario.  Variabile che fa riferimento a una risorsa di sistema controllata dal blocco `Using`.|  
|`New`|Obbligatoria se l'istruzione `Using` acquisisce la risorsa.  Se la risorsa è già stata acquisita, utilizzare la seconda alternativa di sintassi.|  
|`resourcetype`|Necessario.  Classe della risorsa.  La classe deve implementare l'interfaccia <xref:System.IDisposable>.|  
|`arglist`|Opzionale.  Elenco di argomenti passati al costruttore per creare un'istanza del parametro `resourcetype`.  Vedere [Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md).|  
|`resourceexpression`|Necessario.  Variabile o espressione che fa riferimento a una risorsa di sistema che soddisfa i requisiti del parametro `resourcetype`.  Se si utilizza la seconda alternativa di sintassi, è necessario acquisire la risorsa prima di passare il controllo all'istruzione `Using`.|  
  
## Note  
 Talvolta il codice richiede una risorsa non gestita, come ad esempio un handle di file, un wrapper COM o una connessione SQL.  Un blocco `Using` garantisce che una o più di queste risorse vengano eliminate quando non sono più necessarie al codice.  In questo modo, esse tornano disponibili per altro codice.  
  
 Le risorse gestite vengono eliminate dal Garbage Collector \(GC\) di .NET Framework senza necessità di scrivere altro codice.  Non è necessario un blocco `Using` per le risorse gestite.  Tuttavia, è comunque possibile utilizzare un blocco `Using` per forzare l'eliminazione di una risorsa gestita invece di attendere il Garbage Collector.  
  
 Un blocco `Using` è suddiviso in tre parti, ovvero acquisizione, uso ed eliminazione.  
  
-   Per *acquisizione* si intende la creazione di una variabile e la sua inizializzazione affinché faccia riferimento alla risorsa di sistema.  L'istruzione `Using` può acquisire una o più risorse oppure è possibile acquisire specificamente una risorsa prima di accedere al blocco e fornirla all'istruzione `Using`.  Se si fornisce il parametro `resourceexpression`, è necessario acquisire la risorsa prima di passare il controllo all'istruzione `Using`.  
  
-   Per *uso* si intende accedere alle risorse e utilizzarle per eseguire delle operazioni.  Le istruzioni fra `Using` e `End Using` rappresentano l'uso delle risorse.  
  
-   Per *eliminazione* si intende chiamare il metodo <xref:System.IDisposable.Dispose%2A> per l'oggetto in `resourcename`.  Tale operazione consente all'oggetto di terminare correttamente le relative risorse.  L'istruzione `End Using` elimina le risorse che si trovano sotto il controllo del blocco `Using`.  
  
## Comportamento  
 Un blocco `Using` si comporta come una costruzione `Try`...`Finally` in cui il blocco `Try` utilizza le risorse e il blocco `Finally` le elimina.  Per questo motivo, il blocco `Using` garantisce l'eliminazione delle risorse, indipendentemente dalle modalità con cui viene terminato il blocco di istruzioni.  Questo meccanismo è valido anche per le eccezioni non gestite, con esclusione dell'eccezione <xref:System.StackOverflowException>.  
  
 L'ambito di ogni variabile di risorsa acquisita dall'istruzione `Using` è limitato al blocco `Using`.  
  
 Se si specificano più risorse di sistema nell'istruzione `Using`, si ottiene lo stesso effetto ottenuto annidando dei blocchi `Using` uno nell'altro.  
  
 Se `resourcename` è `Nothing`, alcuna chiamata a <xref:System.IDisposable.Dispose%2A> viene eseguita e non viene generata alcuna eccezione.  
  
## Gestione strutturata delle eccezioni all'interno di un blocco Using  
 Se è necessario gestire un'eccezione che potrebbe verificarsi all'interno del blocco `Using`, è possibile aggiungergli una costruzione `Try`...`Finally` completa.  Se è necessario gestire il caso in cui l'istruzione `Using` non ha esito positivo nell'acquisizione di una risorsa, è possibile eseguire un test per verificare se il valore del parametro `resourcename` è `Nothing`.  
  
## Gestione strutturata delle eccezioni in alternativa a un blocco Using  
 Se è necessario poter controllare in modo più specifico l'acquisizione delle risorse o se è necessario altro codice nel blocco `Finally`, è possibile riscrivere il blocco `Using` come costruzione `Try`...`Finally`.  Nell'esempio seguente sono riportate le costruzioni di base di `Try` e `Using` che si equivalgono per quanto riguarda l'acquisizione e l'eliminazione di `resource`.  
  
```vb  
Using resource As New resourceType   
    ' Insert code to work with resource.  
End Using  
  
' For the acquisition and disposal of resource, the following  
' Try construction is equivalent to the Using block.  
Dim resource As New resourceType  
Try   
    ' Insert code to work with resource.  
Finally   
    If resource IsNot Nothing Then  
        resource.Dispose()   
    End If  
End Try   
```  
  
> [!NOTE]
>  il codice all'interno del blocco `Using` non deve assegnare l'oggetto in `resourcename` a un'altra variabile.  Quando si esce dal blocco `Using`, la risorsa viene eliminata e l'altra variabile non può accedere alla risorsa a cui punta.  
  
## Esempio  
 L'esempio seguente consente di creare un file denominato log.txt e produce due righe di testo al file.  L'esempio legge anche nello stesso file e visualizzare le righe di testo.  
  
 Poiché le classi <xref:System.IO.TextReader> e <xref:System.IO.TextWriter> implementano l'interfaccia <xref:System.IDisposable>, il codice può utilizzare istruzioni `Using` per garantire che il file verrà chiuso dopo la scrittura e le operazioni di lettura.  
  
 [!code-vb[VbVbalrStatements#50](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/using-statement_1.vb)]  
  
## Vedere anche  
 <xref:System.IDisposable>   
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [How to: Dispose of a System Resource](../../../visual-basic/programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md)
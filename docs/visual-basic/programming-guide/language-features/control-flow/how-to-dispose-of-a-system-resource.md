---
title: "How to: Dispose of a System Resource (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Using statement, disposing of system resources"
  - "Visual Basic code, control flow"
  - "system resources, disposing of"
  - "resources [Visual Basic], disposing of system"
  - "system resources"
  - "Using statement, Using...End Using"
  - "Using block"
ms.assetid: 8be2b239-8090-419b-8e7e-bcaa75b0ecc8
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Dispose of a System Resource (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare un blocco `Using` per garantire l'eliminazione di una risorsa da parte del sistema quando il codice esce dal blocco.  Questa funzionalità risulta utile quando si utilizza una risorsa di sistema che impiega una grande quantità di memoria o che deve essere utilizzata da altri componenti.  
  
### Per eliminare una connessione di database quando non è più utilizzata dal codice  
  
1.  Accertarsi di includere l'[Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) appropriata per la connessione di database all'inizio del file di origine \(in questo caso, lo spazio dei nomi <xref:System.Data.SqlClient>\).  
  
2.  Creare un blocco `Using` con le istruzioni `Using` ed `End Using`.  All'interno del blocco inserire il codice relativo alla connessione di database.  
  
3.  Dichiarare la connessione e creare un'istanza di quest'ultima come parte dell'istruzione `Using`.  
  
    ```  
    ' Insert the following line at the beginning of your source file.  
    Imports System.Data.SqlClient  
    Public Sub AccessSql(ByVal s As String)  
        Using sqc As New System.Data.SqlClient.SqlConnection(s)  
            MsgBox("Connected with string """ & sqc.ConnectionString & """")  
        End Using  
    End Sub  
    ```  
  
     La risorsa viene eliminata dal sistema indipendentemente dal modo con cui si esce dal blocco, compreso il caso di un'eccezione non gestita.  
  
     Tenere presente che non è possibile accedere a `sqc` dall'esterno del blocco `Using` perché il relativo ambito è limitato al blocco stesso.  
  
     È possibile utilizzare questa stessa tecnica su una risorsa di sistema, ad esempio un handle di file o un wrapper COM.  È possibile utilizzare un blocco `Using` per essere certi che la risorsa sia disponibile per altri componenti dopo l'uscita dal blocco `Using` stesso.  
  
## Vedere anche  
 <xref:System.Data.SqlClient.SqlConnection>   
 [Control Flow](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Decision Structures](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Loop Structures](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Other Control Structures](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)   
 [Nested Control Structures](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Using Statement](../../../../visual-basic/language-reference/statements/using-statement.md)
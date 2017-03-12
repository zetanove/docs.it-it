---
title: "Structures and Other Programming Elements (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "structures, arrays"
  - "procedures, structures as arguments to"
  - "objects [Visual Basic], structure elements"
  - "arrays [Visual Basic], structure elements"
  - "nested structures"
ms.assetid: 0f849313-ccd2-4c9a-acb9-69de6751c088
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Structures and Other Programming Elements (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile utilizzare strutture insieme a matrici, oggetti e routine, nonché con altre strutture.  Le interazioni fanno uso della stessa sintassi utilizzata singolarmente da questi elementi.  
  
> [!NOTE]
>  Non è possibile inizializzare alcun elemento della struttura nella dichiarazione della struttura.  È possibile assegnare valori solo agli elementi di una variabile dichiarata come un tipo di struttura.  
  
## Strutture e matrici  
 Una struttura può contenere una matrice come uno o più dei suoi elementi.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As String  
    Public purchaseDate As Date  
End Structure   
```  
  
 È possibile accedere ai valori di una matrice presente all'interno di una struttura con le stesse modalità con cui si accede alla proprietà di un oggetto.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Dim mySystem As systemInfo  
ReDim mySystem.diskDrives(3)  
mySystem.diskDrives(0) = "1.44 MB"  
```  
  
 È inoltre possibile dichiarare una matrice di strutture.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Dim allSystems(100) As systemInfo  
```  
  
 Per accedere ai componenti di questa architettura di dati si seguono le stesse regole.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
ReDim allSystems(5).diskDrives(3)  
allSystems(5).CPU = "386SX"  
allSystems(5).diskDrives(2) = "100M SCSI"  
```  
  
## Strutture e oggetti  
 Una struttura può contenere un oggetto come uno o più dei suoi elementi.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Protected Structure userInput  
    Public userName As String  
    Public inputForm As System.Windows.Forms.Form  
    Public userFileNumber As Integer  
End Structure  
```  
  
 In una dichiarazione di questo tipo si consiglia di utilizzare una classe di oggetti specifica, anziché `Object`.  
  
## Strutture e routine  
 È possibile passare una struttura come argomento di routine.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Public currentCPUName As String = "700MHz Pentium compatible"  
Public currentMemorySize As Long = 256  
Public Sub fillSystem(ByRef someSystem As systemInfo)  
    someSystem.cPU = currentCPUName  
    someSystem.memory = currentMemorySize  
    someSystem.purchaseDate = Now  
End Sub  
```  
  
 Nell'esempio precedente la struttura viene passata *per riferimento*, operazione che consente alla routine di modificare i propri elementi in modo che le modifiche abbiano effetto nel codice chiamante.  Se si desidera proteggere una struttura da tali modifiche, passarla per valore.  
  
 È inoltre possibile restituire una struttura da una routine `Function`.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Dim allSystems(100) As systemInfo  
Function findByDate(ByVal searchDate As Date) As systemInfo  
    Dim i As Integer  
    For i = 1 To 100  
        If allSystems(i).purchaseDate = searchDate Then Return allSystems(i)  
    Next i  
   ' Process error: system with desired purchase date not found.  
End Function  
```  
  
## Strutture all'interno di strutture  
 Le strutture possono contenere altre strutture.  Questa condizione è illustrata nell'esempio che segue.  
  
```vb#  
Public Structure driveInfo  
    Public type As String  
    Public size As Long  
End Structure  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As driveInfo  
    Public purchaseDate As Date  
End Structure  
```  
  
```vb#  
Dim allSystems(100) As systemInfo  
ReDim allSystems(1).diskDrives(3)  
allSystems(1).diskDrives(0).type = "Floppy"  
```  
  
 È inoltre possibile utilizzare questa tecnica per incapsulare una struttura definita in un modulo all'interno di una struttura definita in un modulo differente.  
  
 Le strutture possono contenere altre strutture per un numero arbitrario di livelli.  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [How to: Declare a Structure](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Structure Variables](../../../../visual-basic/programming-guide/language-features/data-types/structure-variables.md)   
 [Structures and Classes](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md)
---
title: "Troubleshooting Arrays (Visual Basic) | Microsoft Docs"
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
  - "troubleshooting arrays"
  - "arrays [Visual Basic], initialization errors"
  - "troubleshooting Visual Basic, arrays"
  - "arrays [Visual Basic], compilation errors"
  - "arrays [Visual Basic], declaration errors"
  - "arrays [Visual Basic], troubleshooting"
ms.assetid: f4e971c7-c0a4-4ed7-a77a-8d71039f266f
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Troubleshooting Arrays (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa pagina sono elencati alcuni problemi comuni che possono verificarsi durante l'utilizzo delle matrici.  
  
## Errori di compilazione durante la dichiarazione e l'inizializzazione di una matrice  
 Gli errori di compilazione possono dipendere da un'incomprensione delle regole relative alla dichiarazione, alla creazione e all'inizializzazione delle matrici.  Le cause di errore più comuni sono le seguenti:  
  
-   Definizione di una clausola [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md) dopo aver specificato le lunghezze delle dimensioni nella dichiarazione della variabile della matrice.  Nel codice seguente vengono illustrate le dichiarazioni non corrette di questo tipo.  
  
     `Dim INVALIDsingleDimByteArray(2) As Byte = New Byte()`  
  
     `Dim INVALIDtwoDimShortArray(1, 1) As Short = New Short(,)`  
  
     `Dim INVALIDjaggedByteArray(1)() As Byte = New Byte()()`  
  
-   Definizione di lunghezze di dimensioni per altre matrici oltre a quella di primo livello in una matrice di matrici.  Nel codice seguente viene illustrata una dichiarazione non corretta di questo tipo.  
  
     `Dim INVALIDjaggedByteArray(1)(1) As Byte`  
  
-   Omissione della parola chiave `New` durante la definizione dei valori di un elemento.  Nel codice seguente viene illustrata una dichiarazione non corretta di questo tipo.  
  
     `Dim INVALIDoneDimShortArray() As Short = Short() {0, 1, 2, 3}`  
  
-   Definizione di una clausola `New` non racchiusa tra parentesi graffe \(`{}`\).  Nel codice seguente vengono illustrate le dichiarazioni non corrette di questo tipo.  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte()`  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte(2)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(,)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(1, 1)`  
  
## Accesso a una matrice al di fuori dei limiti  
 Durante il processo di inizializzazione di una matrice viene assegnato un limite superiore e un limite inferiore a ciascuna di queste dimensioni.  Per accedere a un elemento della matrice, è necessario specificare un indice, o pedice, valido per ogni dimensione.  Se il valore dell'indice è al di sotto del limite inferiore o al di sopra del limite superiore, viene generata un'eccezione <xref:System.IndexOutOfRangeException>.  Poiché il compilatore non è in grado di rilevare questo errore, si verifica un errore in fase di esecuzione.  
  
### Definizione di limiti  
 Quando un altro componente passa una matrice al codice, ad esempio l'argomento di una routine, le dimensioni della matrice o le lunghezze delle sue dimensioni sono sconosciute.  Si consiglia di definire sempre il limite superiore di ciascuna dimensione di una matrice prima di provare ad accedere a un elemento.  Se la matrice non è stata creata con una clausola `New` di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], è possibile che il valore del limite inferiore sia diverso da 0. Per questo motivo, è consigliabile definire anche il limite inferiore.  
  
### Definizione della dimensione  
 Durante la definizione dei limiti di una matrice multidimensionale, è necessario prestare particolare attenzione al modo in cui viene specificata la dimensione.  I parametri `dimension` dei metodi <xref:System.Array.GetLowerBound%2A> e <xref:System.Array.GetUpperBound%2A> sono in base 0 e i parametri `Rank` delle funzioni [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] <xref:Microsoft.VisualBasic.Information.LBound%2A> e <xref:Microsoft.VisualBasic.Information.UBound%2A> sono in base 1.  
  
## Vedere anche  
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [How to: Initialize an Array Variable in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)
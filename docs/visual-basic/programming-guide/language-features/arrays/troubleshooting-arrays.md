---
title: Risoluzione dei problemi di matrici (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- troubleshooting arrays
- arrays [Visual Basic], initialization errors
- troubleshooting Visual Basic, arrays
- arrays [Visual Basic], compilation errors
- arrays [Visual Basic], declaration errors
- arrays [Visual Basic], troubleshooting
ms.assetid: f4e971c7-c0a4-4ed7-a77a-8d71039f266f
caps.latest.revision: 17
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: db38c0c2a4f8b74a6b862f86f426b4d8837f4424
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-arrays-visual-basic"></a>Risoluzione dei problemi relativi alle matrici (Visual Basic)
Questa pagina sono elencati alcuni problemi comuni che possono verificarsi quando si lavora con le matrici.  
  
## <a name="compilation-errors-declaring-and-initializing-an-array"></a>Errori di compilazione dichiarazione e inizializzazione di una matrice  
 Errori di compilazione possono dipendere da un'incomprensione delle regole per la dichiarazione, la creazione e inizializzazione di matrici. Le cause più comuni di errori sono i seguenti:  
  
-   Fornendo un [nuovo operatore](../../../../visual-basic/language-reference/operators/new-operator.md) clausola dopo aver specificato le lunghezze delle dimensioni nella dichiarazione di variabile di matrice. Le righe di codice seguente mostrano le dichiarazioni non valide di questo tipo.  
  
     `Dim INVALIDsingleDimByteArray(2) As Byte = New Byte()`  
  
     `Dim INVALIDtwoDimShortArray(1, 1) As Short = New Short(,)`  
  
     `Dim INVALIDjaggedByteArray(1)() As Byte = New Byte()()`  
  
-   Specifica le lunghezze delle dimensioni per più di una matrice di livello superiore di una matrice di matrici. L'esempio di codice seguente viene illustrata una dichiarazione di questo tipo non valida.  
  
     `Dim INVALIDjaggedByteArray(1)(1) As Byte`  
  
-   L'omissione di `New` parola chiave quando si specificano i valori dell'elemento. L'esempio di codice seguente viene illustrata una dichiarazione di questo tipo non valida.  
  
     `Dim INVALIDoneDimShortArray() As Short = Short() {0, 1, 2, 3}`  
  
-   Fornendo un `New` clausola senza parentesi graffe (`{}`). Le righe di codice seguente mostrano le dichiarazioni non valide di questo tipo.  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte()`  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte(2)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(,)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(1, 1)`  
  
## <a name="accessing-an-array-out-of-bounds"></a>Accesso a una matrice fuori dai limiti  
 Il processo di inizializzazione di una matrice assegna un limite superiore e inferiore di ogni dimensione. L'accesso a un elemento della matrice debba specificare un indice valido o un indice, per ogni dimensione. Se il valore dell'indice è di sotto del limite inferiore o di sopra del limite superiore, un <xref:System.IndexOutOfRangeException>risultati dell'eccezione.</xref:System.IndexOutOfRangeException> Il compilatore non è in grado di rilevare un errore di questo tipo, si verifica un errore in fase di esecuzione.  
  
### <a name="determining-bounds"></a>Determinazione dei limiti  
 Se un altro componente passa una matrice al codice, ad esempio come un argomento di routine, non si conosce la dimensione della matrice o le lunghezze delle dimensioni. È sempre necessario determinare il limite superiore per ogni dimensione della matrice prima di tentare di accedere a tutti gli elementi. Se la matrice è stata creata in modo diverso da un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] `New` clausola, potrebbe essere il limite inferiore diverso da 0 ed è più sicuro determinare tale limite.  
  
### <a name="specifying-the-dimension"></a>Specifica la dimensione  
 Durante la determinazione dei limiti di una matrice multidimensionale, prestare attenzione a come specificare la dimensione. Il `dimension` parametri della <xref:System.Array.GetLowerBound%2A>e <xref:System.Array.GetUpperBound%2A>metodi sono basati su 0, mentre il `Rank` parametri di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Information.LBound%2A>e <xref:Microsoft.VisualBasic.Information.UBound%2A>funzioni sono basati su 1.</xref:Microsoft.VisualBasic.Information.UBound%2A> </xref:Microsoft.VisualBasic.Information.LBound%2A> </xref:System.Array.GetUpperBound%2A> </xref:System.Array.GetLowerBound%2A>  
  
## <a name="see-also"></a>Vedere anche  
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Procedura: inizializzare una variabile di matrice in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)

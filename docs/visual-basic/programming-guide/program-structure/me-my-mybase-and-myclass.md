---
title: "Me, My, MyBase, and MyClass in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "MyClass"
  - "vb.Me"
  - "MyBase"
  - "vb.MyBase"
  - "Me"
  - "vb.MyClass"
  - "vb.This"
  - "vb.My"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My object"
  - "self-reference, Me keyword"
  - "MyClass keyword, relationship to similar programming elements"
  - "Me keyword, relationship to similar programming elements"
  - "Me keyword, referring to the current instance of an object"
  - "Me keyword"
  - "self-reference"
  - "current instance, Me keyword"
  - "MyBase keyword, relationship to similar programming elements"
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Me, My, MyBase, and MyClass in Visual Basic
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`Me`, `My`, `MyBase` e `MyClass` in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] hanno nomi simili, ma scopi diversi.  In questo argomento viene illustrata ciascuna di queste entità per poterle distinguere.  
  
## Me  
 La parola chiave `Me` consente di fare riferimento all'istanza specifica di una classe o struttura in cui il codice è attualmente in esecuzione.  La parola chiave `Me` ha lo stesso comportamento di una variabile oggetto o di una variabile struttura che fa riferimento all'istanza corrente.  La parola chiave `Me` è particolarmente utile per il passaggio di informazioni relative all'istanza di una classe o struttura in esecuzione a una routine in un'altra classe, struttura o modulo.  
  
 Si supponga ad esempio che in un modulo si trovi la seguente routine:  
  
```  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 È possibile chiamare la routine e passare l'istanza corrente della classe <xref:System.Windows.Forms.Form> come argomento utilizzando l'istruzione seguente.  
  
```  
ChangeFormColor(Me)  
```  
  
## My  
 La funzione `My` consente di accedere in modo semplice e intuitivo a numerose classi [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] per permettere agli utenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] di interagire con il computer, l'applicazione, le impostazioni, le risorse e così via.  
  
## MyBase  
 La parola chiave `MyBase` si comporta come una variabile oggetto che fa riferimento alla classe di base dell'istanza corrente di una classe.  `MyBase` viene in genere utilizzata per accedere ai membri della classe di base sottoposti a override o nascosti in una classe derivata.  `MyBase.New` viene utilizzata per chiamare in modo esplicito il costruttore di una classe base da un costruttore di una classe derivata.  
  
## MyClass  
 La parola chiave `MyClass` si comporta come una variabile oggetto che fa riferimento all'istanza corrente di una classe nella sua implementazione originale.  `MyClass` è simile a `Me`, tuttavia tutte le chiamate di metodi effettuate su questa parola chiave vengono considerate come se il metodo fosse `NotOverridable`.  
  
## Vedere anche  
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
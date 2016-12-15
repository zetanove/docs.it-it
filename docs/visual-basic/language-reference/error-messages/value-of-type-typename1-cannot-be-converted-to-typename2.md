---
title: "Value of type &#39;&lt;typename1&gt;&#39; cannot be converted to &#39;&lt;typename2&gt;&#39; | Microsoft Docs"
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
  - "vbc30955"
  - "bc30955"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30955"
ms.assetid: 966b61eb-441e-48b0-bedf-ca95384ecb8b
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Value of type &#39;&lt;typename1&gt;&#39; cannot be converted to &#39;&lt;typename2&gt;&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Impossibile convertire il valore di tipo '\<nometipo1\>' in '\<nometipo2\>'.La mancata corrispondenza del tipo potrebbe essere dovuta alla presenza simultanea di un riferimento al file e di un riferimento di progetto all'assembly '\<nomeassembly\>'.   Provare a sostituire il riferimento di file a '\<percorsofile\>' del progetto '\<nomeprogetto1\>' con un riferimento di progetto a '\<nomeprogetto2\>'.  
  
 In una situazione in cui in un progetto viene creato un riferimento al progetto e un riferimento al file, il compilatore non sarà in grado di garantire che un tipo possa essere convertito in un altro.  
  
 Nello pseudo\-codice descritto di seguito viene illustrata una situazione che può generare questo errore.  
  
 `' ================ Visual Basic project P1 ================`  
  
 `'        P1 makes a PROJECT REFERENCE to project P2`  
  
 `'        and a FILE REFERENCE to project P3.`  
  
 `Public commonObject As P3.commonClass`  
  
 `commonObject = P2.getCommonClass()`  
  
 `' ================ Visual Basic project P2 ================`  
  
 `'        P2 makes a PROJECT REFERENCE to project P3`  
  
 `Public Function getCommonClass() As P3.commonClass`  
  
 `Return New P3.commonClass`  
  
 `End Function`  
  
 `' ================ Visual Basic project P3 ================`  
  
 `Public Class commonClass`  
  
 `End Class`  
  
 Nel progetto `P1` viene creato un riferimento di progetto indiretto dal progetto `P2` al progetto `P3`, oltre a un riferimento di file diretto a `P3`.  La dichiarazione di `commonObject` utilizza il riferimento di file a `P3`, mentre la chiamata a `P2.getCommonClass` utilizza il riferimento di progetto a `P3`.  
  
 Il problema di questa situazione dipende dal fatto che nel riferimento di file vengono specificati un percorso e un nome di file per il file di output di `P3` \(generalmente p3.dll\), mentre nei riferimenti al progetto il progetto di origine \(`P3`\) viene identificato in base al nome del progetto.  Per questo motivo, il compilatore non sarà in grado di garantire che il tipo `P3.commonClass` proviene dallo stesso codice di origine tramite i due diversi riferimenti.  
  
 Questa situazione si verifica generalmente quando sono presenti riferimenti di progetto e riferimenti di file contemporaneamente.  Nell'illustrazione precedente, il problema non si verificherà se `P1` farà un riferimento di progetto diretto a `P3` anziché un riferimento di file.  
  
 **ID errore:** BC30955  
  
### Per correggere l'errore  
  
-   Trasformare un riferimento di file in un riferimento di progetto.  
  
## Vedere anche  
 [Type Conversions in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)   
 [Procedura: aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
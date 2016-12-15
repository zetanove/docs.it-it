---
title: "Value of type &#39;&lt;typename1&gt;&#39; cannot be converted to &#39;&lt;typename2&gt;&#39; (Multiple file references) | Microsoft Docs"
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
  - "vbc30961"
  - "bc30961"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30961"
ms.assetid: 8be5aa0d-d236-4ac3-aa9c-5044f9f6562b
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Value of type &#39;&lt;typename1&gt;&#39; cannot be converted to &#39;&lt;typename2&gt;&#39; (Multiple file references)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Impossibile convertire il valore di tipo '\<nometipo1\>' in '\<nometipo2\>'.La mancata corrispondenza dei tipi può essere causata dall'unione di un riferimento di file a '\<percorsofile1\>' nel progetto '\<nomeprogetto1\>' con un riferimento di file a '\<percorsofile2\>' nel progetto '\<nomeprogetto2\>'.Se gli assembly sono identici, provare a sostituire i riferimenti in modo che entrambi provengano dalla stessa posizione.  
  
 In una situazione in cui in un progetto viene creato più di un riferimento di file a un assembly, il compilatore non sarà in grado di garantire che un tipo possa essere convertito in un altro.  
  
 Ogni riferimento di file specifica un percorso e un nome di file per il file di output di un progetto \(in genere un file DLL\).  Il compilatore non sarà in grado di garantire che i file di output provengono dalla stessa origine o che rappresentino la stessa versione dello stesso assembly.  Pertanto non sarà possibile garantire che i tipi nei differenti riferimenti siano uguali né che un tipo possa essere convertito in un altro.  
  
 È possibile utilizzare un singolo riferimento di file se è noto che gli assembly a cui viene fatto riferimento hanno la stessa identità dell'assembly.  L'*identità dell'assembly* include il nome, la versione, la chiave pubblica, se esiste, e le impostazioni cultura dell'assembly.  Queste informazioni identificano l'assembly in modo univoco.  
  
 **ID errore:** BC30961  
  
### Per correggere l'errore  
  
-   Se gli assembly a cui viene fatto riferimento hanno la stessa identità dell'assembly, rimuovere o sostituire uno dei riferimenti di file in modo che esista un unico riferimento di file.  
  
-   In caso contrario, modificare il codice in modo che non si tenti di convertire un tipo di uno in un tipo dell'altro.  
  
## Vedere anche  
 [Type Conversions in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)   
 [Procedura: aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
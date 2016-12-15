---
title: "Ordinal is not valid | Microsoft Docs"
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
  - "vbrID452"
dev_langs: 
  - "VB"
ms.assetid: 7459562b-cd4f-4590-95e0-6126ae3589a5
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Ordinal is not valid
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La chiamata a una libreria a collegamento dinamico \(DLL\) indica di utilizzare un numero al posto di un nome di routine, tramite la sintassi `#num`.  Le cause possibili dell'errore sono le seguenti:  
  
-   Il tentativo di convertire l'espressione `#num` in un ordinale non è riuscito.  
  
-   L'espressione `#num` non specifica alcuna funzione nella DLL.  
  
-   Una libreria dei tipi ha una dichiarazione non valida, il che comporta l'utilizzo interno di un numero ordinale non valido.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che l'espressione rappresenti un numero valido, oppure chiamare la routine tramite nome.  
  
2.  Assicurarsi che `#num` identifichi una funzione valida nella DLL.  
  
3.  Isolare la chiamata alla routine responsabile del problema, inserendo i commenti al di fuori del codice.  Scrivere un'istruzione `Declare` per la routine e riferire il problema al fornitore della libreria dei tipi.  
  
## Vedere anche  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)
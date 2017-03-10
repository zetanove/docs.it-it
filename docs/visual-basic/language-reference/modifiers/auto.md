---
title: "Auto (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Auto"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Auto keyword, external references"
  - "Declare statement, marshaling strings"
  - "Auto keyword"
  - "Auto keyword, marshaling strings"
ms.assetid: bf79ba95-a62c-48a5-916f-0ac7a52c13ec
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Auto (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che in Visual Basic è necessario effettuare il marshalling delle stringhe secondo le regole di .NET Framework basate sul nome esterno della routine esterna dichiarata.  
  
 Quando si chiama una routine definita al di fuori del progetto, il compilatore Visual Basic non ha accesso alle informazioni necessarie per chiamare correttamente la routine.  Tali informazioni includono la posizione della routine, la procedura per identificarla, la relativa sequenza di chiamata e il tipo restituito, nonché il set di caratteri stringa utilizzato.  L'[Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md) crea un riferimento a una routine esterna e fornisce le informazioni necessarie.  
  
 La parte `charsetmodifier` dell'istruzione `Declare` fornisce le informazioni sul set di caratteri per il marshalling delle stringhe durante una chiamata alla routine esterna.  Influisce inoltre sulle modalità di ricerca del nome della routine esterna nel file esterno.  Il modificatore `Auto` specifica che in Visual Basic è necessario effettuare il marshalling delle stringhe in base alle regole di .NET Framework e determinare il set di caratteri base della piattaforma di run\-time e, se possibile, modificare il nome della routine esterna qualora la ricerca iniziale non riuscisse.  Per ulteriori informazioni, vedere "Set di caratteri" in [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md).  
  
 Se non viene specificato alcun modificatore del set di caratteri, il valore predefinito è `Ansi`.  
  
## Note  
 Il modificatore `Auto` può essere utilizzato in questo contesto:  
  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
## Note per gli sviluppatori di applicazioni per Smart Device  
 Questa parola chiave non è supportata.  
  
## Vedere anche  
 [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md)   
 [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)
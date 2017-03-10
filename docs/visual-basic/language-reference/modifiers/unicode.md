---
title: "Unicode (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Unicode"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Unicode, external references"
  - "Declare statement, marshaling strings"
  - "Unicode keyword"
  - "Unicode, marshaling strings"
ms.assetid: 0021d5ff-3209-444e-8497-420f3e6ee075
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Unicode (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che Visual Basic deve eseguire il marshalling di tutte le stringhe in valori Unicode indipendentemente dal nome della routine esterna dichiarata.  
  
 Quando si chiama una routine definita al di fuori del progetto, il compilatore Visual Basic non può accedere alle informazioni necessarie per chiamare correttamente la routine.  Tali informazioni includono la posizione della routine, la procedura per identificarla, la relativa sequenza di chiamata e il tipo restituito, nonché il set di caratteri stringa utilizzato.  L'[Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md) crea un riferimento a una routine esterna e fornisce le informazioni necessarie.  
  
 La parte `charsetmodifier` dell'istruzione `Declare` fornisce le informazioni sul set di caratteri per il marshalling delle stringhe durante una chiamata alla routine esterna.  Influisce inoltre sulle modalità di ricerca del nome della routine esterna nel file esterno.  Il modificatore `Unicode` specifica che Visual Basic dovrà eseguire il marshalling di tutte le stringhe in valori Unicode ed effettuare la ricerca della routine senza modificarne il nome durante l'operazione.  
  
 Se non viene specificato alcun modificatore del set di caratteri, il valore predefinito è `Ansi`.  
  
## Note  
 È possibile utilizzare il modificatore `Unicode` nel seguente contesto:  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
## Note per gli sviluppatori di applicazioni per Smart Device  
 Questa parola chiave non è supportata.  
  
## Vedere anche  
 [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md)   
 [Auto](../../../visual-basic/language-reference/modifiers/auto.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)
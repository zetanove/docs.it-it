---
title: "Ansi (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Ansi"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Declare statement, marshaling strings"
  - "ANSI, Visual Basic"
  - "ANSI"
ms.assetid: 4f1fa6ff-5557-41ab-b6da-90baf4c15917
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Ansi (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che Visual Basic deve eseguire il marshalling di tutte le stringhe in valori ANSI \(American National Standards Institute\), a prescindere dal nome della routine esterna dichiarato.  
  
 Quando si chiama una routine definita al di fuori del progetto, il compilatore Visual Basic non ha accesso alle informazioni necessarie per chiamare correttamente la routine.  Tali informazioni includono la posizione della routine, la procedura per identificarla, la relativa sequenza di chiamata e il tipo restituito, nonché il set di caratteri stringa utilizzato.  L'[Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md) crea un riferimento a una routine esterna e fornisce le informazioni necessarie.  
  
 La parte `charsetmodifier` dell'istruzione `Declare` fornisce le informazioni sul set di caratteri per il marshalling delle stringhe durante una chiamata alla routine esterna.  Influisce inoltre sulle modalità di ricerca del nome della routine esterna nel file esterno.  Il modificatore `Ansi` specifica che Visual Basic deve eseguire il marshalling di tutte le stringhe in valori ANSI, quindi eseguire ricerche nella routine senza modificarne il nome durante l'operazione.  
  
 Se non viene specificato alcun modificatore del set di caratteri, il valore predefinito è `Ansi`.  
  
## Note  
 È possibile utilizzare il modificatore `Ansi` nel seguente contesto:  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
## Note per gli sviluppatori di applicazioni per Smart Device  
 Questa parola chiave non è supportata.  
  
## Vedere anche  
 [Auto](../../../visual-basic/language-reference/modifiers/auto.md)   
 [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)
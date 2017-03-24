---
title: "Procedura: implementare funzioni di accesso a eventi personalizzati (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "funzioni di accesso [C#], funzioni di accesso agli eventi"
  - "add (funzione di accesso) [C#]"
  - "eventi [C#], add (funzione di accesso)"
  - "eventi [C#], remove (funzione di accesso)"
  - "remove (funzione di accesso) [C#]"
ms.assetid: bf903abf-03a4-4f7b-ab6b-b7e59bc2ee1e
caps.latest.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 7
---
# Procedura: implementare funzioni di accesso a eventi personalizzati (Guida per programmatori C#)
Un evento è un tipo speciale di delegato multicast che può essere richiamato solo dall'interno della classe in cui è dichiarato.  Il codice client sottoscrive l'evento fornendo un riferimento a un metodo che deve essere richiamato quando l'evento viene generato.  Questi metodi vengono aggiunti all'elenco di chiamate del delegato tramite funzioni di accesso agli eventi, che sono simili alle funzioni di accesso alle proprietà, ad eccezione del fatto che sono denominate `add` e `remove`.  Nella maggior parte dei casi, non è necessario fornire funzioni di accesso a eventi personalizzate.  Se nel codice non sono disponibili funzioni di accesso a eventi personalizzate, il compilatore le aggiunge automaticamente.  Tuttavia, in alcuni casi può essere necessario fornire un comportamento personalizzato,  come illustrato nell'argomento [Procedura: implementare eventi di interfaccia](../../../csharp/programming-guide/events/how-to-implement-interface-events.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come implementare funzioni di accesso a eventi add e remove personalizzate.  Anche se è possibile sostituire qualsiasi parte di codice nelle funzioni di accesso, si consiglia di bloccare l'evento prima di aggiungere o rimuovere un nuovo metodo per la gestione eventi.  
  
```  
event EventHandler IDrawingObject.OnDraw  
        {  
            add  
            {  
                lock (PreDrawEvent)  
                {  
                    PreDrawEvent += value;  
                }  
            }  
            remove  
            {  
                lock (PreDrawEvent)  
                {  
                    PreDrawEvent -= value;  
                }  
            }  
        }  
  
```  
  
## Vedere anche  
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [event](../../../csharp/language-reference/keywords/event.md)
---
title: "Procedura: implementare gli eventi di interfaccia (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "eventi [C#], in interfacce"
  - "interfacce [C#], implementazione di eventi in classi"
ms.assetid: 63527447-9535-4880-8e95-35e2075827df
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# Procedura: implementare gli eventi di interfaccia (Guida per programmatori C#)
Un'[interfaccia](../../../csharp/language-reference/keywords/interface.md) può dichiarare un [evento](../../../csharp/language-reference/keywords/event.md).  Nell'esempio seguente viene illustrato come implementare eventi di interfaccia in una classe.  Le regole sono le stesse utilizzate per l'implementazione di qualsiasi metodo o proprietà di interfaccia.  
  
### Per implementare eventi di interfaccia in una classe  
  
-   Dichiarare l'evento nella classe e quindi richiamarlo nelle aree appropriate.  
  
    ```  
    namespace ImplementInterfaceEvents  
    {  
        public interface IDrawingObject  
        {  
            event EventHandler ShapeChanged;  
        }  
        public class MyEventArgs : EventArgs   
        {  
            // class members  
        }  
        public class Shape : IDrawingObject  
        {  
            public event EventHandler ShapeChanged;  
            void ChangeShape()  
            {  
                // Do something here before the event…  
  
                OnShapeChanged(new MyEventArgs(/*arguments*/));  
  
                // or do something here after the event.   
            }  
            protected virtual void OnShapeChanged(MyEventArgs e)  
            {  
                if(ShapeChanged != null)  
                {  
                   ShapeChanged(this, e);  
                }  
            }  
        }  
  
    }  
    ```  
  
## Esempio  
 Nell'esempio seguente viene illustrato come gestire la situazione meno comune in cui la classe eredita da due o più interfacce e a ogni interfaccia è associato un evento con lo stesso nome.  In questo caso, è necessario fornire un'implementazione di interfaccia esplicita per almeno uno degli eventi.  Quando si scrive un'implementazione di interfaccia esplicita per un evento, è anche necessario scrivere le funzioni di accesso agli eventi `add` e `remove`.  In genere queste funzioni sono fornite dal compilatore, ma in questo caso il compilatore non è in grado di farlo.  
  
 Fornendo funzioni di accesso personalizzate, è possibile specificare se i due eventi sono rappresentati dallo stesso evento nella classe, o da eventi diversi.  Ad esempio, se gli eventi devono essere generati in momenti diversi secondo le specifiche dell'interfaccia, è possibile associare ogni evento a un'implementazione separata nella classe.  Nell'esempio seguente i sottoscrittori determinano l'evento `OnDraw` che riceveranno eseguendo il cast del riferimento della forma su `IShape` o `IDrawingObject`.  
  
 [!code-cs[csProgGuideEvents#10](../../../csharp/programming-guide/events/codesnippet/csharp/how-to-implement-interfa_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Implementazione esplicita dell'interfaccia](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)   
 [Procedura: generare eventi di classe base nelle classi derivate](../../../csharp/programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md)
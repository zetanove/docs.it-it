---
title: "Procedura: pubblicare eventi conformi alle linee guida di .NET Framework (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "eventi [C#], linee guida dell'implementazione"
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# Procedura: pubblicare eventi conformi alle linee guida di .NET Framework (Guida per programmatori C#)
Nella procedura seguente viene illustrato come aggiungere eventi conformi al modello standard di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] per classi e struct.  Tutti gli eventi nella libreria di classi di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] sono basati sul delegato <xref:System.EventHandler> che è definito nel modo seguente:  
  
```  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
>  [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)] introduce una versione generica di questo delegato, <xref:System.EventHandler%601>.  Negli esempi seguenti viene illustrato come utilizzare entrambe le versioni.  
  
 Nonostante gli eventi definiti in classi possano essere basati su qualsiasi tipo delegato valido, inclusi i delegati che restituiscono un valore, è in genere consigliabile basare gli eventi sul modello di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] utilizzando l'oggetto <xref:System.EventHandler>, come illustrato nell'esempio seguente:  
  
### Per pubblicare eventi basati sul modello EventHandler  
  
1.  Ignorare questo passaggio e andare direttamente al passaggio 3a se non è necessario inviare dati personalizzati con l'evento. Dichiarare la classe per i dati personalizzati in un ambito visibile sia alle classi publisher che subscriber.  Aggiungere quindi i membri necessari per inserire i dati degli eventi personalizzati.  In questo esempio viene restituita una semplice stringa.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
2.  \(Ignorare questo passaggio se si utilizza la versione generica di <xref:System.EventHandler%601>.\) Dichiarare un delegato nella classe di pubblicazione.  Assegnargli un nome che termini con *EventHandler*.  Il secondo parametro specifica il tipo EventArgs personalizzato.  
  
    ```  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3.  Dichiarare l'evento nella classe di pubblicazione eseguendo una delle operazioni seguenti.  
  
    1.  Se non si dispone di una classe EventArgs personalizzata, il tipo di evento sarà il delegato EventHandler non generico.  Non è necessario dichiarare il delegato perché è già dichiarato nello spazio dei nomi <xref:System> incluso quando si crea il progetto C\#.  Aggiungere il codice seguente alla classe publisher.  
  
        ```  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2.  Se si utilizza la versione non generica di <xref:System.EventHandler> e si dispone di una classe personalizzata derivata da <xref:System.EventArgs>, dichiarare l'evento all'interno della classe di pubblicazione e utilizzare il delegato del passaggio 2 come tipo:  
  
        ```  
        public event CustomEventHandler RaiseCustomEvent;  
  
        ```  
  
    3.  Se si utilizza la versione generica, non è necessario un delegato personalizzato.  Nella classe di pubblicazione specificare invece il tipo di evento come `EventHandler<CustomEventArgs>`, sostituendo il nome della classe personalizzata racchiuso tra parentesi acute.  
  
        ```  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## Esempio  
 Nell'esempio seguente vengono illustrati i passaggi indicati sopra utilizzando una classe EventArgs personalizzata e <xref:System.EventHandler%601> come tipo di evento.  
  
 [!code-cs[csProgGuideEvents#2](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-publish-events-that-conform-to-net-framework-guidelines_1.cs)]  
  
## Vedere anche  
 <xref:System.Delegate>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)
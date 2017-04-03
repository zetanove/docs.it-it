---
title: 'Procedura: Pubblicare eventi conformi alle linee guida di .NET Framework (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- events [C#], implementation guidelines
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
caps.latest.revision: 31
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 78d069249c8131a091a206703c475faaf641d17b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-publish-events-that-conform-to-net-framework-guidelines-c-programming-guide"></a>Procedura: pubblicare eventi conformi alle linee guida di .NET Framework (Guida per programmatori C#)
La procedura seguente illustra come aggiungere a classi e struct gli eventi che seguono il modello standard [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Tutti gli eventi della libreria di classi [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] si basano sul delegato <xref:System.EventHandler>, che viene definito come segue:  
  
```  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
>  [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] introduce una versione generica di questo delegato, <xref:System.EventHandler%601>. Negli esempi seguenti viene illustrato l'uso di entrambe le versioni.  
  
 Anche se gli eventi nelle classi che vengono definite possono essere basati su qualsiasi tipo di delegato valido, inclusi i delegati che restituiscono un valore, è consigliabile basare gli eventi sul modello [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] usando <xref:System.EventHandler>, come illustrato nell'esempio seguente.  
  
### <a name="to-publish-events-based-on-the-eventhandler-pattern"></a>Per pubblicare eventi basati sul modello EventHandler  
  
1.  Ignorare questo passaggio e andare al passaggio 3a se non è necessario inviare i dati personalizzati con l'evento. Dichiarare la classe per i dati personalizzati in un ambito che sia visibile sia per la classe dell'editore che per quella del sottoscrittore. Aggiungere i membri necessari per contenere i dati di evento personalizzati. In questo esempio viene restituita una semplice stringa.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
2.  Ignorare questo passaggio se si usa la versione generica di <xref:System.EventHandler%601>. Dichiarare un delegato nella classe di pubblicazione. Assegnargli un nome che termini con *EventHandler*. Il secondo parametro specifica il tipo EventArgs personalizzato.  
  
    ```  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3.  Dichiarare l'evento nella classe di pubblicazione usando uno dei passaggi seguenti.  
  
    1.  Se non si ha una classe EventArgs personalizzata, il tipo di evento sarà il delegato EventHandler non generico. Non è necessario dichiarare il delegato poiché è già stato dichiarato nello spazio dei nomi <xref:System> che viene incluso quando si crea il progetto in C#. Aggiungere il codice seguente alla classe dell'editore.  
  
        ```  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2.  Se si usa la versione non generica di <xref:System.EventHandler> e si ha una classe personalizzata derivata da <xref:System.EventArgs>, dichiarare l'evento all'interno della classe di pubblicazione e usare il delegato del passaggio 2 come tipo.  
  
        ```  
        public event CustomEventHandler RaiseCustomEvent;  
  
        ```  
  
    3.  Se si usa la versione generica, non è necessario un delegato personalizzato. Al contrario, nella classe di pubblicazione specificare il tipo di evento come `EventHandler<CustomEventArgs>`, sostituendo il nome della classe racchiuso tra parentesi acute.  
  
        ```  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra i passaggi precedenti usando una classe EventArgs personalizzata e <xref:System.EventHandler%601> come tipo di evento.  
  
 [!code-cs[csProgGuideEvents#2](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-publish-events-that-conform-to-net-framework-guidelines_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Delegate>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)

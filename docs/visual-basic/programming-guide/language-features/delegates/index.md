---
title: Delegati (Visual Basic) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- delegates [Visual Basic]
- Visual Basic code, delegates
ms.assetid: 410b60dc-5e60-4ec0-bfae-426755a2ee28
caps.latest.revision: 10
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 0fad74980e3c8cf66b9909b50bdaa3f9f4f567a1
ms.lasthandoff: 03/13/2017

---
# <a name="delegates-visual-basic"></a>Delegati (Visual Basic)
I delegati sono oggetti che fanno riferimento ai metodi. Vengono a volte descritti come *puntatori a funzione indipendenti dai tipi* poiché sono simili ai puntatori a funzione usati in altri linguaggi di programmazione. A differenza dei puntatori a funzione, tuttavia, i delegati [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sono un tipo riferimento basato sulla classe <xref:System.Delegate?displayProperty=fullName>. I delegati possono fare riferimento sia a metodi condivisi, ovvero metodi che è possibile chiamare senza una specifica istanza di una classe, sia a metodi di istanza.  
  
## <a name="delegates-and-events"></a>Delegati ed eventi  
 I delegati sono utili nelle situazioni in cui è necessario un intermediario tra una routine chiamante e la routine chiamata. Ad esempio, può essere necessario che un oggetto generatore di eventi sia in grado di chiamare gestori di eventi differenti in circostanze diverse. Purtroppo, l'oggetto che genera gli eventi non può sapere in anticipo quale gestore eventi gestirà uno specifico evento. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente di associare in modo dinamico i gestori eventi agli eventi mediante la creazione automatica di un delegato quando viene usata l'istruzione `AddHandler`. In fase di esecuzione, il delegato inoltrerà le chiamate al gestore eventi appropriato.  
  
 Sebbene sia possibile creare manualmente i delegati, nella maggior parte dei casi [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea automaticamente il delegato con tutti i dettagli necessari. Un'istruzione `Event`, ad esempio, consente di definire implicitamente una classe delegata denominata `<EventName>EventHandler` come classe nidificata della classe contenente l'istruzione `Event` e con la stessa firma dell'evento. L'istruzione `AddressOf` crea in modo implicito un'istanza di un delegato che fa riferimento a una routine specifica. Le due righe di codice seguenti sono equivalenti. Nella prima riga è possibile osservare la creazione esplicita di un'istanza di `Eventhandler`, con un riferimento al metodo `Button1_Click` inviato come argomento. La seconda riga rappresenta un modo più pratico di eseguire la stessa operazione.  
  
 [!code-vb[VbVbalrDelegates#6](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_1.vb)]  
  
 È possibile usare la sintassi abbreviata per creare delegati ogni volta che il compilatore è in grado di determinare il tipo del delegato in base al contesto.  
  
## <a name="declaring-events-that-use-an-existing-delegate-type"></a>Dichiarazione di eventi che usano un tipo delegato esistente  
 In alcune situazioni, è consigliabile dichiarare un evento che usa un tipo delegato esistente come delegato sottostante. La sintassi seguente illustra come eseguire tale operazione:  
  
 [!code-vb[VbVbalrDelegates#7](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_2.vb)]  
  
 Questa operazione si rivela utile quando si vogliono inviare più eventi allo stesso gestore.  
  
## <a name="delegate-variables-and-parameters"></a>Variabili e parametri dei delegati  
 È possibile usare i delegati per altre attività non relative a eventi, ad esempio il modello di threading Free, oppure con routine che richiedono la chiamata di diverse versioni delle funzioni in fase di compilazione.  
  
 Si supponga, ad esempio, di avere un'applicazione di annunci pubblicitari che include una casella di riepilogo contenente nomi di automobili. Gli annunci sono ordinati per titolo, in genere corrispondente al modello dell'auto. Se per alcune auto il modello è preceduto dall'anno di produzione, può verificarsi un problema. Il problema consiste nel fatto che la funzionalità di ordinamento integrata della casella di riepilogo esegue l'ordinamento solo in base ai codici dei caratteri, elencando prima tutti gli annunci che iniziano con una data e quindi tutti quelli che iniziano con il modello.  
  
 Per risolvere il problema, è possibile creare una routine di ordinamento in una classe che usa l'ordinamento alfabetico standard per la maggior parte delle caselle di riepilogo, ma che è in grado di passare, in fase di esecuzione, alla routine di ordinamento personalizzata per gli annunci relativi alle automobili. A questo scopo, è necessario passare la routine di ordinamento personalizzata alla classe di ordinamento in fase di esecuzione usando i delegati.  
  
## <a name="addressof-and-lambda-expressions"></a>Espressioni AddressOf e Lambda  
 Ogni classe delegata definisce un costruttore a cui viene passata la specifica di un metodo dell'oggetto. Un argomento di un costruttore di delegati deve essere un riferimento a un metodo o a un'espressione lambda.  
  
 Per specificare un riferimento a un metodo, usare la sintassi seguente:  
  
 `AddressOf` [`expression`.]`methodName`  
  
 Il tipo in fase di compilazione dell'elemento `expression` deve essere il nome di una classe o un'interfaccia contenente un metodo con il nome specificato la cui firma corrisponde a quella della classe delegata. Il metodo `methodName` può essere o un metodo condiviso o un metodo di istanza. `methodName` non è un elemento facoltativo, anche se si crea un delegato per il metodo predefinito della classe.  
  
 Per specificare un'espressione lambda, usare la sintassi seguente:  
  
 `Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`  
  
 Nell'esempio seguente sono illustrate sia l'espressione `AddressOf` che l'espressione lambda usate per specificare il riferimento per un delegato.  
  
 [!code-vb[VbVbalrDelegates#15](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_3.vb)]  
  
 La firma della funzione deve corrispondere a quella del tipo delegato. Per altre informazioni sulle espressioni lambda, vedere [Espressioni lambda in C++](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md). Per altri esempi di espressioni lambda e assegnazioni di `AddressOf` a delegati, vedere [Conversione di tipo relaxed del delegato](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Procedura: Richiamare un metodo delegato](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)|Viene offerto un esempio che mostra come associare un metodo a un delegato e quindi richiamare tale metodo tramite il delegato.|  
|[Procedura: Passare una routine a un'altra routine in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)|Viene illustrato come usare i delegati per passare una routine a un'altra routine.|  
|[Conversione di tipo relaxed del delegato](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)|Viene descritto come assegnare subroutine e funzioni a delegati o gestori anche quando le relative firme non sono identiche.|  
|[Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)|Viene offerta una panoramica degli eventi in Visual Basic.|

---
title: Istruzione RaiseEvent | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.RaiseEventMethod
- vb.RaiseEvent
- RaiseEvent
dev_langs:
- VB
helpviewer_keywords:
- raising events, RaiseEvent statement
- RaiseEvent statement
- event handlers, connecting events to
ms.assetid: f82e380a-1e6b-4047-bea8-c853f4d2c742
caps.latest.revision: 19
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 059b1347c4a35b896f5aa19cadb28fbceb8b25c9
ms.lasthandoff: 03/13/2017

---
# <a name="raiseevent-statement"></a>Istruzione RaiseEvent
Trigger di un evento dichiarato a livello di modulo in una classe, un modulo o un documento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
RaiseEvent eventname[( argumentlist )]  
```  
  
## <a name="parts"></a>Parti  
 `eventname`  
 Obbligatorio. Nome dell'evento da attivare.  
  
 `argumentlist`  
 Facoltativo. Elenco delimitato da virgole di variabili, matrici o espressioni. Il `argumentlist` argomento deve essere racchiuso tra parentesi. Se non sono presenti argomenti, è necessario omettere le parentesi.  
  
## <a name="remarks"></a>Note  
 Obbligatoria `eventname` è il nome di un evento dichiarato all'interno del modulo. Ne consegue convenzioni di denominazione di variabili di Visual Basic.  
  
 Se l'evento non è stata dichiarata all'interno del modulo in cui viene generato, si verifica un errore. Nel frammento di codice seguente viene illustrata una dichiarazione di evento e una procedura in cui viene generato l'evento.  
  
 [!code-vb[VbVbalrEvents&#37;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_1.vb)]  
  
 Non è possibile utilizzare `RaiseEvent` per generare eventi non vengono dichiarati in modo esplicito nel modulo. Ad esempio, tutti i form ereditano un <xref:System.Windows.Forms.Control.Click>evento <xref:System.Windows.Forms.Form?displayProperty=fullName>, non può essere generato utilizzando `RaiseEvent` in un form derivato.</xref:System.Windows.Forms.Form?displayProperty=fullName> </xref:System.Windows.Forms.Control.Click> Se si dichiara un `Click` evento nel modulo del form, esso nasconde il modulo <xref:System.Windows.Forms.Control.Click>eventi.</xref:System.Windows.Forms.Control.Click> È comunque possibile richiamare il modulo <xref:System.Windows.Forms.Control.Click>evento chiamando il <xref:System.Windows.Forms.Control.OnClick%2A>(metodo).</xref:System.Windows.Forms.Control.OnClick%2A> </xref:System.Windows.Forms.Control.Click>  
  
 Per impostazione predefinita, un evento definito in Visual Basic genera gestori eventi nell'ordine che vengono stabilite le connessioni. Poiché gli eventi possono essere `ByRef` parametri, un processo collegato in seguito possono essere passati parametri che sono stati modificati da un gestore eventi precedenti. Dopo che i gestori di eventi è stato eseguito, il controllo viene restituito alla subroutine che ha generato l'evento.  
  
> [!NOTE]
>  Gli eventi non condivisi non devono essere generati all'interno del costruttore della classe in cui sono dichiarati. Anche se tali eventi non causano errori di run-time, potrebbero non riuscire a essere rilevate dai gestori eventi associati. Utilizzare il `Shared` modificatore per creare un evento condiviso se è necessario generare un evento da un costruttore.  
  
> [!NOTE]
>  È possibile modificare il comportamento predefinito di eventi mediante la definizione di un evento personalizzato. Per gli eventi personalizzati, il `RaiseEvent` istruzione richiama l'evento `RaiseEvent` della funzione di accesso. Per ulteriori informazioni sugli eventi personalizzati, vedere [istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## <a name="example"></a>Esempio  
 Negli esempi seguenti, gli eventi vengono usati per il conto alla rovescia dei secondi, da 10 a 0. Il codice illustra alcune delle relative agli eventi di metodi, proprietà e le istruzioni, inclusa la `RaiseEvent` istruzione.  
  
 La classe che genera un evento viene definita origine e i metodi che lo elaborano vengono definiti gestori eventi. Un'origine eventi può disporre di più gestori per gli eventi generati. Quando la classe genera l'evento, lo stesso evento viene generato in tutte le classi per cui è stato scelto di gestire eventi per tale istanza dell'oggetto.  
  
 Nell'esempio vengono usati anche un form (`Form1`) con un pulsante (`Button1`) e una casella di testo (`TextBox1`). Quando si fa clic sul pulsante, nella prima casella di testo viene visualizzato il conto alla rovescia dei secondi da 10 a 0. Al termine dei&10; secondi, nella prima casella di testo viene visualizzato "Done".  
  
 Il codice di `Form1` specifica gli stati di inizio e fine del form. Contiene inoltre il codice eseguito quando vengono generati gli eventi.  
  
 Per utilizzare questo esempio, aprire un nuovo progetto applicazione Windows, aggiungere un pulsante denominato `Button1` e una casella di testo denominato `TextBox1` per il form principale, denominato `Form1`. Quindi fare doppio clic su form e fare clic su **Visualizza codice** per aprire l'Editor di codice.  
  
 Aggiungere un `WithEvents` sezione delle dichiarazioni di variabile di `Form1` (classe).  
  
 [!code-vb[VbVbalrEvents&#14;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_2.vb)]  
  
## <a name="example"></a>Esempio  
 Aggiungere il codice seguente al codice per `Form1`: Sostituire eventuali procedure duplicate esistenti, ad esempio `Form_Load`, o `Button_Click`.  
  
 [!code-vb[VbVbalrEvents&#15;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_3.vb)]  
  
 Premere F5 per eseguire l'esempio precedente, quindi fare clic sul pulsante con etichettato **avviare**. Nella prima casella di testo viene avviato il conto alla rovescia dei secondi. Al termine dei&10; secondi, nella prima casella di testo viene visualizzato "Done".  
  
> [!NOTE]
>  Il `My.Application.DoEvents` metodo elabora gli eventi esattamente allo stesso modo del form. Per consentire al modulo gestire gli eventi direttamente, è possibile utilizzare il multithreading. Per ulteriori informazioni, vedere [Threading](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c).  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)   
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)   
 [AddHandler (istruzione)](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler (istruzione)](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handle](../../../visual-basic/language-reference/statements/handles-clause.md)

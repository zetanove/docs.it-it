---
title: Informazioni sul chiamante (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 15d556eb-4d0c-4497-98a3-7f60abb7d6a1
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9a4b63fb424ad6aef9d1bd56f43ccccd79f0b9b3
ms.lasthandoff: 03/13/2017

---
# <a name="caller-information-visual-basic"></a>Informazioni sul chiamante (Visual Basic)
Gli attributi di informazioni sul chiamante consentono di ottenere informazioni sul chiamante di un metodo. È possibile ottenere il percorso del file del codice sorgente, il numero di riga nel codice sorgente e il nome del chiamante. Queste informazioni sono utili per la tracciatura, il debug e la creazione di strumenti diagnostici.  
  
 Per ottenere queste informazioni, utilizzare gli attributi applicati ai parametri facoltativi, a ognuno dei quali è associato un valore predefinito. Nella tabella seguente vengono elencati gli attributi di informazioni sul chiamante definiti nel <xref:System.Runtime.CompilerServices?displayProperty=fullName>dello spazio dei nomi:</xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
|Attributo|Descrizione|Tipo|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute></xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|Percorso completo del file di origine contenente il chiamante. Si tratta del percorso del file al momento della compilazione.|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute></xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|Numero di riga nel file di origine in cui viene chiamato il metodo.|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute></xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|Nome di una proprietà o di un metodo del chiamante. Vedere [i nomi dei membri](#MEMBERNAMES) più avanti in questo argomento.|`String`|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare gli attributi di informazioni sul chiamante. Per ogni chiamata al metodo `TraceMessage`, le informazioni sul chiamante vengono sostituite come argomenti dei parametri facoltativi.  
  
```vb  
Private Sub DoProcessing()  
    TraceMessage("Something happened.")  
End Sub  
  
Public Sub TraceMessage(message As String,  
        <System.Runtime.CompilerServices.CallerMemberName> Optional memberName As String = Nothing,  
        <System.Runtime.CompilerServices.CallerFilePath> Optional sourcefilePath As String = Nothing,  
        <System.Runtime.CompilerServices.CallerLineNumber()> Optional sourceLineNumber As Integer = 0)  
  
    System.Diagnostics.Trace.WriteLine("message: " & message)  
    System.Diagnostics.Trace.WriteLine("member name: " & memberName)  
    System.Diagnostics.Trace.WriteLine("source file path: " & sourcefilePath)  
    System.Diagnostics.Trace.WriteLine("source line number: " & sourceLineNumber)  
End Sub  
  
' Sample output:  
'   message: Something happened.  
'   member name: DoProcessing  
'   source file path: C:\Users\username\Documents\Visual Studio 2012\Projects\CallerInfoVB\CallerInfoVB\Form1.vb  
'   source line number: 15  
```  
  
## <a name="remarks"></a>Note  
 È sempre necessario specificare un valore esplicito per ciascun parametro facoltativo. Non è possibile applicare attributi di informazioni sul chiamante ai parametri non specificati come facoltativi.  
  
 Gli attributi di informazioni sul chiamante non restituiscono un parametro facoltativo, ma influiscono sul valore predefinito passato quando l'argomento è omesso.  
  
 I valori delle informazioni sul chiamante vengono generati come valori letterali in Intermediate Language (IL) in fase di compilazione. A differenza dei risultati della <xref:System.Exception.StackTrace%2A>proprietà per le eccezioni, i risultati non sono interessati da offuscamento.</xref:System.Exception.StackTrace%2A>  
  
 È possibile fornire esplicitamente gli argomenti facoltativi per esaminare o nascondere le informazioni sul chiamante.  
  
###  <a name="MEMBERNAMES"></a>Nomi dei membri  
 È possibile utilizzare l'attributo `CallerMemberName` per specificare il nome del membro come argomento `String` al metodo chiamato. Utilizzando questa tecnica, si evita il problema che **Refactoring di ridenominazione** non modifica il `String` valori. Questo vantaggio è particolarmente utile per le attività seguenti:  
  
-   Utilizzo della tracciatura e delle routine di diagnostica.  
  
-   Implementazione di <xref:System.ComponentModel.INotifyPropertyChanged>durante l'associazione di dati.</xref:System.ComponentModel.INotifyPropertyChanged> Questa interfaccia consente alla proprietà di un oggetto di notificare a un controllo associato la modifica della proprietà stessa in modo che il controllo possa visualizzare le informazioni aggiornate. Senza l'attributo `CallerMemberName`, è necessario specificare il nome della proprietà come valore letterale.  
  
 Nel grafico seguente vengono mostrati i nomi dei membri restituiti quando si utilizza l'attributo `CallerMemberName`.  
  
|Elemento in cui si verificano le chiamate|Nome del membro restituito|  
|-------------------------|------------------------|  
|Metodo, proprietà o evento|Nome del metodo, della proprietà o dell'evento da cui la chiamata ha avuto origine.|  
|Costruttore|Stringa ".ctor"|  
|Costruttore statico|Stringa ".cctor"|  
|Distruttore|Stringa "Finalize"|  
|Operatori o conversioni definiti dall'utente|Nome generato per il membro, ad esempio "op_Addition".|  
|Costruttore dell'attributo|Nome del membro a cui viene applicato l'attributo. Se l'attributo è un qualsiasi elemento in un membro (ad esempio un parametro, un valore restituito o un parametro di tipo generico), il risultato è il nome del membro associato a tale elemento.|  
|Nessun membro contenitore (ad esempio a livello di assembly o attributi applicati a tipi)|Valore predefinito del parametro facoltativo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi (Visual Basic)](../../../visual-basic/language-reference/attributes.md)   
 [Attributi comuni (Visual Basic)](../../../visual-basic/programming-guide/concepts/attributes/common-attributes.md)   
 [Parametri facoltativi](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Concetti di programmazione (Visual Basic)](../../../visual-basic/programming-guide/concepts/index.md)

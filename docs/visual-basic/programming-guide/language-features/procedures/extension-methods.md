---
title: "Metodi di estensione (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.ExtensionMethods"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "estensione di tipi di dati"
  - "metodi di estensione [Visual Basic]"
ms.assetid: b8020aae-374d-46a9-bcb7-8cc2390b93b6
caps.latest.revision: 41
caps.handback.revision: 41
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Metodi di estensione (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

I metodi di estensione consentono agli sviluppatori di aggiungere funzionalità personalizzate a tipi di dati già definiti senza creare un nuovo tipo derivato.  I metodi di estensione rendono possibile la scrittura di un metodo che può essere chiamato come se fosse un metodo di istanza del tipo esistente.  
  
## Note  
 Un metodo di estensione può essere solo una routine `Sub` o una routine `Function`.  Non è possibile definire una proprietà, un campo o un evento di estensione.  Tutti i metodi di estensione devono essere contrassegnati con l'attributo di estensione `<Extension()>` dello spazio dei nomi <xref:System.Runtime.CompilerServices?displayProperty=fullName>.  
  
 Il primo parametro della definizione di un metodo di estensione specifica il tipo di dati che il metodo estende.  Quando il metodo viene eseguito, il primo parametro viene associato all'istanza del tipo di dati che richiama il metodo.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio riportato di seguito viene definita un'estensione `Print` per il tipo di dati <xref:System.String>.  Il metodo utilizza `Console.WriteLine` per visualizzare una stringa.  Il parametro del metodo `Print`, `aString`, stabilisce che il metodo estende la classe <xref:System.String>.  
  
 [!code-vb[VbVbalrExtensionMethods#1](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_1.vb)]  
  
 Notare che la definizione del metodo di estensione è contrassegnata con l'attributo di estensione `<Extension()>`.  Il contrassegno del modulo nel quale è definito il metodo è facoltativo, tuttavia ogni metodo di estensione deve essere contrassegnato.  <xref:System.Runtime.CompilerServices> deve essere importato per accedere all'attributo di estensione.  
  
 I metodi di estensione possono essere dichiarati solo nei moduli.  In genere, il modulo nel quale è definito un metodo di estensione non è lo stesso nel quale viene chiamato.  Il modulo che contiene il metodo di estensione viene invece importato, se necessario, per portarlo nell'ambito.  Una volta che il modulo contenente `Print` si trova nell'ambito, il metodo può essere chiamato come se fosse un metodo di istanza comune che non assume argomenti, ad esempio `ToUpper`:  
  
 [!code-vb[VbVbalrExtensionMethods#2](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_2.vb)]  
  
 Anche il prossimo esempio, `PrintAndPunctuate`, è un'estensione di <xref:System.String>, in questo caso definito con due parametri.  Il primo parametro, `aString`, stabilisce che il metodo di estensione estende <xref:System.String>.  Il secondo parametro, `punc`, deve essere una stringa di segni di punteggiatura passata come argomento quando il metodo viene chiamato.  Il metodo visualizza la stringa seguita dai segni di punteggiatura.  
  
 [!code-vb[VbVbalrExtensionMethods#3](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_3.vb)]  
  
 Il metodo viene chiamato inviando un argomento stringa per `punc`: `example.PrintAndPunctuate(".")`  
  
 Nell'esempio che segue vengono illustrate la definizione e la chiamata di `Print` e `PrintAndPunctuate`.  <xref:System.Runtime.CompilerServices> viene importato nel modulo della definizione per consentire l'accesso all'attributo di estensione.  
  
### Codice  
  
```vb#  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
  
    <Extension()>   
    Public Sub Print(ByVal aString As String)  
        Console.WriteLine(aString)  
    End Sub  
  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
```  
  
 Successivamente i metodi di estensione vengono inseriti nell'ambito e chiamati.  
  
```vb#  
Imports ConsoleApplication2.StringExtensions  
Module Module1  
  
    Sub Main()  
  
        Dim example As String = "Example string"  
        example.Print()  
  
        example = "Hello"  
        example.PrintAndPunctuate(".")  
        example.PrintAndPunctuate("!!!!")  
  
    End Sub  
End Module  
```  
  
### Commenti  
 Tutto ciò che è occorre per eseguire questi metodi di estensione o metodi simili è che si trovino nell'ambito.  Se il modulo che contiene un metodo di estensione è nell'ambito, è visibile in IntelliSense e può essere chiamato come se fosse un metodo di istanza comune.  
  
 Notare che quando i metodi vengono richiamati, non viene inviato alcun argomento per il primo parametro.  Il parametro `aString` delle precedenti definizioni di metodo è associato a `example`, l'istanza di `String` che le chiama.  Il compilatore utilizzerà `example` come argomento inviato al primo parametro.  
  
 Il metodo di estensione viene eseguito se viene chiamato per un oggetto impostato su `Nothing`.  Questa operazione non è applicabile ai metodi di istanza ordinari.  È possibile verificare in modo esplicito la presenza di `Nothing` nel metodo di estensione.  
  
## Tipi che è possibile estendere  
 È possibile definire un metodo di estensione nella maggior parte dei tipi che possono essere rappresentati in un elenco di parametri di Visual Basic, inclusi gli elementi seguenti:  
  
-   Classi \(tipi di riferimento\)  
  
-   Strutture \(tipi di valore\)  
  
-   Interfacce  
  
-   Delegati  
  
-   Argomenti ByRef e ByVal  
  
-   Parametri di metodo generici  
  
-   Matrici  
  
 Poiché il primo parametro specifica il tipo di dati esteso dal metodo di estensione, è obbligatorio e non facoltativo.  Per tale ragione, i parametri `Optional` e i parametri `ParamArray` non possono essere il primo parametro dell'elenco di parametri.  
  
 I metodi di estensione vengono ignorati in associazione tardiva.  Nell'esempio seguente l'istruzione `anObject.PrintMe()` genera un'eccezione <xref:System.MissingMemberException>; la stessa eccezione sarebbe visualizzata se fosse eliminata la seconda definizione del metodo di estensione `PrintMe` .  
  
 [!code-vb[VbVbalrExtensionMethods#9](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_4.vb)]  
  
## Suggerimenti  
 I metodi di estensione forniscono una modalità comoda ed efficace di estendere un tipo esistente.  Tuttavia, per utilizzarli correttamente, occorre considerare alcuni punti,  che riguardano principalmente gli autori delle librerie di classi ma che potrebbero influire su qualsiasi applicazione che utilizza i metodi di estensione.  
  
 In generale, i metodi di estensione aggiunti ai tipi che non si possiede sono più vulnerabili dei metodi di estensione aggiunti ai tipi che si controlla.  Nelle classi che non si possiede possono verificarsi svariati eventi che possono interferire con i metodi di estensione.  
  
-   Se esiste un membro di istanza accessibile che ha una firma compatibile con gli argomenti dell'istruzione chiamante, senza necessità di conversioni verso un tipo di dati più piccolo da argomento a parametro, il metodo di istanza verrà utilizzato di preferenza rispetto a qualsiasi metodo di estensione.  Se pertanto in un dato punto viene aggiunto a una classe un metodo di istanza appropriato, un membro di estensione esistente sul quale ci si basa potrebbe divenire inaccessibile.  
  
-   L'autore di un metodo di estensione non può impedire agli altri programmatori di scrivere metodi di estensione in conflitto che possono avere la precedenza sull'estensione originale.  
  
-   È possibile migliorare la robustezza inserendo i metodi di estensione nel rispettivo spazio dei nomi.  Gli utenti della libreria possono quindi includere o escludere uno spazio dei nomi, oppure scegliere tra gli spazi dei nomi, separatamente dal resto della libreria.  
  
-   Potrebbe essere più sicuro estendere le interfacce che estendere le classi, specialmente se non si possiede l'interfaccia o la classe.  Una modifica in un'interfaccia influisce su ogni classe che l'implementa.  Pertanto è meno probabile che l'autore aggiunga o modifichi i metodi in un'interfaccia.  Tuttavia, se una classe implementa due interfacce che hanno metodi di estensione con la stessa firma, nessun metodo di estensione sarà visibile.  
  
-   Estendere il tipo più specifico possibile.  In una gerarchia di tipi, se si seleziona un tipo dal quale sono derivati molti altri tipi, vi sono livelli di possibilità per l'introduzione di metodi di istanza o di altri metodi di estensione che potrebbero interferire con i propri.  
  
## Metodi di estensione, metodi di istanza e proprietà  
 Quando un metodo di istanza nell'ambito ha una firma che è compatibile con gli argomenti di un'istruzione chiamante, il metodo di istanza viene preferito a qualsiasi metodo di estensione.  Il metodo di istanza ha la precedenza anche se il metodo di estensione rappresenta una corrispondenza migliore.  Nell'esempio seguente `ExampleClass` contiene un metodo di istanza denominato `ExampleMethod` che ha un parametro di tipo `Integer`.  Il metodo di estensione `ExampleMethod` estende `ExampleClass` e ha un parametro di tipo `Long`.  
  
 [!code-vb[VbVbalrExtensionMethods#4](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_5.vb)]  
  
 La prima chiamata a `ExampleMethod` nel codice seguente chiama il metodo di estensione, poiché `arg1` è `Long` ed è compatibile solo con il parametro `Long` nel metodo di estensione.  La seconda chiamata a `ExampleMethod` ha un argomento `Integer`, `arg2`, e chiama il metodo di istanza.  
  
 [!code-vb[VbVbalrExtensionMethods#5](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_6.vb)]  
  
 Invertire ora i tipi di dati dei parametri nei due metodi:  
  
 [!code-vb[VbVbalrExtensionMethods#6](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_7.vb)]  
  
 Questa volta il codice in `Main` chiama il metodo di istanza tutte e due le volte  perché sia `arg1` che `arg2` hanno una conversione verso un tipo di dati più grande a `Long` e il metodo di istanza ha la precedenza sul metodo di estensione in entrambi casi.  
  
 [!code-vb[VbVbalrExtensionMethods#7](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_8.vb)]  
  
 Pertanto, un metodo di estensione non può sostituire un metodo di istanza esistente.  Tuttavia, quando un metodo di estensione ha lo stesso nome di un metodo di istanza ma le firme non sono in conflitto, è possibile accedere a entrambi i metodi.  Ad esempio, se la classe `ExampleClass` contiene un metodo denominato `ExampleMethod` che non accetta argomenti, sono consentiti i metodi di estensione con lo stesso nome ma con firme diversa, come mostrato nel codice seguente.  
  
 [!code-vb[VbVbalrExtensionMethods#8](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/extension-methods_9.vb)]  
  
 L'output di questo codice è il seguente:  
  
 `Extension method`  
  
 `Instance method`  
  
 La situazione è più semplice con le proprietà: se un metodo di estensione ha lo stesso nome di una proprietà della classe che estende, il metodo di estensione non è visibile e non è possibile accedervi.  
  
## Precedenza nei metodi di estensione  
 Quando due metodi di estensione che hanno firme identiche si trovano nell'ambito e sono accessibili, verrà richiamato quello con la precedenza più elevata.  La precedenza di un metodo di estensione è basata sul meccanismo utilizzato per portare il metodo nell'ambito.  Nell'elenco che segue viene indicata la gerarchia di precedenza, dalla più alta alla più bassa.  
  
1.  I metodi di estensione definiti all'interno del modulo corrente.  
  
2.  I metodi di estensione definiti nei tipi di dati nello spazio dei nomi corrente o uno dei rispettivi padri, con spazi dei nomi figlio che hanno precedenza più elevata rispetto agli spazi dei nomi padre.  
  
3.  I metodi di estensione definiti in qualsiasi importazione di tipi nel file corrente.  
  
4.  I metodi di estensione definiti in qualsiasi importazione di spazi dei nomi nel file corrente.  
  
5.  I metodi di estensione definiti in qualsiasi importazione di tipi a livello di progetto.  
  
6.  I metodi di estensione definiti in qualsiasi importazione di spazi dei nomi a livello di progetto.  
  
 Se la precedenza non risolve l'ambiguità, è possibile utilizzare il nome completo per specificare il metodo che si sta chiamando.  Se il metodo `Print` nel precedente esempio viene definito in un modulo denominato `StringExtensions`, il nome completo è `StringExtensions.Print(example)` anziché `example.Print()`.  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices>   
 <xref:System.Runtime.CompilerServices.ExtensionAttribute>   
 [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [Module Statement](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
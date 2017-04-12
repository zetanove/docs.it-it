---
title: Metodi di estensione (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ExtensionMethods
dev_langs:
- VB
helpviewer_keywords:
- extending data types
- extension methods [Visual Basic]
ms.assetid: b8020aae-374d-46a9-bcb7-8cc2390b93b6
caps.latest.revision: 41
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 381fa0db2d92590d23ebd71a7823a8465e94a6e6
ms.lasthandoff: 03/13/2017

---
# <a name="extension-methods-visual-basic"></a>Metodi di estensione (Visual Basic)
Metodi di estensione consentono agli sviluppatori di aggiungere funzionalità personalizzate ai tipi di dati che sono già definiti senza creare un nuovo tipo derivato. Metodi di estensione consentono di scrivere un metodo che può essere chiamato come se fosse un metodo di istanza del tipo esistente.  
  
## <a name="remarks"></a>Note  
 Un metodo di estensione può essere solo un `Sub` procedura o una `Function` procedura. È possibile definire una proprietà di estensione, campo o dell'evento. Tutti i metodi di estensione devono essere contrassegnati con l'attributo di estensione `<Extension()>` dal <xref:System.Runtime.CompilerServices?displayProperty=fullName>dello spazio dei nomi.</xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
 Il primo parametro in una definizione di metodo di estensione specifica quale tipo di dati si estende il metodo. Quando viene eseguito il metodo, il primo parametro è associato all'istanza del tipo di dati che richiama il metodo.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 L'esempio seguente definisce una `Print` estensione per il <xref:System.String>tipo di dati.</xref:System.String> Il metodo utilizza `Console.WriteLine` per visualizzare una stringa. Il parametro di `Print` (metodo), `aString`, stabilisce che il metodo estende la <xref:System.String>classe.</xref:System.String>  
  
 [!code-vb[VbVbalrExtensionMethods n.&1;](./codesnippet/VisualBasic/extension-methods_1.vb)]  
  
 Si noti che la definizione di metodo di estensione è contrassegnata con l'attributo di estensione `<Extension()>`. Il contrassegno del modulo in cui è definito il metodo è facoltativo, ma ogni metodo di estensione deve essere contrassegnato. <xref:System.Runtime.CompilerServices>deve essere importato per accedere all'attributo di estensione.</xref:System.Runtime.CompilerServices>  
  
 Metodi di estensione possono essere dichiarati solo all'interno di moduli. Il modulo in cui è definito un metodo di estensione non è in genere, il modulo stesso di quello in cui viene chiamato. Al contrario, viene importato il modulo che contiene il metodo di estensione, se deve essere, in modo che sia nell'ambito. Dopo il modulo che contiene `Print` è nell'ambito, il metodo può essere chiamato come se fosse un metodo di istanza comune che non accetta argomenti, ad esempio `ToUpper`:  
  
 [!code-vb[VbVbalrExtensionMethods n.&2;](./codesnippet/VisualBasic/extension-methods_2.vb)]  
  
 Nell'esempio successivo viene `PrintAndPunctuate`, è anche un'estensione di <xref:System.String>, in questo caso definito con due parametri.</xref:System.String> Il primo parametro, `aString`, stabilisce che il metodo di estensione estende <xref:System.String>.</xref:System.String> Il secondo parametro, `punc`, deve essere una stringa di segni di punteggiatura che viene passata come argomento quando viene chiamato il metodo. Il metodo visualizza la stringa seguita da segni di punteggiatura.  
  
 [!code-vb[VbVbalrExtensionMethods n.&3;](./codesnippet/VisualBasic/extension-methods_3.vb)]  
  
 Viene chiamato il metodo mediante l'invio di un argomento di stringa per `punc`:`example.PrintAndPunctuate(".")`  
  
 Nell'esempio seguente `Print` e `PrintAndPunctuate` definito e chiamato. <xref:System.Runtime.CompilerServices>viene importato nel modulo della definizione per consentire l'accesso all'attributo di estensione.</xref:System.Runtime.CompilerServices>  
  
### <a name="code"></a>Codice  
  
```vb  
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
  
 Successivamente, i metodi di estensione vengono inseriti nell'ambito e chiamati.  
  
```vb  
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
  
### <a name="comments"></a>Commenti  
 Tutto ciò che è necessario essere in grado di eseguire questi o metodi di estensione simili è che si trovino nell'ambito. Se il modulo che contiene un metodo di estensione è nell'ambito, è visibile in IntelliSense e può essere chiamato come se fosse un metodo di istanza comune.  
  
 Si noti che, quando vengono richiamati i metodi, nessun argomento viene inviato per il primo parametro. Parametro `aString` nel precedente metodo definizioni è associato a `example`, l'istanza di `String` che le chiama. Il compilatore utilizzerà `example` come argomento inviato al primo parametro.  
  
 Se viene chiamato un metodo di estensione per un oggetto che è impostato su `Nothing`, viene eseguito il metodo di estensione. Questo non è applicabile ai metodi di istanza comune. È possibile controllare in modo esplicito di `Nothing` nel metodo di estensione.  
  
## <a name="types-that-can-be-extended"></a>Tipi che possono essere estesi  
 È possibile definire un metodo di estensione nella maggior parte dei tipi che possono essere rappresentati in un elenco di parametri di Visual Basic, inclusi i seguenti:  
  
-   Classi (tipi di riferimento)  
  
-   Strutture (tipi valore)  
  
-   Interfacce  
  
-   Delegati  
  
-   Argomenti ByRef e ByVal  
  
-   Parametri di metodo generico  
  
-   Matrici  
  
 Poiché il primo parametro specifica il tipo di dati che estende il metodo di estensione, è obbligatorio e non può essere facoltativo. Per questo motivo, `Optional` parametri e `ParamArray` i parametri non possono essere il primo parametro nell'elenco di parametri.  
  
 Metodi di estensione non sono considerati in associazione tardiva. Nell'esempio seguente, l'istruzione `anObject.PrintMe()` genera un <xref:System.MissingMemberException>eccezione, la stessa eccezione verrà visualizzato se il secondo `PrintMe` definizione di metodo di estensione sono stati eliminati.</xref:System.MissingMemberException>  
  
 [!code-vb[9 VbVbalrExtensionMethods](./codesnippet/VisualBasic/extension-methods_4.vb)]  
  
## <a name="best-practices"></a>Suggerimenti  
 Metodi di estensione forniscono un modo pratico e potente per estendere un tipo esistente. Tuttavia, per poterli utilizzare correttamente, esistono alcuni punti da considerare. Queste considerazioni si applicano principalmente per gli autori di librerie di classi, ma che potrebbero influire su qualsiasi applicazione che utilizza i metodi di estensione.  
  
 In generale, i metodi di estensione che aggiungono ai tipi che non si è proprietari sono più vulnerabili rispetto ai metodi di estensione aggiunti ai tipi che è possibile controllare. Può verificarsi una serie di operazioni nelle classi non si è proprietari che possono interferire con i metodi di estensione.  
  
-   Se un membro di istanza accessibile con una firma compatibile con gli argomenti nell'istruzione di chiamata, non le conversioni necessarie dall'argomento al parametro, verrà utilizzato il metodo di istanza a qualsiasi metodo di estensione. Pertanto, se un metodo di istanza appropriato viene aggiunto a una classe a un certo punto, un membro esistente di estensione che affidano potrebbe diventare inaccessibile.  
  
-   L'autore di un metodo di estensione non può impedire agli altri programmatori di scrivere i metodi di estensione in conflitto che possono avere la precedenza sull'estensione originale.  
  
-   È possibile migliorare la robustezza inserendo i metodi di estensione nel proprio spazio dei nomi. I consumer della libreria possono includere uno spazio dei nomi o escluderlo o selezionare tra gli spazi dei nomi, separatamente dal resto della libreria.  
  
-   Potrebbe essere preferibile estendere interfacce piuttosto che di estendere le classi, soprattutto se non si dispone di interfaccia o classe. Una modifica in un'interfaccia influisce su ogni classe che lo implementa. Pertanto, l'autore potrebbe essere meno probabile che aggiungere o modificare i metodi in un'interfaccia. Tuttavia, se una classe implementa due interfacce che dispongono di metodi di estensione con la stessa firma, nessuno dei due metodi di estensione sono visibili.  
  
-   Estendere il tipo più specifico che possibile. In una gerarchia di tipi, se si seleziona un tipo da cui derivano molti altri tipi, sono disponibili livelli di possibilità per l'introduzione di metodi di istanza o altri metodi di estensione che potrebbero interferire con i propri.  
  
## <a name="extension-methods-instance-methods-and-properties"></a>Proprietà, metodi di istanza e metodi di estensione  
 Quando un metodo di istanza nell'ambito ha una firma compatibile con gli argomenti di un'istruzione di chiamata, viene scelto il metodo di istanza a qualsiasi metodo di estensione. Il metodo di istanza ha la precedenza anche se il metodo di estensione è una corrispondenza migliore. Nell'esempio seguente, `ExampleClass` contiene un metodo di istanza denominato `ExampleMethod` che ha un parametro di tipo `Integer`. Metodo di estensione `ExampleMethod` estende `ExampleClass`, e ha un parametro di tipo `Long`.  
  
 [!code-vb[VbVbalrExtensionMethods n.&4;](./codesnippet/VisualBasic/extension-methods_5.vb)]  
  
 La prima chiamata a `ExampleMethod` nel codice seguente chiama il metodo di estensione, poiché `arg1` è `Long` ed è compatibile solo con il `Long` parametro nel metodo di estensione. La seconda chiamata a `ExampleMethod` ha un `Integer` argomento, `arg2`, e chiama il metodo di istanza.  
  
 [!code-vb[VbVbalrExtensionMethods n.&5;](./codesnippet/VisualBasic/extension-methods_6.vb)]  
  
 Invertire ora i tipi di dati dei parametri nei due metodi:  
  
 [!code-vb[6 VbVbalrExtensionMethods](./codesnippet/VisualBasic/extension-methods_7.vb)]  
  
 Questa volta il codice in `Main` chiama il metodo di istanza due volte. Infatti, entrambi `arg1` e `arg2` dispone di una conversione di ampliamento per `Long`, e il metodo di istanza ha la precedenza sul metodo di estensione in entrambi i casi.  
  
 [!code-vb[VbVbalrExtensionMethods&#7;](./codesnippet/VisualBasic/extension-methods_8.vb)]  
  
 Di conseguenza, un metodo di estensione non può sostituire un metodo di istanza esistenti. Tuttavia, quando un metodo di estensione ha lo stesso nome di un metodo di istanza, ma le firme non sono in conflitto, entrambi i metodi sono accessibili. Ad esempio, se classe `ExampleClass` contiene un metodo denominato `ExampleMethod` che non accetta argomenti, i metodi di estensione con lo stesso nome ma sono consentite firme diverse, come illustrato nel codice seguente.  
  
 [!code-vb[VbVbalrExtensionMethods n.&8;](./codesnippet/VisualBasic/extension-methods_9.vb)]  
  
 L'output da questo codice è come segue:  
  
 `Extension method`  
  
 `Instance method`  
  
 La situazione è più semplice con le proprietà: se un metodo di estensione ha lo stesso nome di una proprietà della classe che estende, il metodo di estensione non è visibile e non è accessibile.  
  
## <a name="extension-method-precedence"></a>Precedenza nei metodi di estensione  
 Quando due metodi di estensione che presentano firme identiche incluse nell'ambito e accessibile, verrà richiamato quello con priorità più alta. La priorità di un metodo di estensione è basata sul meccanismo utilizzato per portare il metodo nell'ambito. Nell'elenco seguente viene illustrata la gerarchia di precedenza, dal più alto al più basso.  
  
1.  Metodi di estensione definiti all'interno del modulo corrente.  
  
2.  Metodi di estensione definiti all'interno di dati tipi di spazio dei nomi corrente o uno qualsiasi dei relativi elementi padre, con spazi dei nomi figlio con precedenza maggiore rispetto a spazi dei nomi padre.  
  
3.  Metodi di estensione definiti in qualsiasi tipo di importazione del file corrente.  
  
4.  Metodi di estensione definiti in qualsiasi importazione dello spazio dei nomi nel file corrente.  
  
5.  Metodi di estensione definiti in qualsiasi tipo di progetto a livello di importazione.  
  
6.  Metodi di estensione definiti in qualsiasi importazione dello spazio dei nomi a livello di progetto.  
  
 Se la priorità non consente di risolvere l'ambiguità, è possibile utilizzare il nome completo per specificare il metodo che si sta chiamando. Se il `Print` metodo nell'esempio precedente viene definito in un modulo denominato `StringExtensions`, il nome completo è `StringExtensions.Print(example)` invece di `example.Print()`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices></xref:System.Runtime.CompilerServices>   
 <xref:System.Runtime.CompilerServices.ExtensionAttribute></xref:System.Runtime.CompilerServices.ExtensionAttribute>   
 [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [Module (istruzione)](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Parametri facoltativi](./optional-parameters.md)   
 [Matrici di parametri](./parameter-arrays.md)   
 [Cenni preliminari sugli attributi](../../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [Ambito in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)

---
title: nameof (Riferimenti di C# e Visual Basic) | Microsoft Docs
ms.date: 2017-03-03
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- nameof_CSharpKeyword
- nameof
dev_langs:
- CSharp
ms.assetid: 33601bf3-cc2c-4496-846d-f9679bccf2a7
caps.latest.revision: 3
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
ms.translationtype: Human Translation
ms.sourcegitcommit: dc1c456c71efb3cc6e60a8fdc77384e65975f110
ms.openlocfilehash: da3fef282ac71de07057131069bf58d4f761ad2d
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="nameof-c-and-visual-basic-reference"></a>nameof (Riferimenti di C# e Visual Basic)

Usata per ottenere il nome di stringa semplice (non qualificata) di una variabile, un tipo o un membro.  

Quando si segnalano errori nel codice, si associano collegamenti MVC (Model-View-Controller), si attivano eventi di modifica delle proprietà, è spesso necessario acquisire il nome di stringa di un metodo.  Con `nameof` è possibile garantire la validità del codice in caso di ridenominazione delle definizioni.  In precedenza, per fare riferimento alle definizioni era necessario usare valori letterali di stringa. Questo approccio tuttavia non è efficace quando si rinominano elementi del codice poiché gli strumenti non hanno l'indicazione di verificare questi valori letterali di stringa.  
  
 Il formato dell'espressione `nameof` è il seguente:  
  
```csharp  
if (x == null) throw new ArgumentNullException(nameof(x));  
WriteLine(nameof(person.Address.ZipCode)); // prints "ZipCode"  
```  
  
## <a name="key-use-cases"></a>Casi di utilizzo principali  
 Questi esempi illustrano i casi di utilizzo principali relativi a `nameof`.  
  
 Convalida dei parametri:  
 ```csharp  
void f(string s) {  
    if (s == null) throw new ArgumentNullException(nameof(s));  
}  
```  
  
 Collegamenti ad azioni MVC:  
 ```html  
<%= Html.ActionLink("Sign up",  
             @typeof(UserController),  
             @nameof(UserController.SignUp))  
%>  
```  
  
 INotifyPropertyChanged:  
 ```csharp  
int p {  
    get { return this.p; }  
    set { this.p = value; PropertyChanged(this, new PropertyChangedEventArgs(nameof(this.p)); } // nameof(p) works too  
}  
```  
  
 Proprietà di dipendenza XAML:  
 ```csharp  
public static DependencyProperty AgeProperty = DependencyProperty.Register(nameof(Age), typeof(int), typeof(C));  
```  
  
 Registrazione:  
 ```csharp  
void f(int i) {  
    Log(nameof(f), "method entry");  
}  
```  
  
 Attributi:  
 ```csharp  
[DebuggerDisplay("={" + nameof(GetString) + "()}")]  
class C {  
    string GetString() { }  
}  
```  
  
## <a name="examples"></a>Esempi  
 Alcuni esempi per C#:  
  
```csharp  
using Stuff = Some.Cool.Functionality  
class C {  
    static int Method1 (string x, int y) {}  
    static int Method1 (string x, string y) {}  
    int Method2 (int z) {}  
    string f<T>() => nameof(T);  
}  
  
var c = new C()  
  
nameof(C) -> "C"  
nameof(C.Method1) -> "Method1"   
nameof(C.Method2) -> "Method2"  
nameof(c.Method1) -> "Method1"   
nameof(c.Method2) -> "Method2"  
nameof(z) -> "z" // inside of Method2 ok, inside Method1 is a compiler error  
nameof(Stuff) = "Stuff"  
nameof(T) -> "T" // works inside of method but not in attributes on the method  
nameof(f) -> "f"  
nameof(f<T>) -> syntax error  
nameof(f<>) -> syntax error  
nameof(Method2()) -> error "This expression does not have a name"  
```  
  
 Molti degli esempi sopra riportati sono validi per Visual Basic.  Ecco invece alcuni esempi specifici di Visual Basic:  
  
```vb  
NameOf(a!Foo) -> ' error  "This expression does not have a name"  
NameOf(dict("Foo")) -> ' error  "This expression does not have a name": default property access  
NameOf(dict.Item("Foo")) -> ' error  "This expression does not have a name"  
NameOf(arr(2)) -> ' error  "This expression does not have a name": array element index  
Dim x = Nothing   
NameOf(x.ToString(2)) -> ' error  "This expression does not have a name"  
Dim o = Nothing  
NameOf(o.Equals) -> ' result "Equals".  Warning: "Access of static member of instance; instance will not be evaluated"  
```  
  
## <a name="remarks"></a>Note  
 L'argomento di `nameof` deve essere un nome semplice, un nome qualificato, un accesso di tipo membro, un accesso di base con un membro specificato oppure questo accesso con un membro specificato.  L'espressione dell'argomento identifica una definizione di codice, ma non viene mai valutata.  
  
 Dal momento che l'argomento deve essere un'espressione dal punto di vista sintattico, sono presenti molti elementi non consentiti che non è utile elencare.  Vale la pena di menzionare i seguenti, che sono quelli che producono errori, ovvero tipi predefiniti (ad esempio `int` o `void`), tipi nullable (`Point?`), tipi di matrice (`Customer[,]`), tipi di puntatore (`Buffer*`), alias qualificati (`A::B`) e tipi generici non associati (`Dictionary<,>`), nonché simboli di pre-elaborazione (`DEBUG`) ed etichette (`loop:`).  
  
 Se è necessario ottenere il nome completo, è possibile usare l'espressione `typeof` unitamente a `nameof`.  Ad esempio:
```csharp  
class C {
    void f(int i) {  
        Log($"{typeof(C)}.{nameof(f)}", "method entry");  
    }
}
``` 

 Purtroppo `typeof` non è un'espressione costante come `nameof`, quindi non è possibile usare `typeof` in combinazione con `nameof` in tutti i punti in cui è possibile usare `nameof`.  Ad esempio, quanto segue genera un errore di compilazione CS0182:
 ```csharp  
[DebuggerDisplay("={" + typeof(C) + nameof(GetString) + "()}")]  
class C {  
    string GetString() { }  
}  
```    
 Negli esempi si nota che è possibile usare un nome di tipi e accedere a un nome di metodo di istanza.  Non è necessario disporre di un'istanza del tipo, come richiesto nelle espressioni valutate.  In alcune situazioni può risultare molto comodo usare il nome del tipo ma, dal momento che viene fatto riferimento solo al nome senza usare i dati dell'istanza, non è necessario optare per un'espressione o una variabile di istanza.  
  
 È possibile fare riferimento ai membri di una classe in espressioni di attributo nella classe.  
  
 Non esiste alcun modo per ottenere informazioni sulle firme, ad esempio con "`Method1 (str, str)`".  A tale scopo è possibile usare un'espressione `Expression e = () => A.B.Method1("s1", "s2")` ed estrarre MemberInfo dall'albero delle espressioni risultante.  
  
## <a name="language-specifications"></a>Specifiche del linguaggio  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
 Per altre informazioni, vedere [Riferimenti per il linguaggio Visual Basic](../../../visual-basic/language-reference/index.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [Riferimenti per il linguaggio Visual Basic](../../../visual-basic/language-reference/index.md)   
 [Guida per programmatori Visual Basic](../../../visual-basic/programming-guide/index.md)


---
title: "Enhancing Debugging with the Debugger Display Attributes | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "debugger, display attributes"
  - "DebuggerTypeProxyAttribute attribute"
  - "debugging [.NET Framework], debugger display attributes"
  - "DebuggerDisplayAttribute attribute"
  - "display attributes for debugger"
  - "DebuggerBrowsableAttribute attribute"
ms.assetid: 72bb7aa9-459b-42c4-9163-9312fab4c410
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Enhancing Debugging with the Debugger Display Attributes
Gli attributi di visualizzazione del debugger consentono allo sviluppatore del tipo, che meglio conosce il comportamento di tale tipo in fase di esecuzione, di specificare anche l'aspetto che il tipo dovrà avere quando verrà visualizzato in un debugger.  Inoltre, gli attributi di visualizzazione che forniscono una proprietà `Target` possono essere applicati a livello di assembly da utenti che non hanno alcuna conoscenza del codice sorgente.  L'attributo <xref:System.Diagnostics.DebuggerDisplayAttribute> controlla la modalità di visualizzazione di un tipo o di un membro nelle finestre delle variabili del debugger.  L'attributo <xref:System.Diagnostics.DebuggerBrowsableAttribute> determina se e come una proprietà o un campo viene visualizzato nelle finestre delle variabili del debugger.  L'attributo <xref:System.Diagnostics.DebuggerTypeProxyAttribute> specifica un tipo di sostituzione, ovvero un proxy, per un tipo e cambia la modalità di visualizzazione del tipo nelle finestre del debugger.  Quando viene visualizzata una variabile a cui è associato un proxy, quest'ultimo sostituisce il tipo originale nella finestra di visualizzazione del debugger**.** Nella finestra delle variabili del debuggervengono visualizzati soltanto i membri pubblici del tipo proxy.  I membri privati non vengono visualizzati.  
  
## Utilizzo dell'attributo DebuggerDisplayAttribute  
 Il costruttore <xref:System.Diagnostics.DebuggerDisplayAttribute.%23ctor%2A> ha un unico argomento, ovvero una stringa da visualizzare nella colonna Valore per le istanze del tipo.  Questa stringa può contenere parentesi graffe \({ e }\).  Il testo racchiuso tra parentesi graffe viene valutato come un'espressione.  Ad esempio, il codice C\# riportato di seguito fa sì che venga visualizzata la stringa "Count \= 4" quando viene selezionato il segno più \(\+\) per espandere la visualizzazione del debugger per un'istanza di `MyHashtable`.  
  
```  
[DebuggerDisplay("Count = {count}")]  
class MyHashtable  
{  
    public int count = 4;  
}  
```  
  
 Gli attributi applicati alle proprietà a cui si fa riferimento nell'espressione non vengono elaborati.  Per il compilatore C\# è consentita un'espressione generale che abbia soltanto accesso implicito a questo riferimento per l'istanza corrente del tipo di destinazione.  L'espressione è limitata, ovvero non ha accesso ad alias, variabili locali o puntatori.  Nel codice C\# è possibile utilizzare un'espressione generale tra le parentesi graffe cha abbia soltanto accesso implicito al puntatore `this` per l'istanza corrente del tipo di destinazione.  
  
 Se ad esempio un oggetto C\# possiede una funzione `ToString()` sottoposta a override, il debugger chiamerà l'override e ne visualizzerà il risultato anziché la stringa standard `{<typeName>}.` Pertanto, se è stato eseguito l'override di `ToString()`, non è necessario utilizzare <xref:System.Diagnostics.DebuggerDisplayAttribute>.  Se si utilizzano entrambi, l'attributo <xref:System.Diagnostics.DebuggerDisplayAttribute> avrà la precedenza sull'override di `ToString()`.  
  
## Utilizzo dell'attributo DebuggerBrowsableAttribute  
 Applicare l'attributo <xref:System.Diagnostics.DebuggerBrowsableAttribute> a un campo o una proprietà per specificare la modalità di visualizzazione del campo o della proprietà nella finestra del debugger.  Il costruttore di questo attributo accetta uno dei valori di enumerazione <xref:System.Diagnostics.DebuggerBrowsableState>, che specifica uno dei seguenti stati:  
  
-   <xref:System.Diagnostics.DebuggerBrowsableState> indica che il membro non è visualizzato nella finestra dei dati.  Ad esempio, utilizzando questo valore per la classe <xref:System.Diagnostics.DebuggerBrowsableAttribute> in un campo, il campo viene rimosso dalla gerarchia e non viene visualizzato quando si espande il tipo contenitore facendo clic sul segno più \(\+\) per l'istanza del tipo.  
  
-   <xref:System.Diagnostics.DebuggerBrowsableState> indica che i membri sono visualizzati ma non espansi per impostazione predefinita.  Questo è il comportamento predefinito.  
  
-   <xref:System.Diagnostics.DebuggerBrowsableState> indica che il membro stesso non deve essere visualizzato, ma gli oggetti che lo costituiscono devono essere visualizzati se si tratta di una matrice o di una raccolta.  
  
> [!NOTE]
>  L'attributo <xref:System.Diagnostics.DebuggerBrowsableAttribute> non è supportato da Visual Basic in .NET Framework versione 2.0.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare l'attributo <xref:System.Diagnostics.DebuggerBrowsableAttribute> per impedire che la proprietà che segue l'attributo venga visualizzata nella finestra di debug relativa alla classe.  
  
```  
[DebuggerBrowsable(DebuggerBrowsableState.Never)]  
public static string y = "Test String";  
```  
  
## Utilizzo dell'attributo DebuggerTypeProxy  
 Utilizzare l'attributo <xref:System.Diagnostics.DebuggerTypeProxyAttribute> quando è necessario modificare radicalmente la visualizzazione di un tipo nel debugger, senza modificare il tipo stesso.  L'attributo <xref:System.Diagnostics.DebuggerTypeProxyAttribute> viene utilizzato per specificare un proxy di visualizzazione per un tipo, consentendo a uno sviluppatore di personalizzare la visualizzazione del tipo.  Analogamente a <xref:System.Diagnostics.DebuggerDisplayAttribute>, questo attributo può essere utilizzato a livello di assembly, nel qual caso la proprietà <xref:System.Diagnostics.DebuggerTypeProxyAttribute.Target%2A> specifica il tipo per il quale verrà utilizzato il proxy.  Si consiglia di utilizzare questo attributo per specificare un tipo privato annidato che si trova all'interno del tipo al quale viene applicato l'attributo.  Un analizzatore di espressioni che supporta i visualizzatori di tipi verifica la presenza di questo attributo al momento della visualizzazione di un tipo.  Se l'attributo viene rilevato, l'analizzatore di espressioni sostituisce il tipo a cui è applicato l'attributo con il tipo proxy di visualizzazione.  
  
 Quando è presente <xref:System.Diagnostics.DebuggerTypeProxyAttribute>, nella finestra delle variabili del debugger vengono visualizzati solo i membri pubblici del tipo proxy.  I membri privati non vengono visualizzati.  Il comportamento della finestra dei dati rimane invariato.  
  
 Per evitare di ridurre inutilmente le prestazioni, gli attributi del proxy di visualizzazione non vengono elaborati fino a quando l'oggetto non viene espanso, mediante il clic dell'utente sul segno più \(\+\) accanto al tipo in una finestra dei dati o mediante l'applicazione dell'attributo <xref:System.Diagnostics.DebuggerBrowsableAttribute>.  Si consiglia pertanto di non applicare attributi al tipo di visualizzazione.  ma di applicarli nel corpo del tipo visualizzato.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare l'attributo <xref:System.Diagnostics.DebuggerTypeProxyAttribute> per specificare un tipo da utilizzare come proxy di visualizzazione nel debugger.  
  
```  
  
[DebuggerTypeProxy(typeof(HashtableDebugView))]  
class MyHashtable : Hashtable  
{  
    private const string TestString =   
        "This should not appear in the debug window.";  
  
    internal class HashtableDebugView  
    {  
        private Hashtable hashtable;  
        public const string TestStringProxy =   
            "This should appear in the debug window.";  
  
        // The constructor for the type proxy class must have a   
        // constructor that takes the target type as a parameter.  
        public HashtableDebugView(Hashtable hashtable)  
        {  
            this.hashtable = hashtable;  
        }  
    }  
}  
```  
  
## Esempio  
  
### Descrizione  
 L'esempio di codice riportato di seguito può essere eseguito in [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] per vedere i risultati dell'applicazione degli attributi <xref:System.Diagnostics.DebuggerDisplayAttribute>, <xref:System.Diagnostics.DebuggerBrowsableAttribute> e <xref:System.Diagnostics.DebuggerTypeProxyAttribute>.  
  
### Codice  
 [!code-cpp[System.Diagnostics.DebuggerBrowsableAttribute#1](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Diagnostics.DebuggerBrowsableAttribute/cpp/program.cpp#1)]
 [!code-csharp[System.Diagnostics.DebuggerBrowsableAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Diagnostics.DebuggerBrowsableAttribute/CS/program.cs#1)]
 [!code-vb[System.Diagnostics.DebuggerBrowsableAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Diagnostics.DebuggerBrowsableAttribute/VB/module1.vb#1)]  
  
## Vedere anche  
 <xref:System.Diagnostics.DebuggerDisplayAttribute>   
 <xref:System.Diagnostics.DebuggerBrowsableAttribute>   
 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>
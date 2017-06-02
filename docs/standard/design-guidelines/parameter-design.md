---
title: "Progettazione di parametri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "membro linee guida di progettazione [.NET Framework], parametri"
  - "membri [.NET Framework], parametri"
  - "nomi di parametri [.NET Framework]"
  - "parametri, linee guida di progettazione"
  - "parametri riservati"
ms.assetid: 3f33bf46-4a7b-43b3-bb78-1ffebe0dcfa6
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Progettazione di parametri
Questa sezione vengono fornite linee guida generali per la progettazione del parametro, incluse sezioni con linee guida per la verifica di argomenti. Inoltre, è consigliabile consultare le istruzioni riportate in [Denominazione dei parametri](../../../docs/standard/design-guidelines/naming-parameters.md).  
  
 **✓ si** utilizzare il tipo di parametro meno derivato che fornisce le funzionalità richieste da un membro.  
  
 Si supponga, ad esempio, che si desidera progettare un metodo che enumera una raccolta e la stampa di ogni elemento nella console. Tale metodo deve richiedere <xref:System.Collections.IEnumerable> come parametro, non <xref:System.Collections.ArrayList> o <xref:System.Collections.IList>, ad esempio.  
  
 **X non** utilizzare parametri riservati.  
  
 Se più input a un membro è necessaria nelle versioni future, è possibile aggiungere un nuovo overload.  
  
 **X non** sono esposte pubblicamente i metodi che accettano puntatori, matrici di puntatori o le matrici multidimensionali come parametri.  
  
 I puntatori e matrici multidimensionali sono relativamente difficili da utilizzare in modo corretto. In quasi tutti i casi, le API possono essere riprogettate per evitare di creare questi tipi come parametri.  
  
 **✓ si** posizionare tutti `out` dopo tutti i valori da parametri e `ref` parametri \(escluse le matrici di parametri\), anche se il risultato è un'incoerenza nel parametro ordinamento tra gli overload \(vedere [Overload dei membri](../../../docs/standard/design-guidelines/member-overloading.md)\).  
  
 Il `out` i parametri possono essere considerati come valori di ritorno a capo e raggruppandoli rende più facile da comprendere la firma del metodo.  
  
 **✓ si** coerente nella denominazione dei parametri quando si esegue l'override di membri o di implementazione di membri di interfaccia.  
  
 Questo comunica meglio la relazione tra i metodi.  
  
### Scelta tra l'enumerazione e i parametri booleani  
 **✓ si** utilizzare enumerazioni se un membro in caso contrario sarebbe due o più parametri Boolean.  
  
 **X non** utilizzare valori booleani, a meno che non si è assolutamente certi non vi sarà mai la necessità di più di due valori.  
  
 Le enumerazioni offrono spazio per la successiva aggiunta di valori, ma è necessario essere consapevoli di tutte le implicazioni dell'aggiunta di valori per le enumerazioni, descritti in [Progettazione di enum](../../../docs/standard/design-guidelines/enum.md).  
  
 **✓ PROVARE** utilizzando i valori booleani per parametri del costruttore che sono effettivamente due stati, valori e vengono semplicemente utilizzati per inizializzare le proprietà booleane.  
  
### Convalida di argomenti  
 **✓ si** convalidare gli argomenti passati ai membri pubblici, protetti o implementati in modo esplicito. Generare <xref:System.ArgumentException?displayProperty=fullName>, o una delle sue sottoclassi, se la convalida non riesce.  
  
 Si noti che la convalida effettiva non deve necessariamente essere eseguita nel membro pubblico o protetto stesso. Questo può verificarsi con un livello inferiore in alcune routine privata o interna. Il punto principale è che l'intera area della superficie esposta agli utenti finali controlla gli argomenti.  
  
 **✓ si** generare <xref:System.ArgumentNullException> Se viene passato un argomento null e il membro non supporta argomenti null.  
  
 **✓ si** la convalida dei parametri di enumerazione.  
  
 Non presupporre gli argomenti enum saranno nell'intervallo definito dal tipo enum. CLR consente di eseguire il cast di qualsiasi valore intero in un valore di enumerazione, anche se il valore non è definito nell'enumerazione.  
  
 **X non** utilizzare <xref:System.Enum.IsDefined%2A?displayProperty=fullName> per intervallo di enumerazione controlla.  
  
 **✓ si** tenere presente che gli argomenti modificabili potrebbero essere state modificate dopo che sono stati convalidati.  
  
 Se il membro è basata sulla protezione, vengono fornite informazioni utili per creare una copia e quindi convalidare ed elaborare l'argomento.  
  
### Passaggio dei parametri  
 Dalla prospettiva di una finestra di progettazione di framework, sono disponibili tre gruppi principali di parametri: parametri, dal valore `ref` parametri, e `out` i parametri.  
  
 Quando viene passato un argomento tramite un parametro per valore, il membro riceve una copia dell'argomento effettivo passato. Se l'argomento è un tipo di valore, una copia dell'argomento viene inserita nello stack. Se l'argomento è un tipo di riferimento, una copia del riferimento viene inserita nello stack. Più diffusi linguaggi CLR, ad esempio c\#, Visual Basic.NET e C\+\+, predefinito per il passaggio di parametri per valore.  
  
 Quando si passa un argomento tramite un `ref` parametro, il membro riceve un riferimento all'argomento effettivo passato. Se l'argomento è un tipo di valore, viene inserito un riferimento all'argomento nello stack. Se l'argomento è un tipo di riferimento, un riferimento al riferimento viene inserito nello stack.`Ref` parametri possono essere utilizzati per consentire il membro modificare gli argomenti passati dal chiamante.  
  
 `Out` i parametri sono simili a `ref` parametri, con alcune piccole differenze. Il parametro verrà considerato inizialmente non assegnati e non può essere letto nel corpo del membro prima che viene assegnato un valore. Inoltre, il parametro deve essere assegnato un valore prima che venga restituito il membro.  
  
 **X evitare** mediante `out` o `ref` parametri.  
  
 Utilizzo `out` o `ref` parametri richiede esperienza nell'utilizzo dei puntatori, conoscenza delle differiscano tra tipi di valore e tipi di riferimento e dei metodi con più valori restituiti. Inoltre, la differenza tra `out` e `ref` parametri spesso non è compresa. Gli architetti di Framework progettazione per un pubblico generico non prevedere che gli utenti in grado di utilizzare i `out` o `ref` parametri.  
  
 **X non** passare tipi di riferimento per riferimento.  
  
 Esistono alcune eccezioni alla regola, ad esempio un metodo che può essere utilizzato per scambiare i riferimenti.  
  
### Membri con un numero variabile di parametri  
 I membri che possono accettare un numero variabile di argomenti vengono espressi, fornendo un parametro di matrice. Ad esempio, <xref:System.String> fornisce il metodo seguente:  
  
```  
public class String {  
    public static string Format(string format, object[] parameters);  
}  
```  
  
 Un utente può quindi chiamare il <xref:System.String.Format%2A?displayProperty=fullName> \(metodo\), come indicato di seguito:  
  
 `String.Format("File {0} not found in {1}",new object[]{filename,directory});`  
  
 Aggiunta della parola chiave params di c\# per un parametro di matrice viene modificato il parametro a un parametro di matrice params cosiddette e fornisce un collegamento per la creazione di una matrice temporanea.  
  
```  
public class String {  
    public static string Format(string format, params object[] parameters);  
}  
```  
  
 Questa operazione consente all'utente di chiamare il metodo passando gli elementi della matrice direttamente nell'elenco di argomenti.  
  
 `String.Format("File {0} not found in {1}",filename,directory);`  
  
 Si noti che la parola chiave params può essere aggiunto solo l'ultimo parametro nell'elenco di parametri.  
  
 **✓ PROVARE** aggiungendo la parola chiave params ai parametri di matrice, se si prevede che gli utenti finali di passare le matrici con un numero ridotto di elementi. Se è previsto che un numero elevato di elementi verrà passato in comune gli scenari, gli utenti probabilmente non supera comunque inline questi elementi e pertanto non è necessaria la parola chiave params.  
  
 **X evitare** utilizzando matrici params se il chiamante sarebbe quasi sempre l'input già presente una matrice.  
  
 Ad esempio, i membri con i parametri di matrice di byte non sarebbero quasi mai essere chiamati passando singoli byte. Per questo motivo, i parametri di matrice di byte in .NET Framework non utilizzano la parola chiave params.  
  
 **X non** utilizzare matrici params se la matrice viene modificata dal membro che accetta il parametro di matrice params.  
  
 A causa il fatto che molti compilatori gli argomenti per il membro in una matrice temporanea nel sito di chiamata, la matrice potrebbe essere un oggetto temporaneo e pertanto tutte le modifiche alla matrice andranno persi.  
  
 **✓ PROVARE** utilizzando la parola chiave params in un overload semplice, anche se potrebbe non utilizza un overload più complesso.  
  
 È necessario stabilire se gli utenti importanza la presenza di una matrice di parametri in uno degli overload anche se non è stato in tutti gli overload.  
  
 **✓ si** tenta di ordinare i parametri per consentire di utilizzare la parola chiave params.  
  
 **✓ PROVARE** fornisce overload speciali e i percorsi di codice per le chiamate con un numero ridotto di argomenti nelle API estremamente sensibili alle prestazioni.  
  
 Questo rende possibile per evitare di creare oggetti matrice quando viene chiamata l'API con un numero ridotto di argomenti. Modulo i nomi dei parametri eseguendo una forma singolare del parametro della matrice e aggiunta di un suffisso numerico.  
  
 È consigliabile farlo solo se si prevede per l'intero percorso del codice speciale, non solo creare una matrice e chiamare il metodo più generico.  
  
 **✓ si** tenere presente che null può essere passato come argomento di matrice params.  
  
 È necessario convalidare che la matrice non sia null prima dell'elaborazione.  
  
 **X non** utilizzare il `varargs` metodi, altrimenti noti come i puntini di sospensione.  
  
 Alcuni linguaggi CLR, quali C\+\+, supportano una convenzione alternativa per il passaggio di elenchi di parametri variabile denominati `varargs` metodi. La convenzione di non utilizzare nel Framework, perché non è conforme a CLS.  
  
### Parametri del puntatore  
 In generale, i puntatori non devono essere visualizzati nell'area di superficie di un framework di codice gestito ben progettata. La maggior parte dei casi, i puntatori devono essere incapsulati. Tuttavia, in alcuni casi sono richiesti per motivi di interoperabilità tra i puntatori e utilizzando i puntatori in questi casi è appropriato.  
  
 **✓ si** forniscono un'alternativa per i membri che accetta un argomento di puntatore, poiché i puntatori non sono conformi a CLS.  
  
 **X evitare** in questo argomento costoso il controllo degli argomenti del puntatore.  
  
 **✓ si** convenzioni comuni correlate al puntatore durante la progettazione di membri con i puntatori.  
  
 Ad esempio, è necessario passare l'indice di inizio, perché aritmetica dei puntatori semplice può essere utilizzata per ottenere lo stesso risultato.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)
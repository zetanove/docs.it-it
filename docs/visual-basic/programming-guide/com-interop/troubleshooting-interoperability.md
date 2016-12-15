---
title: "Troubleshooting Interoperability (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "interop, deploying assemblies"
  - "assemblies [Visual Basic]"
  - "interop, installing assemblies that share components"
  - "COM objects, troubleshooting"
  - "interop, sharing components"
  - "troubleshooting interoperability"
  - "interoperability, troubleshooting"
  - "COM interop, troubleshooting"
  - "assemblies [Visual Basic], deploying"
  - "troubleshooting Visual Basic, interoperability"
  - "interop assemblies"
  - "interoperability, sharing components"
  - "shared components, using with assemblies"
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Troubleshooting Interoperability (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Durante l'interazione tra COM e codice gestito di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], potrebbero verificarsi alcuni dei problemi più comuni descritti di seguito.  
  
##  <a name="vbconinteroperabilitymarshalinganchor1"></a> Marshalling di interoperabilità  
 Può essere talvolta necessario utilizzare tipi di dati che non fanno parte di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  Anche se gli assembly di interoperabilità gestiscono la maggior parte delle operazioni relative agli oggetti COM, potrebbe essere necessario controllare i tipi di dati utilizzati quando gli oggetti gestiti sono esposti a COM.  Nelle strutture delle librerie di classi, ad esempio, è necessario che sia specificato il tipo non gestito `BStr` nelle stringhe inviate a oggetti COM creati mediante Visual Basic 6.0 e versioni precedenti.  In questi casi è possibile utilizzare l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> per far sì che i tipi gestiti vengano esposti come tipi non gestiti.  
  
##  <a name="vbconinteroperabilitymarshalinganchor2"></a> Esportazione di stringhe di lunghezza fissa in codice non gestito  
 In Visual Basic 6.0 e nelle versioni precedenti le stringhe vengono esportate in oggetti COM come sequenze di byte senza un carattere di terminazione null.  Per garantire la compatibilità con altri linguaggi, in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] viene incluso un carattere di terminazione durante l'esportazione delle stringhe.  Il metodo migliore per gestire il problema dell'incompatibilità consiste nell'esportare le stringhe senza carattere di terminazione come matrici di `Byte` o `Char`.  
  
##  <a name="vbconinteroperabilitymarshalinganchor3"></a> Esportazione delle gerarchie di ereditarietà  
 Quando vengono esposte come oggetti COM, le gerarchie di classi gestite risultano a un solo livello.  Ad esempio, se si definisce una classe base con un membro e quindi si eredita la classe base in una classe derivata esposta come oggetto COM, i client che utilizzano la classe derivata nell'oggetto COM non saranno in grado di utilizzare i membri ereditati.  È possibile accedere ai membri della classe base dagli oggetti COM solo come istanze di una classe base e solo se anche la classe base è creata come oggetto COM.  
  
## Metodi di overload  
 Benché sia possibile creare metodi di overload con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], questi non sono supportati da COM.  Quando una classe contenente metodi di overload viene esposta come oggetto COM, per i metodi di overload vengono generati nuovi nomi.  
  
 Ad esempio, si consideri una classe con due overload del metodo `Synch`.  Quando la classe viene esposta come oggetto COM, è possibile che i nuovi nomi generati siano `Synch` e `Synch_2`.  
  
 La ridenominazione può provocare due problemi per i consumer dell'oggetto COM.  
  
1.  È possibile che i client non si aspettino i nomi dei metodi generati.  
  
2.  I nomi dei metodi generati nella classe esposta come oggetto COM potrebbero cambiare quando vengono aggiunti nuovi overload alla classe o alla classe base.  Questa situazione può provocare problemi di controllo della versione.  
  
 Per risolvere entrambi i problemi, assegnare a ogni metodo un nome univoco anziché utilizzare l'overload quando si sviluppano oggetti che saranno esposti come oggetti COM.  
  
##  <a name="vbconinteroperabilitymarshalinganchor4"></a> Utilizzo di oggetti COM attraverso assembly di interoperabilità  
 Gli assembly di interoperabilità vengono utilizzati come se fossero codice gestito in sostituzione degli oggetti COM che rappresentano.  Tuttavia, poiché gli assembly di interoperabilità sono wrapper e non veri e propri oggetti COM, vi sono alcune differenze tra l'utilizzo di questi assembly e degli assembly standard.  Le differenze riguardano ad esempio l'esposizione delle classi e dei tipi di dati di parametri e valori restituiti.  
  
##  <a name="vbconinteroperabilitymarshalinganchor5"></a> Classi esposte sia come interfacce sia come classi  
 A differenza delle classi degli assembly standard, le classi COM sono esposte in assembly di interoperabilità sia come interfaccia sia come classi che rappresentano le classi COM.  Il nome dell'interfaccia è identico a quello della classe COM.  La classe di interoperabilità ha lo stesso nome della classe COM originale, a cui è aggiunto il suffisso "Class".  Si supponga ad esempio che un progetto contenga un riferimento a un assembly di interoperabilità per un oggetto COM.  Se la classe COM è denominata `MyComClass`, IntelliSense e il Visualizzatore oggetti mostreranno un'interfaccia denominata `MyComClass` e una classe denominata `MyComClassClass`.  
  
##  <a name="vbconinteroperabilitymarshalinganchor6"></a> Creazione di istanze di classi .NET Framework  
 Un'istanza di una classe [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] in genere viene creata mediante l'istruzione `New` con un nome di classe.  L'istruzione `New` può essere utilizzata con un'interfaccia solo quando una classe COM è rappresentata da un assembly di interoperabilità.  A meno che non si usi la classe COM con un'istruzione `Inherits`, è possibile utilizzare l'interfaccia come se fosse una classe.  Nel codice riportato di seguito viene illustrato come creare un oggetto `Command` in un progetto che contiene un riferimento all'oggetto COM di Microsoft ActiveX Data Objects 2.8 Library:  
  
 [!code-vb[VbVbalrInterop#20](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_1.vb)]  
  
 Tuttavia, se si utilizza la classe COM come base per una classe derivata, è necessario utilizzare la classe di interoperabilità che rappresenta la classe COM, come nel codice seguente:  
  
 [!code-vb[VbVbalrInterop#21](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_2.vb)]  
  
> [!NOTE]
>  Gli assembly di interoperabilità implementano in modo implicito interfacce che rappresentano le classi COM.  Non tentare di utilizzare l'istruzione `Implements` per implementare tali interfacce. In caso contrario, verrà generato un errore.  
  
##  <a name="vbconinteroperabilitymarshalinganchor7"></a> Tipi di dati per parametri e valori restituiti  
 A differenza dei membri degli assembly standard, i membri degli assembly di interoperabilità possono includere tipi di dati diversi da quelli utilizzati nella dichiarazione originale dell'oggetto.  Anche se gli assembly di interoperabilità convertono in modo implicito i tipi COM in tipi di Common Language Runtime compatibili, è necessario verificare i tipi di dati utilizzati in entrambi i modelli, in modo da evitare errori di runtime.  Negli oggetti COM creati con Visual Basic 6.0 e versioni precedenti, ad esempio, con i valori di tipo `Integer` si presuppone il tipo equivalente di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], vale a dire `Short`.  Si consiglia di utilizzare il Visualizzatore oggetti per verificare le caratteristiche dei membri importati prima di utilizzarli.  
  
##  <a name="vbconinteroperabilitymarshalinganchor8"></a> Metodi COM a livello di modulo  
 Molti oggetti COM vengono utilizzati creando un'istanza di una classe COM utilizzando la parola chiave `New` e richiamando quindi i metodi dell'oggetto.  Un'eccezione a questa regola riguarda oggetti COM contenenti classi COM `AppObj` o `GlobalMultiUse`.  Tali classi assomigliano ai metodi a livello di modulo nelle classi [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)].  In Visual Basic 6.0 e versioni precedenti vengono create automaticamente e in modo implicito istanze di tali oggetti la prima volta che viene chiamato uno dei relativi metodi.  In Visual Basic 6.0 è possibile, ad esempio, aggiungere un riferimento a Microsoft DAO 3.6 Object Library e chiamare il metodo `DBEngine` senza prima creare un'istanza.  
  
```  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] richiede che le istanze di oggetti COM siano sempre create prima di poterne utilizzare i metodi.  Per utilizzare i metodi in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)], dichiarare una variabile della classe desiderata e utilizzare la nuova parola chiave per assegnare l'oggetto alla variabile oggetto.  La parola chiave `Shared` può essere utilizzata quando si desidera verificare che venga creata solo un'istanza della classe.  
  
 [!code-vb[VbVbalrInterop#23](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_3.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor9"></a> Errori non gestiti in gestori eventi  
 Uno dei problemi di interoperabilità più frequenti riguarda la presenza di errori in gestori eventi che gestiscono eventi generati da oggetti COM.  Questo tipo di errori viene ignorato a meno che non venga effettuato un controllo specifico degli errori mediante le istruzioni `On Error` o `Try...Catch...Finally`.  L'esempio riportato di seguito è tratto, a titolo esemplificativo, da un progetto [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] che include un riferimento all'oggetto COM di Microsoft ActiveX Data Objects 2.8 Library.  
  
 [!code-vb[VbVbalrInterop#24](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_4.vb)]  
  
 Nell'esempio viene generato un errore nel modo previsto.  Se tuttavia si tenta di eseguire lo stesso esempio senza il blocco `Try...Catch...Finally`, l'errore verrà ignorato come se fosse stata utilizzata l'istruzione `OnError Resume Next`.  Senza la gestione degli errori, la divisione per zero non riuscirà automaticamente.  Poiché questo tipo di errori non genera mai errori di eccezioni non gestite, è indispensabile che venga utilizzata qualche forma di gestione delle eccezioni nei gestori eventi che gestiscono eventi provenienti da oggetti COM.  
  
### Nozioni di base sugli errori di interoperabilità COM  
 Senza la gestione degli errori, le chiamate all'interoperabilità spesso generano errori che non contengono molte informazioni.  Quando possibile, utilizzare la gestione strutturata degli errori per fornire più informazioni sui problemi quando essi si verificano.  Ciò potrebbe risultare particolarmente utile quando si esegue il debug di applicazioni.  Di seguito è riportato un esempio:  
  
 [!code-vb[VbVbalrInterop#25](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_5.vb)]  
  
 È possibile reperire informazioni quali la descrizione dell'errore, HRESULT e l'origine di errori COM esaminando il contenuto dell'oggetto eccezione.  
  
##  <a name="vbconinteroperabilitymarshalinganchor10"></a> Problemi relativi ai controlli ActiveX  
 La maggior parte dei controlli ActiveX che funziona con Visual Basic 6.0 non presenta problemi con [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)].  Le eccezioni principali sono i controlli contenitore oppure i controlli che contengono in modo visivo altri controlli.  Di seguito sono riportati alcuni esempi di controlli meno recenti che non funzionano correttamente con [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]:  
  
-   Controllo Microsoft Forms 2.0 Frame  
  
-   Controllo di scorrimento, noto anche come casella di selezione  
  
-   Controllo struttura a schede Sheridan  
  
 Sono disponibili solo alcune soluzioni relative a problemi di controlli ActiveX non supportati.  È possibile eseguire la migrazione dei controlli esistenti in [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] se si è proprietari del codice sorgente originale.  In caso contrario, è possibile richiedere ai fornitori di software versioni dei controlli aggiornate compatibili con .NET per sostituire i controlli ActiveX non supportati.  
  
##  <a name="vbconinteroperabilitymarshalinganchor11"></a> Passaggio di proprietà in sola lettura di controlli ByRef  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] talvolta genera errori COM come "Error 0x800A017F CTL\_E\_SETNOTSUPPORTED" quando si passano proprietà `ReadOnly` di alcuni controlli ActiveX meno recenti come parametri `ByRef` ad altre routine.  Chiamate di routine simili da Visual Basic 6.0 non generano un errore e i parametri vengono considerati come se fossero stati passati per valore.  Il messaggio di errore visualizzato in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] è l'oggetto COM che indica che è in corso un tentativo di modifica di una proprietà che non dispone della routine `Set` della proprietà.  
  
 Se si dispone dell'accesso alla routine chiamata, è possibile impedire l'errore utilizzando la parola chiave `ByVal` per dichiarare parametri che accettano proprietà `ReadOnly`.  Di seguito è riportato un esempio:  
  
 [!code-vb[VbVbalrInterop#26](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_6.vb)]  
  
 Se non si dispone dell'accesso al codice sorgente relativo alla routine chiamata, è possibile imporre il passaggio per valore della proprietà aggiungendo una serie supplementare di parentesi per racchiudere la routine chiamante.  In un progetto che contiene un riferimento all'oggetto COM di Microsoft ActiveX Data Objects 2.8 Library, ad esempio, è possibile utilizzare:  
  
 [!code-vb[VbVbalrInterop#27](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_7.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor12"></a> Distribuzione di assembly con esposizione dell'interoperabilità  
 La distribuzione di assembly in cui vengono esposte interfacce COM presenta alcune problematiche esclusive.  Un potenziale problema può verificarsi, ad esempio, quando viene fatto riferimento allo stesso assembly COM da applicazioni separate.  Questa situazione si riscontra spesso quando si installa una nuova versione di un assembly e la versione precedente viene ancora utilizzata da un'altra applicazione.  La disinstallazione di un assembly che utilizza una DLL condivisa può determinarne accidentalmente la mancata disponibilità per gli altri assembly.  
  
 Per evitare questo problema, è opportuno installare gli assembly condivisi nella Global Assembly Cache e utilizzare un modulo unione per il componente.  Se non è possibile installare l'applicazione nella Global Assembly Cache, è opportuno eseguirne l'installazione in CommonFilesFolder in una sottodirectory specifica della versione.  
  
 È opportuno inserire gli assembly non condivisi nella stessa directory dell'applicazione chiamante.  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe \(Type Library Importer\)](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)   
 [Tlbexp.exe \(Type Library Exporter\)](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)   
 [Walkthrough: Implementing Inheritance with COM Objects](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Global Assembly Cache](../Topic/Global%20Assembly%20Cache.md)
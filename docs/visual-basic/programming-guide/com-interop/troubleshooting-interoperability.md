---
title: "Risoluzione dei problemi di interoperabilità (Visual Basic) | Documenti di Microsoft"
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
- interop, deploying assemblies
- assemblies [Visual Basic]
- interop, installing assemblies that share components
- COM objects, troubleshooting
- interop, sharing components
- troubleshooting interoperability
- interoperability, troubleshooting
- COM interop, troubleshooting
- assemblies [Visual Basic], deploying
- troubleshooting Visual Basic, interoperability
- interop assemblies
- interoperability, sharing components
- shared components, using with assemblies
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
caps.latest.revision: 21
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
ms.openlocfilehash: cbc37638ed5c57b94356c2d189f36b66202ceba5
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-interoperability-visual-basic"></a>Risoluzione dei problemi relativi all'interoperabilità (Visual Basic)
Durante l'interazione tra COM e il codice gestito del [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], è possibile riscontrare uno o più dei seguenti problemi comuni.  
  
##  <a name="vbconinteroperabilitymarshalinganchor1"></a>Marshalling di interoperabilità  
 In alcuni casi, potrebbe essere necessario utilizzare i tipi di dati che non sono in parte il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Gli assembly di interoperabilità gestiscono la maggior parte del lavoro per gli oggetti COM, ma potrebbe essere necessario controllare i tipi di dati che vengono utilizzati quando gli oggetti gestiti esposti a COM. Ad esempio, è necessario specificare le strutture nelle librerie di classi di `BStr` tipo nelle stringhe inviate a oggetti COM creati mediante Visual Basic 6.0 e versioni precedenti non gestito. In questi casi, è possibile utilizzare il <xref:System.Runtime.InteropServices.MarshalAsAttribute>attributo in modo tipi gestiti vengano esposti come tipi non gestiti.</xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
##  <a name="vbconinteroperabilitymarshalinganchor2"></a>Esportazione di stringhe a lunghezza fissa in codice non gestito  
 In Visual Basic 6.0 e versioni precedenti, le stringhe vengono esportate in oggetti COM come sequenze di byte senza un carattere di terminazione null. Per la compatibilità con altri linguaggi, [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] include un carattere di terminazione durante l'esportazione di stringhe. È il modo migliore per risolvere questo problema di incompatibilità per esportare le stringhe senza carattere di terminazione come matrici di `Byte` o `Char`.  
  
##  <a name="vbconinteroperabilitymarshalinganchor3"></a>L'esportazione delle gerarchie di ereditarietà  
 Gerarchie appiattire out quando esposti come oggetti COM di classe gestita. Ad esempio, se si definisce una classe base con un membro e quindi ereditare la classe di base in una classe derivata che viene esposto come un oggetto COM, i client che utilizzano la classe derivata dell'oggetto COM non sarà in grado di utilizzare i membri ereditati. Membri della classe base è possibile accedere da oggetti COM solo come istanze di una classe base e quindi solo se la classe di base viene inoltre creata come oggetto COM.  
  
## <a name="overloaded-methods"></a>Metodi di overload  
 Sebbene sia possibile creare metodi di overload con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], non sono supportate da COM. Quando una classe che contiene metodi di overload viene esposta come oggetto COM, vengono generati nuovi nomi per i metodi di overload.  
  
 Ad esempio, si consideri una classe che dispone di due overload di `Synch` metodo. Quando la classe viene esposta come oggetto COM, i nuovi nomi di metodo generato potrebbero essere `Synch` e `Synch_2`.  
  
 La ridenominazione può causare due problemi per i consumer dell'oggetto COM.  
  
1.  I client potrebbero non prevedere i nomi di metodo generato.  
  
2.  I nomi di metodo generato nella classe esposta come oggetto COM possono cambiare quando vengono aggiunti nuovi overload per la classe o la relativa classe base. Ciò può provocare problemi di controllo delle versioni.  
  
 Per risolvere entrambi i problemi, assegnare a ogni metodo di un nome univoco, anziché utilizzare l'overload, quando si sviluppano oggetti che verranno esposti come oggetti COM.  
  
##  <a name="vbconinteroperabilitymarshalinganchor4"></a>Utilizzo di oggetti COM tramite assembly di interoperabilità  
 Utilizzare assembly di interoperabilità come se fossero in sostituzione di codice gestito per gli oggetti COM che rappresentano. Tuttavia, poiché si tratta di wrapper e gli oggetti COM non effettivi, esistono alcune differenze tra l'utilizzo di assembly di interoperabilità e gli assembly standard. Le differenze includono l'esposizione di classi e tipi di dati per i parametri e valori restituiti.  
  
##  <a name="vbconinteroperabilitymarshalinganchor5"></a>Classi esposte come entrambe le interfacce e classi  
 A differenza delle classi in assembly standard, le classi COM vengono esposte nell'assembly di interoperabilità come un'interfaccia e una classe che rappresenta la classe COM. Il nome dell'interfaccia è identico a quello della classe COM. Il nome della classe di interoperabilità è uguale a quello della classe COM originale, ma con la parola "Classe" aggiunto. Ad esempio, si supponga di che avere un progetto con un riferimento a un assembly di interoperabilità per un oggetto COM. Se la classe COM è denominata `MyComClass`, IntelliSense e il Visualizzatore Mostra un'interfaccia denominata `MyComClass` e una classe denominata `MyComClassClass`.  
  
##  <a name="vbconinteroperabilitymarshalinganchor6"></a>Creazione di istanze di classi .NET Framework  
 In genere viene creata un'istanza di un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] usando il `New` istruzione con un nome di classe. Quando una classe COM rappresentata da un assembly di interoperabilità è un caso in cui è possibile utilizzare il `New` istruzione con un'interfaccia. A meno che non si utilizza la classe COM con un `Inherits` istruzione, è possibile utilizzare l'interfaccia come se fosse una classe. Il codice seguente viene illustrato come creare un `Command` oggetto in un progetto che contiene un riferimento all'oggetto Microsoft ActiveX Data oggetti 2.8 libreria COM:  
  
 [!code-vb[VbVbalrInterop&#20;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_1.vb)]  
  
 Tuttavia, se si utilizza la classe COM come base per una classe derivata, è necessario utilizzare la classe di interoperabilità che rappresenta la classe COM, come nel codice seguente:  
  
 [!code-vb[VbVbalrInterop numero&21;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_2.vb)]  
  
> [!NOTE]
>  Assembly di interoperabilità implementano in modo implicito interfacce che rappresentano classi COM. Non è consigliabile provare a utilizzare il `Implements` comporterà l'istruzione per implementare queste interfacce o un errore.  
  
##  <a name="vbconinteroperabilitymarshalinganchor7"></a>Tipi di dati per i parametri e valori restituiti  
 A differenza dei membri dell'assembly standard, i membri di assembly di interoperabilità possono includere tipi di dati che differiscono da quelli utilizzati nella dichiarazione dell'oggetto originale. Anche se gli assembly di interoperabilità convertono implicita dei tipi COM in tipi di common language runtime compatibili, è necessario prestare attenzione ai tipi di dati che vengono utilizzati da entrambi i lati per evitare errori di runtime. Ad esempio, negli oggetti COM creati in Visual Basic 6.0 e versioni precedenti, i valori di tipo `Integer` presuppongono il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] tipo equivalente, `Short`. È consigliabile che utilizzare il Visualizzatore oggetti per esaminare le caratteristiche dei membri importati prima di utilizzarli.  
  
##  <a name="vbconinteroperabilitymarshalinganchor8"></a>Metodi COM a livello di modulo  
 Molti oggetti COM vengono utilizzati creando un'istanza di una classe COM utilizzando il `New` (parola chiave) e quindi chiamando i metodi dell'oggetto. Un'eccezione a questa regola riguarda oggetti COM che contengono `AppObj` o `GlobalMultiUse` classi COM. Tali classi assomigliano ai metodi a livello di modulo in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] classi. Visual Basic 6.0 e versioni precedenti in modo implicito creano istanze di tali oggetti è la prima volta che viene chiamato uno dei relativi metodi. In Visual Basic 6.0, ad esempio, è possibile aggiungere un riferimento alla libreria oggetti Microsoft DAO 3.6 e chiamare il `DBEngine` metodo senza prima creare un'istanza:  
  
```  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]è necessario creare istanze di oggetti COM sempre prima di poter utilizzare i relativi metodi. Utilizzare questi metodi in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)], dichiarare una variabile della classe desiderata e utilizzare la parola chiave new per assegnare l'oggetto per la variabile oggetto. Il `Shared` parola chiave può essere utilizzata quando si desidera assicurarsi che viene creata solo un'istanza della classe.  
  
 [!code-vb[VbVbalrInterop&#23;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_3.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor9"></a>Errori non gestiti nei gestori eventi  
 Un problema di interoperabilità comune riguarda gli errori nei gestori eventi che gestiscono gli eventi generati da oggetti COM. Tali errori vengono ignorati a meno che non un controllo specifico degli errori utilizzando `On Error` o `Try...Catch...Finally` istruzioni. Ad esempio, l'esempio seguente è da un [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] progetto che contiene un riferimento all'oggetto Microsoft ActiveX Data oggetti 2.8 libreria COM.  
  
 [!code-vb[VbVbalrInterop&#24;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_4.vb)]  
  
 In questo esempio viene generato un errore nel modo previsto. Tuttavia, se si tenta dello stesso esempio senza il `Try...Catch...Finally` blocco, l'errore viene ignorato se è stato utilizzato il `OnError Resume Next` istruzione. Senza la gestione degli errori, la divisione per zero non riuscirà automaticamente. Poiché tali errori non generano mai errori di eccezione non gestita, è importante utilizzare qualche forma di gestione delle eccezioni nei gestori eventi che gestiscono gli eventi da oggetti COM.  
  
### <a name="understanding-com-interop-errors"></a>Informazioni sugli errori di interoperabilità COM  
 Senza la gestione degli errori, le chiamate all'interoperabilità spesso generano errori che forniscono informazioni insufficienti. Se possibile, utilizzare gestione per fornire ulteriori informazioni sui problemi quando si verificano errori strutturata. Può essere particolarmente utile quando si esegue il debug di applicazioni. Ad esempio:  
  
 [!code-vb[VbVbalrInterop&#25;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_5.vb)]  
  
 È possibile trovare informazioni quali la descrizione dell'errore, HRESULT e l'origine degli errori COM esaminando il contenuto dell'oggetto eccezione.  
  
##  <a name="vbconinteroperabilitymarshalinganchor10"></a>Problemi relativi al controllo ActiveX  
 Utilizzano la maggior parte dei controlli ActiveX che funzionano con Visual Basic 6.0 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] senza problemi. Le principali eccezioni sono controlli contenitore, o che visivamente contengono altri controlli. Alcuni esempi di controlli precedenti che non funzionano correttamente con [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] sono i seguenti:  
  
-   Controllo di Microsoft Forms 2.0 Frame  
  
-   Controllo di scorrimento, noto anche come il controllo di selezione  
  
-   Schede Sheridan  
  
 Sono disponibili solo alcune soluzioni per problemi di controlli ActiveX non supportati. È possibile migrare i controlli esistenti a [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] se si è proprietari del codice sorgente originale. In caso contrario, è possibile controllare con fornitori di software per l'aggiornamento. NET-compatibile con le versioni dei controlli per sostituire non supportati controlli ActiveX.  
  
##  <a name="vbconinteroperabilitymarshalinganchor11"></a>Passaggio di proprietà ReadOnly di controlli ByRef  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]talvolta genera errori COM, ad esempio "Error 0x800A017F CTL_E_SETNOTSUPPORTED" quando si passa `ReadOnly` le proprietà di alcuni controlli ActiveX meno recenti come `ByRef` parametri alle altre procedure. Chiamate di routine simili da Visual Basic 6.0 non generano un errore e i parametri vengono considerati come se passati per valore. Il messaggio di errore visualizzato in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] è l'oggetto COM che indica che si sta tentando di modificare una proprietà che non dispone di una proprietà `Set` procedura.  
  
 Se si dispone di accesso per la routine chiamata, è possibile impedire l'errore utilizzando il `ByVal` parola chiave per dichiarare i parametri che accettano `ReadOnly` proprietà. Ad esempio:  
  
 [!code-vb[&#26; VbVbalrInterop](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_6.vb)]  
  
 Se non si ha accesso al codice sorgente per la routine chiamata, è possibile forzare la proprietà può essere passato per valore mediante l'aggiunta di un set aggiuntivo di parentesi quadre intorno alla routine chiamante. In un progetto che contiene un riferimento all'oggetto Microsoft ActiveX Data oggetti 2.8 libreria COM, ad esempio, è possibile utilizzare:  
  
 [!code-vb[VbVbalrInterop&#27;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_7.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor12"></a>Distribuzione di assembly che espongono l'interoperabilità  
 Distribuzione di assembly che espongono interfacce COM presenta alcune difficoltà specifiche. Ad esempio, un potenziale problema si verifica quando applicazioni separate che fanno riferimento allo stesso assembly COM. Questa situazione è comune quando si installa una nuova versione di un assembly e un'altra applicazione utilizza ancora la versione precedente dell'assembly. Se si disinstalla un assembly che condivide una DLL, sarà possibile involontariamente renderla disponibile ad altri assembly.  
  
 Per evitare questo problema, è necessario installare gli assembly condivisi alla Global Assembly Cache (GAC) e utilizzare un modulo unione per il componente. Se non è possibile installare l'applicazione nella Global Assembly Cache, deve essere installato in CommonFilesFolder in una sottodirectory specifica della versione.  
  
 Gli assembly che non sono condivisi devono trovarsi side-by-side nella directory dell'applicazione chiamante.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute></xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Interoperabilità COM](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe (Type Library Importer)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)   
 [Tlbexp.exe (Type Library Exporter)](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)   
 [Procedura dettagliata: Implementazione dell'ereditarietà con gli oggetti COM](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Inherits (istruzione)](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Global Assembly Cache](http://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202)

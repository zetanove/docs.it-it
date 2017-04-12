---
title: Convenzioni di codifica di Visual Basic | Documenti di Microsoft
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
- coding conventions, Visual Basic
- examples [Visual Basic], coding conventions
- Visual Basic code, conventions
ms.assetid: c1df130b-fec6-49a5-becf-0a7e494a1d0f
caps.latest.revision: 48
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 5712f14d53b86552a0b82af38ecf579577ef3fa1
ms.lasthandoff: 03/13/2017

---
# <a name="visual-basic-coding-conventions"></a>Convenzioni di codifica di Visual Basic
Microsoft sviluppa esempi e documentazione che seguire le istruzioni in questo argomento. Se si seguono le stesse convenzioni di codifica, è possibile ottenere i seguenti vantaggi:  
  
-   Il codice avrà un aspetto coerente, in modo che chi legge possa concentrarsi meglio sul contenuto, non layout.  
  
-   Lettori di comprendere il codice più rapidamente poiché è possibile apportare presupposti basati sulle esperienze precedenti.  
  
-   È possibile copiare, modificare e gestire più facilmente il codice.  
  
-   Consente di assicurare che il codice viene illustrato "procedure consigliate" per Visual Basic.  
  
## <a name="naming-conventions"></a>Convenzioni di denominazione  
  
-   Per informazioni sulle linee guida per la denominazione, vedere [convenzioni di denominazione per](http://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3) argomento.  
  
-   Non utilizzare "My" o "my" come parte di un nome di variabile. Questa procedura crea confusione con il `My` oggetti.  
  
-   Non è necessario modificare i nomi degli oggetti nel codice generato automaticamente per adattare le linee guida.  
  
## <a name="layout-conventions"></a>Convenzioni di layout  
  
-   Inserire le schede come spazi e utilizzare rientri intelligenti con rientri di quattro spazi.  
  
-   Utilizzare **riformattazione del listato di codice (riformattazione) di** di riformattare il codice nell'editor di codice. Per ulteriori informazioni, vedere [opzioni, Editor di testo, base (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/options-text-editor-basic-visual-basic).  
  
-   Utilizzare solo un'istruzione per riga. Non utilizzare il carattere di separatore di riga (:) di Visual Basic.  
  
-   Evitare di utilizzare il carattere di continuazione di riga esplicita "_" a favore di continuazione di riga implicita ovunque il linguaggio consente.  
  
-   Utilizzare una sola dichiarazione per riga.  
  
-   Se **riformattazione del listato di codice (riformattazione) di** non righe di continuazione formato automaticamente, manualmente rientro continuazione righe di una tabulazione. Tuttavia, sempre sinistra-Allinea elementi in un elenco.  
  
    ```  
    a As Integer,  
    b As Integer  
    ```  
  
-   Aggiungere almeno una riga vuota tra le definizioni di metodo e proprietà.  
  
## <a name="commenting-conventions"></a>Convenzioni relative ai commenti  
  
-   Inserire i commenti su una riga separata anziché alla fine di una riga di codice.  
  
-   Avviare commento con una lettera maiuscola e fine commento con un punto.  
  
-   Inserire uno spazio tra i delimitatori di commento (') e il testo del commento.  
  
     [!code-vb[VbVbalrGuidelines n.&2;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_1.vb)]  
  
-   Non racchiudere i commenti con blocchi formattati di asterischi.  
  
## <a name="program-structure"></a>Struttura del programma  
  
-   Quando si utilizza il `Main` (metodo), utilizzare il costrutto predefinito per le nuove applicazioni console e `My` per gli argomenti della riga di comando.  
  
     [!code-vb[VbVbalrGuidelines n.&3;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_2.vb)]  
  
## <a name="language-guidelines"></a>Linee guida della lingua  
  
### <a name="string-data-type"></a>Tipo di dati String  
  
-   Per concatenare stringhe, utilizzare una e commerciale (&).  
  
     [!code-vb[VbVbalrGuidelines n.&4;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_3.vb)]  
  
-   Per accodare stringhe nei cicli, utilizzare il <xref:System.Text.StringBuilder>oggetto.</xref:System.Text.StringBuilder>  
  
     [!code-vb[VbVbalrGuidelines n.&5;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_4.vb)]  
  
### <a name="relaxed-delegates-in-event-handlers"></a>Delegati di tipo relaxed nei gestori eventi  
 Non qualificare in modo esplicito gli argomenti (oggetto ed EventArgs) ai gestori eventi. Se non si utilizza gli argomenti dell'evento che vengono passati a un evento (ad esempio mittente come oggetto, e come EventArgs), utilizzare i delegati di tipo relaxed e omettere gli argomenti dell'evento nel codice:  
  
 [!code-vb[VbVbalrGuidelines&#7;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_5.vb)]  
  
### <a name="unsigned-data-type"></a>Tipi di dati non firmati  
  
-   Utilizzare `Integer` anziché tipi non firmati, tranne quando sono necessari.  
  
### <a name="arrays"></a>Matrici  
  
-   Utilizzare la sintassi breve quando si inizializzano le matrici nella riga della dichiarazione. Ad esempio, utilizzare la sintassi seguente.  
  
     [!code-vb[VbVbalrGuidelines n.&8;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_6.vb)]  
  
     Non utilizzare la sintassi seguente.  
  
     [!code-vb[9 VbVbalrGuidelines](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_7.vb)]  
  
-   Inserire l'identificatore di matrice del tipo, non sulla variabile. Ad esempio, utilizzare la sintassi seguente:  
  
     [!code-vb[VbVbalrGuidelines&#11;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_8.vb)]  
  
     Non utilizzare la sintassi seguente:  
  
     [!code-vb[VbVbalrGuidelines&#10;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_9.vb)]  
  
-   Utilizzare la sintassi {} quando è necessario dichiarare e inizializzare matrici di tipi di dati di base. Ad esempio, utilizzare la sintassi seguente:  
  
     [!code-vb[VbVbalrGuidelines&#12;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_10.vb)]  
  
     Non utilizzare la sintassi seguente:  
  
     [!code-vb[13 VbVbalrGuidelines](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_11.vb)]  
  
### <a name="use-the-with-keyword"></a>Utilizzare la parola chiave  
 Quando si esegue una serie di chiamate a un oggetto, è consigliabile utilizzare il `With` (parola chiave):  
  
 [!code-vb[VbVbalrGuidelines&#15;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_12.vb)]  
  
### <a name="use-the-trycatch-and-using-statements-when-you-use-exception-handling"></a>Utilizzare l'istruzione Try... Catch e utilizzo di istruzioni quando si utilizza la gestione delle eccezioni  
 Non utilizzare `On Error Goto`.  
  
### <a name="use-the-isnot-keyword"></a>Utilizzare la parola chiave IsNot  
 Utilizzare il `IsNot` (parola chiave) anziché `Not...Is Nothing`.  
  
### <a name="new-keyword"></a>Parola chiave New  
  
-   Utilizzare l'istanziazione breve. Ad esempio, utilizzare la sintassi seguente:  
  
     [!code-vb[VbVbalrGuidelines numero&21;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_13.vb)]  
  
     La riga precedente è equivalente a questa:  
  
     [!code-vb[VbVbalrGuidelines&#22;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_14.vb)]  
  
-   Utilizzare gli inizializzatori di oggetto per i nuovi oggetti anziché il costruttore senza parametri:  
  
     [!code-vb[VbVbalrGuidelines&#23;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_15.vb)]  
  
### <a name="event-handling"></a>Gestione di eventi  
  
-   Utilizzare `Handles` anziché `AddHandler`:  
  
     [!code-vb[VbVbalrGuidelines&#24;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_16.vb)]  
  
-   Utilizzare `AddressOf`e non creare un'istanza del delegato in modo esplicito:  
  
     [!code-vb[VbVbalrGuidelines&#25;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_17.vb)]  
  
-   Quando si definisce un evento, utilizzare la sintassi breve e consentire al compilatore di definire il delegato:  
  
     [!code-vb[&#26; VbVbalrGuidelines](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_18.vb)]  
  
-   Verifica se un evento è `Nothing` (null) prima di chiamare il `RaiseEvent` metodo. `RaiseEvent`Cerca `Nothing` prima che venga generato l'evento.  
  
### <a name="using-shared-members"></a>Utilizzo di membri condivisi  
 Chiamare `Shared` membri utilizzando il nome della classe, non una variabile di istanza.  
  
### <a name="use-xml-literals"></a>Utilizzare valori letterali XML  
 Valori letterali XML semplificano le attività più comuni che si verificano quando si lavora con XML (ad esempio, query, trasformazione e caricamento). Quando si sviluppa con XML, attenersi alle seguenti indicazioni:  
  
-   Utilizzare valori letterali XML per creare documenti e frammenti anziché chiamare direttamente le API XML XML.  
  
-   Importare gli spazi dei nomi XML a livello di file o progetto in modo da sfruttare le ottimizzazioni delle prestazioni per i valori letterali XML.  
  
-   Utilizzare le proprietà axis XML per accedere agli elementi e attributi in un documento XML.  
  
-   Utilizzare le espressioni incorporate per includere i valori e creare XML da valori esistenti anziché utilizzare chiamate API, ad esempio il `Add` metodo:  
  
     [!code-vb[VbVbalrGuidelines&#27;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_19.vb)]  
  
### <a name="linq-queries"></a>Query LINQ  
  
-   Utilizzare nomi significativi per le variabili di query:  
  
     [!code-vb[28 VbVbalrGuidelines](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_20.vb)]  
  
-   Fornire nomi di elementi in una query per assicurarsi che i nomi di proprietà di tipi anonimi sono in modo corretto utilizzando la convenzione Pascal maiuscole e minuscole:  
  
     [!code-vb[VbVbalrGuidelines&#29;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_21.vb)]  
  
-   Rinominare le proprietà quando i nomi delle proprietà nel risultato potrebbero risultare ambigui. Ad esempio, se la query restituisce un nome cliente un ID ordine, rinominarle anziché lasciarli come `Name` e `ID` nel risultato:  
  
     [!code-vb[&#30; VbVbalrGuidelines](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_22.vb)]  
  
-   Utilizzare l'inferenza del tipo nella dichiarazione di variabili di query e variabili di intervallo:  
  
     [!code-vb[VbVbalrGuidelines&#31;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_23.vb)]  
  
-   Allineare le clausole di query sotto il `From` istruzione:  
  
     [!code-vb[VbVbalrGuidelines n.&32;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_24.vb)]  
  
-   Utilizzare `Where` clausole prima delle altre clausole di query in modo che successive clausole di query agiscano su set di dati filtrati:  
  
     [!code-vb[VbVbalrGuidelines n.&33;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_25.vb)]  
  
-   Utilizzare il `Join` clausola per definire in modo esplicito un'operazione di join anziché il `Where` clausola per definire in modo implicito un'operazione di join:  
  
     [!code-vb[VbVbalrGuidelines&#34;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_26.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Linee guida per la generazione di codice sicuro](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)

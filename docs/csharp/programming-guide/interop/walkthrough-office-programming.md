---
title: "Procedura dettagliata: programmazione di Office (C# e Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "programmazione Office [C#"
  - "programmazione Office [Visual Basic]"
  - "Office, programmazione in Visual Basic e C#"
ms.assetid: 519cff31-f80b-4f0e-a56b-26358d0f8c51
caps.latest.revision: 46
caps.handback.revision: 46
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura dettagliata: programmazione di Office (C# e Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vs_dev10_long](../../../csharp/programming-guide/interop/includes/vs_dev10_long_md.md)]sono state introdotte nuove funzionalità di C\# e Visual Basic che migliorano la programmazione di Microsoft Office.  A ogni linguaggio sono state aggiunte funzionalità già presenti nell'altro linguaggio.  
  
 Le nuove funzionalità di C\# includono gli argomenti denominati e facoltativi, i valori restituiti di tipo `dynamic` e, nella programmazione COM, la possibilità di omettere la parola chiave `ref` e di accedere alle proprietà indicizzate.  Le nuove funzionalità in Visual Basic includono le proprietà implementate automaticamente, le istruzioni nelle espressioni lambda e gli inizializzatori di raccolta.  
  
 Entrambi i linguaggi consentono di incorporare informazioni sul tipo, in modo da distribuire gli assembly che interagiscono con i componenti COM senza distribuire assembly di interoperabilità primari \(PIA\) al computer dell'utente.  Per altre informazioni, vedere [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
 In questa procedura dettagliata vengono illustrate le nuove funzionalità nel contesto della programmazione di Office, ma molti di essi sono utili anche nella programmazione generale.  Nella procedura dettagliata, si userà innanzitutto un componente aggiuntivo di Excel per creare una cartella di lavoro di Excel.  Si creerà quindi un documento di Word contenente un collegamento alla cartella di lavoro.  Infine, si noterà come la dipendenza di assembly di interoperabilità primario può essere attivata e disattivata.  
  
## Prerequisiti  
 Per completare questa procedura dettagliata è necessario aver installato Microsoft Office Excel 2013 \(o versione 2007 o versione successiva\) e Microsoft Office Word 2013 \(o versione 2007 o versione successiva\) nel computer.  
  
 Se si usa un sistema operativo precedente a [!INCLUDE[windowsver](../../../csharp/programming-guide/interop/includes/windowsver_md.md)], assicurarsi che [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] sia installato.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per impostare un componente aggiuntivo di Excel  
  
1.  Avviare Visual Studio.  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
3.  Nel riquadro **Modelli installati**, espandere **Visual Basic** o **Visual C\#**, espandere **Office** e quindi fare clic su **2013** \(o **2010** o **2007**\).  
  
4.  Nel riquadro **Modelli** selezionare 	**Componente aggiuntivo per Excel 2013** \(o **Componente aggiuntivo per Excel 2010** o **Componente aggiuntivo per Excel 2007**\).  
  
5.  Verificare che nella parte superiore del riquadro **Modelli** sia visualizzato **.NET Framework 4**, o una versione successiva, nel campo **Framework di destinazione**.  
  
6.  Se opportuno, digitare un nome per il progetto nel campo **Nome**.  
  
7.  Fare clic su **OK**.  
  
8.  Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
### Per aggiungere riferimenti  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto, quindi scegliere **Aggiungi riferimento**.  Viene visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
2.  Nella scheda **Assembly**, selezionare **Microsoft.Office.Interop.Excel**, versione 15.0.0.0 \(o versione 14.0.0.0 per Excel 2010 o versione 12.0.0.0 per Excel 2007\), nell'elenco **Nome componente**, quindi tenere premuto il tasto CTRL e selezionare **Microsoft.Office.Interop.Word**, versione 15.0.0.0 \(o versione 14.0.0.0 per Word 2010 o 12.0.0.0 per Word 2007\).  Se gli assembly non sono visibili, può essere necessario assicurarsi che siano installati e visualizzati \(vedere [Procedura: installare assembly di interoperabilità primari di Office](../Topic/How%20to:%20Install%20Office%20Primary%20Interop%20Assemblies.md)\)  
  
3.  Fare clic su **OK**.  
  
### Per aggiungere istruzioni Imports o le direttive using necessarie  
  
1.  In **Esplora soluzioni**, fare clic con il pulsante destro del mouse sui file **ThisAddIn.vb** o **ThisAddIn.cs** e quindi scegliere **Visualizza codice**.  
  
2.  Aggiungere le seguenti istruzioni `Imports` \(Visual Basic\) o direttive `using` \(C\#\) all'inizio del file di codice, se non sono già presenti.  
  
     [!code-cs[csOfficeWalkthrough#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_1.cs)]
     [!code-vb[csOfficeWalkthrough#1](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_1.vb)]  
  
### Per creare un elenco di conti correnti bancari  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto, fare clic su **Aggiungi** e quindi su **Classe**.  Denominare la classe Account.vb se si usa Visual Basic, Account.cs se si usa C\#.  Fare clic su **Aggiungi**.  
  
2.  Sostituire la definizione della classe `Account` con il codice seguente.  Le definizioni di classe usano le *proprietà implementate automaticamente*, una novità di Visual Basic in Visual Studio 2010.  Per altre informazioni, vedere [Auto\-Implemented Properties](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md).  
  
     [!code-cs[csOfficeWalkthrough#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_2.cs)]
     [!code-vb[csOfficeWalkthrough#2](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_2.vb)]  
  
3.  Per creare un elenco `bankAccounts` contenente due conti, aggiungere il seguente codice al metodo `ThisAddIn_Startup` nei file ThisAddIn.vb o ThisAddIn.cs.  Le dichiarazioni dell'elenco usano gli *inizializzatori di raccolta*, una novità di Visual Basic in Visual Studio 2010.  Per altre informazioni, vedere [Collection Initializers](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md).  
  
     [!code-cs[csOfficeWalkthrough#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_3.cs)]
     [!code-vb[csOfficeWalkthrough#3](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_3.vb)]  
  
### Per esportare dati in Excel  
  
1.  Nello stesso file, aggiungere il metodo seguente alla classe `ThisAddIn`.  Il metodo configura una cartella di lavoro di Excel e vi esporta i dati.  
  
     [!code-cs[csOfficeWalkthrough#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_4.cs)]
     [!code-vb[csOfficeWalkthrough#4](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_4.vb)]  
  
     In questo metodo vengono usati due nuove funzionalità di C\#.  Entrambe queste funzionalità sono già esistenti in Visual Basic.  
  
    -   Il metodo [Add](http://go.microsoft.com/fwlink/?LinkId=210910) ha un *parametro facoltativo* per specificare un modello particolare.  I parametri facoltativi, una novità di [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp_dev10_long_md.md)], consentono di omettere l'argomento per il parametro se si vuole usare il valore predefinito del parametro.  Poiché nessun argomento viene inviato nell'esempio precedente, `Add` usa il modello predefinito e crea una nuova cartella di lavoro.  L'istruzione equivalente nelle precedenti versioni di C\# richiede un argomento segnaposto: `excelApp.Workbooks.Add(Type.Missing)`.  
  
         Per altre informazioni, vedere [Argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md).  
  
    -   Le proprietà `Range` e `Offset` dell'oggetto [Range](http://go.microsoft.com/fwlink/?LinkId=210911) usano le funzionalità delle *proprietà indicizzate*.  Questa funzionalità consente di usare tali proprietà dai tipi COM con la tipica sintassi di C\# seguente.  Le proprietà indicizzate consentono anche di usare la proprietà `Value` dell'oggetto `Range`, eliminando la necessità di usare la proprietà `Value2`.  La proprietà `Value` è indicizzata, ma l'indice è facoltativo.  Nell'esempio seguente sono presenti sia argomenti facoltativi sia proprietà indicizzate.  
  
         [!code-cs[csOfficeWalkthrough#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_5.cs)]  
  
         Nelle versioni precedenti del linguaggio, è necessaria la seguente sintassi speciale.  
  
         [!code-cs[csOfficeWalkthrough#6](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_6.cs)]  
  
         Non è possibile creare proprietà indicizzate personalizzate.  La funzionalità supporta solo l'utilizzo di proprietà indicizzate esistenti.  
  
         Per altre informazioni, vedere [Procedura: utilizzare proprietà indicizzate nella programmazione dell'interoperabilità COM](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md).  
  
2.  Aggiungere il seguente codice alla fine di `DisplayInExcel` per regolare la larghezza delle colonne in modo da adattarle al contenuto.  
  
     [!code-cs[csOfficeWalkthrough#7](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_7.cs)]
     [!code-vb[csOfficeWalkthrough#7](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_7.vb)]  
  
     Queste aggiunte dimostrano un'altra nuova funzionalità di C\# 2010: considerare i valori `Object` restituiti dagli host COM, ad esempio Office, come se fossero di tipo [dynamic](../../../csharp/language-reference/keywords/dynamic.md).  Ciò avviene automaticamente quando l'opzione **Incorpora tipi di interoperabilità** è impostata sul valore predefinito, `True`, o allo stesso modo, quando si fa riferimento all'assembly con l'opzione del compilatore [\/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md).  Il tipo `dynamic` consente l'associazione tardiva, già disponibile in Visual Basic, ed evita il cast esplicito richiesto in Visual C\# 2008 e versioni precedenti del linguaggio.  
  
     Ad esempio, `excelApp.Columns[1]` restituisce un `Object` e `AutoFit` è un metodo [Range](http://go.microsoft.com/fwlink/?LinkId=210911) di Excel.  In assenza di `dynamic`, è necessario eseguire il cast dell'oggetto restituito da `excelApp.Columns[1]` come istanza di `Range` prima di chiamare il metodo `AutoFit`.  
  
     [!code-cs[csOfficeWalkthrough#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_8.cs)]  
  
     Per altre informazioni sull'incorporamento di tipi di interoperabilità, vedere le procedure "Per trovare il riferimento all'assembly di interoperabilità primari" e "Per ripristinare la dipendenza di assembly di interoperabilità primario" più avanti in questo argomento.  Per altre informazioni su `dynamic`, vedere [dynamic](../../../csharp/language-reference/keywords/dynamic.md) o [Utilizzo del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md).  
  
### Per richiamare DisplayInExcel  
  
1.  Aggiungere il codice seguente alla fine del metodo `ThisAddIn_StartUp`.  La chiamata a `DisplayInExcel` contiene due argomenti.  Il primo argomento è il nome dell'elenco di conti da elaborare.  Il secondo argomento è un'espressione lambda su più righe che definisce la modalità con cui i dati saranno elaborati.  I valori `ID` e `balance` per ogni conto vengono visualizzati in celle adiacenti e la riga viene visualizzata in rosso se il saldo è inferiore a zero.  Le espressioni lambda su più righe sono una nuova funzionalità di Visual Basic 2010.  Per altre informazioni, vedere [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
     [!code-cs[csOfficeWalkthrough#9](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_9.cs)]
     [!code-vb[csOfficeWalkthrough#9](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_9.vb)]  
  
2.  Premere F5 per eseguire il programma.  Viene visualizzato un foglio di lavoro di Excel che contiene i dati dei conti.  
  
### Per aggiungere un documento di Word  
  
1.  Aggiungere il seguente codice alla fine del metodo `ThisAddIn_StartUp` per creare un documento di Word contenente un collegamento alla cartella di lavoro di Excel.  
  
     [!code-cs[csOfficeWalkthrough#10](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_10.cs)]
     [!code-vb[csOfficeWalkthrough#10](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_10.vb)]  
  
     In questo codice vengono illustrate diverse nuove funzionalità di C\#: la possibilità di omettere la parola chiave `ref` nella programmazione COM, gli argomenti denominati e gli argomenti facoltativi.  Queste funzionalità sono già esistenti in Visual Basic.  Il metodo [PasteSpecial](http://go.microsoft.com/fwlink/?LinkId=147099) presenta sette parametri, ognuno dei quali è definito come parametro di riferimento facoltativo.  Prima di Visual C\# 2010, era necessario definire le variabili di oggetto da usare come argomenti per i sette parametri, anche quando non si aveva alcun valore significativo da inviare.  Gli argomenti denominati e facoltativi consentono di indicare i parametri a cui si vuol accedere per nome e di inviare argomenti solo a tali parametri.  In questo esempio, gli argomenti vengono inviati per indicare che deve essere creato un collegamento alla cartella di lavoro negli Appunti \(parametro `Link`\), e che il collegamento verrà visualizzato nel documento di Word come un'icona \(parametro `DisplayAsIcon`\).  Visual C\# 2010 consente anche di omettere la parola chiave `ref` per questi argomenti.  Confrontare il seguente segmento di codice da Visual C\# 2008 con la riga singola richiesta in Visual C\# 2010:  
  
     [!code-cs[csOfficeWalkthrough#11](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_11.cs)]  
  
### Per eseguire l'applicazione  
  
1.  Premere F5 per eseguire l'applicazione.  Excel viene avviato e viene visualizzata una tabella che contiene le informazioni dei due conti in `bankAccounts`.  Quindi verrà visualizzato un documento di Word contenente un collegamento alla tabella di Excel.  
  
### Per pulire il progetto completato  
  
1.  In Visual Studio, fare clic su **Pulisci soluzione** nel menu **Compila**.  In caso contrario, il componente aggiuntivo verrà eseguito ogni volta che si apre Excel nel computer.  
  
### Per trovare il riferimento all'assembly di interoperabilità primario  
  
1.  Eseguire nuovamente l'applicazione, ma non fare clic **Pulisci soluzione**.  
  
2.  Dal menu **Start** fare clic su **Tutti i programmi**.  Fare clic su **Microsoft Visual Studio 2013**, quindi su **Strumenti di Visual Studio**, quindi **Prompt dei comandi di Visual Studio \(2013\)**.  
  
3.  Digitare `ildasm` nella finestra del prompt dei comandi di Visual Studio \(2013\) e quindi premere INVIO.  Verrà visualizzata la finestra IL DASM.  
  
4.  Nel menu **File** della finestra IL DASM fare clic su **Apri**.  Fare doppio clic su **Visual Studio 2013** e quindi fare doppio clic su **Progetti**.  Aprire la cartella per il progetto e cercare nella cartella bin\/Debug il file *nome progetto*.dll.  Fare doppio clic su *nome progetto*.dll.  Una nuova finestra consente di visualizzare gli attributi del progetto, oltre ai riferimenti ad altri moduli e assembly.  Notare che gli spazi dei nomi `Microsoft.Office.Interop.Excel` e `Microsoft.Office.Interop.Word` sono inclusi nell'assembly.  Per impostazione predefinita in Visual Studio 2013, il compilatore importa i tipi necessari da un assembly di interoperabilità primario di cui viene fatto riferimento nell'assembly.  
  
     Per altre informazioni, vedere [Procedura: Visualizzare il contenuto dell'assembly](../Topic/How%20to:%20View%20Assembly%20Contents.md).  
  
5.  Fare doppio clic sull'icona **MANIFESTO**.  Viene visualizzata una finestra che include un elenco di assembly che contengono gli elementi a cui fa riferimento il progetto.  `Microsoft.Office.Interop.Excel` e `Microsoft.Office.Interop.Word` non sono inclusi nell'elenco.  Poiché i tipi che è necessario importare nell'assembly per il progetto, i riferimenti a un assembly di interoperabilità primario non sono necessari.  Ciò rende più semplice la distribuzione.  Gli assembly di interoperabilità primari non devono essere presenti nel computer dell'utente e, poiché un'applicazione non richiede la distribuzione di una versione specifica di un assembly di interoperabilità primario, è possibile progettare applicazioni compatibili con più versioni di Office, a condizione che le API necessarie siano presenti in tutte le versioni.  
  
     Poiché la distribuzione di assembly di interoperabilità primari non è più necessaria, è possibile creare un'applicazione in scenari avanzati che sia compatibile con più versioni di Office, incluse le versioni precedenti.  Tuttavia, questo metodo funziona solo se il codice non usa alcuna API che non sia disponibile nella versione di Office che si sta usando.  Non è sempre chiaro se una particolare API fosse disponibile in una versione precedente e per tale motivo l'utilizzo di versioni precedenti di Office non è consigliato.  
  
    > [!NOTE]
    >  Non sono stati pubblicati PIA prima di Office 2003.  Di conseguenza, l'unico modo per generare un assembly di interoperabilità per Office 2002 o versioni precedenti consiste nell'importare il riferimento COM.  
  
6.  Chiudere la finestra del manifesto e l'assembly.  
  
### Per ripristinare la dipendenza di assembly di interoperabilità primario  
  
1.  In **Esplora soluzioni**, fare clic su **Mostra tutti i file**.  Espandere la cartella **Riferimenti** e scegliere **Microsoft.Office.Interop.Excel**.  Premere F4 per visualizzare la finestra **Proprietà**.  
  
2.  Nella finestra **Proprietà**, impostare la proprietà **Incorpora tipi di interoperabilità** da **True** a **False**.  
  
3.  Ripetere i passaggi 1 e 2 di questa procedura per `Microsoft.Office.Interop.Word`.  
  
4.  In C\#, commentare le due chiamate `Autofit` alla fine del metodo `DisplayInExcel`.  
  
5.  Premere F5 per verificare che il progetto sia ancora eseguito correttamente.  
  
6.  Ripetere i passaggi da 1 a 3 della procedura precedente per aprire la finestra dell'assembly.  Notare che `Microsoft.Office.Interop.Word` e `Microsoft.Office.Interop.Excel` non sono più presenti nell'elenco di assembly incorporati.  
  
7.  Fare doppio clic sull'icona **MANIFESTO** e scorrere l'elenco degli assembly di riferimento.  Sia `Microsoft.Office.Interop.Word` sia `Microsoft.Office.Interop.Excel` sono inclusi nell'elenco.  Poiché l'applicazione fa riferimento a Excel e assembly di interoperabilità primari di Word e la proprietà **Incorpora tipi di interoperabilità** è impostata su **False**, entrambi gli assembly devono esistere nel computer dell'utente finale.  
  
8.  In Visual Studio, fare clic su **Pulisci soluzione** nel menu **Compila** per pulire il progetto completato.  
  
## Vedere anche  
 [Auto\-Implemented Properties](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)   
 [Collection Initializers](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [Optional Parameters](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Passing Arguments by Position and by Name](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [Early and Late Binding](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Utilizzo del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Procedura: utilizzare proprietà indicizzate nella programmazione dell'interoperabilità COM](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)   
 [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office](../Topic/Walkthrough:%20Embedding%20Type%20Information%20from%20Microsoft%20Office%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: creazione del primo componente aggiuntivo VSTO per Excel](../Topic/Walkthrough:%20Creating%20Your%20First%20VSTO%20Add-in%20for%20Excel.md)   
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Interoperabilità](../../../csharp/programming-guide/interop/interoperability.md)
---
title: Documentazione del codice con i commenti XML
description: Documentazione del codice
keywords: .NET, .NET Core
author: tsolarin
ms.author: wiwagn
ms.date: 02/14/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 8e75e317-4a55-45f2-a866-e76124171838
ms.translationtype: Human Translation
ms.sourcegitcommit: d91daf2005998d81609803982f5fc2c231fe7ad3
ms.openlocfilehash: 4e873d15ae2b2e7a475ea758678423f6ec3b14b3
ms.contentlocale: it-it
ms.lasthandoff: 05/16/2017

---

# <a name="documenting-your-code-with-xml-comments"></a>Documentazione del codice con i commenti XML

I commenti in formato documentazione XML sono commenti speciali, aggiunti alla definizione di ogni tipo o membro definito dall'utente. Sono speciali perché possono essere elaborati dal compilatore per generare un file di documentazione XML in fase di compilazione.
Il file XML generato dal compilatore può essere distribuito insieme agli assembly .NET in modo che Visual Studio e altri IDE possano usare IntelliSense per visualizzare informazioni rapide su tipi o membri. È anche possibile eseguire il file XML tramite strumenti, ad esempio [DocFX](https://dotnet.github.io/docfx/) e [Sandcastle](https://github.com/EWSoftware/SHFB) per generare i siti Web di riferimento all'API.

I commenti in formato documentazione XML, come tutti gli altri commenti, vengono ignorati dal compilatore.

È possibile generare il file XML in fase di compilazione eseguendo una delle operazioni seguenti:

- Se si sviluppa un'applicazione con .NET Core dalla riga di comando, è possibile aggiungere un [elemento DocumentationFile](http://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) alla sezione `<PropertyGroup>` del file di progetto csproj. L'esempio seguente genera un file XML nella directory del progetto con lo stesso nome file radice del progetto:

   ```xml
   <DocumentationFile>$(MSBuildProjectName).xml</DocumentationFile>
   ```

   È anche possibile specificare l'esatto percorso assoluto o relativo e il nome del file XML. L'esempio seguente genera il file XML nella stessa directory della versione di debug di un'applicazione:

    ```xml
   <DocumentationFile>bin\Debug\netcoreapp1.0\App.xml</DocumentationFile>
   ```

- Se si sviluppa un'applicazione tramite Visual Studio, fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà**. Nella finestra di dialogo Proprietà selezionare la scheda **Genera** e controllare **File di documentazione XML**. È anche possibile modificare il percorso in cui il compilatore scrive il file. 

- Se si sta compilando un'applicazione .NET Framework dalla riga di comando, aggiungere l'[opzione di compilazione /doc](language-reference/compiler-options/doc-compiler-option.md) durante la compilazione.  

I commenti in formato documentazione XML usano tre barre (`///`) e un corpo di commento in formato XML. Ad esempio:

[!code-csharp[Commento in formato documentazione XML](../../samples/snippets/csharp/concepts/codedoc/xml-comment.cs)]

## <a name="walkthrough"></a>Procedura dettagliata

In questa sezione viene illustrato come documentare una semplice libreria matematica per descrivere il meccanismo che gli sviluppatori possono usare.

Questo è il codice per la semplice libreria matematica:

[!code-csharp[Libreria di esempio](../../samples/snippets/csharp/concepts/codedoc/sample-library.cs)]

La libreria di esempio supporta quattro operazioni aritmetiche principali, ovvero `add`, `subtract`, `multiply` e `divide` su tipi di dati `int` e `double`.

Si vuole ora creare un documento di riferimento all'API dal codice per sviluppatori di terze parti che usano la libreria ma non hanno accesso al codice sorgente.
Come indicato precedentemente, è possibile usare i tag in formato documentazione XML per ottenere questo risultato. Verranno ora illustrati i tag XML standard supportati dal compilatore C#.

### <a name="ltsummarygt"></a>&lt;summary&gt;

Il tag `<summary>` aggiunge brevi informazioni su un tipo o membro.
Ne viene illustrato l'uso aggiungendolo alla definizione di classe `Math` e al primo metodo `Add`. È possibile applicarlo al resto del codice.

[!code-csharp[Tag summary](../../samples/snippets/csharp/concepts/codedoc/summary-tag.cs)]

Il tag `<summary>` è molto importante ed è consigliabile includerlo perché il suo contenuto è l'origine principale di informazioni sul tipo o sul membro in IntelliSense o in un documento di riferimento all'API.

### <a name="ltremarksgt"></a>&lt;remarks&gt;

Il tag `<remarks>` integra le informazioni sui tipi o membri definiti dal tag `<summary>`. In questo esempio, sarà sufficiente aggiungerlo alla classe.

[!code-csharp[Tag remarks](../../samples/snippets/csharp/concepts/codedoc/remarks-tag.cs)]

### <a name="ltreturnsgt"></a>&lt;returns&gt;

Il tag `<returns>` descrive il valore restituito di una dichiarazione di metodo.
Come in precedenza, nell'esempio seguente viene illustrato il tag `<returns>` nel primo metodo `Add`. È possibile eseguire questa operazione su altri metodi.

[!code-csharp[Tag returns](../../samples/snippets/csharp/concepts/codedoc/returns-tag.cs)]

### <a name="ltvaluegt"></a>&lt;value&gt;

Il tag `<value>` è simile al tag `<returns>`, ad eccezione del fatto che viene usato per le proprietà.
Se la libreria `Math` avesse una proprietà statica denominata `PI`, questo tag dovrebbe essere usato nel modo seguente:

[!code-csharp[Tag value](../../samples/snippets/csharp/concepts/codedoc/value-tag.cs)]

### <a name="ltexamplegt"></a>&lt;example&gt;

Si usa il tag `<example>` per includere un esempio nella documentazione XML.
Ciò comporta l'uso del tag `<code>` del figlio.

[!code-csharp[Tag example](../../samples/snippets/csharp/concepts/codedoc/example-tag.cs)]

Il tag `code` mantiene le interruzioni di riga e il rientro per esempi più lunghi.

### <a name="ltparagt"></a>&lt;para&gt;

Si usa il tag `<para>` per formattare il contenuto all'interno del tag padre. `<para>` viene in genere usato all'interno di un tag, ad esempio `<remarks>` o `<returns>`, per dividere il testo in paragrafi.
È possibile formattare il contenuto del tag `<remarks>` per la definizione delle classi.

[!code-csharp[Tag para](../../samples/snippets/csharp/concepts/codedoc/para-tag.cs)]

### <a name="ltcgt"></a>&lt;c&gt;

Nella formattazione si usa il tag `<c>` per contrassegnare parte del testo come codice.
È simile al tag `<code>`, ma è inline. È utile quando si vuole visualizzare un esempio breve di codice come parte del contenuto del tag.
Ora viene aggiornata la documentazione per la classe `Math`.

[!code-csharp[Tag C](../../samples/snippets/csharp/concepts/codedoc/c-tag.cs)]

### <a name="ltexceptiongt"></a>&lt;exception&gt;

Tramite il tag `<exception>` è possibile comunicare agli sviluppatori che un metodo può generare eccezioni specifiche.
Esaminando la libreria `Math`, è possibile vedere che entrambi i metodi `Add` generano un'eccezione se viene soddisfatta una determinata condizione. Nonostante non sia così ovvio, anche il metodo `Divide` integer genera eccezioni se il parametro `b` è uguale a zero. Aggiungere ora la documentazione sull'eccezione a questo metodo.

[!code-csharp[Tag exception](../../samples/snippets/csharp/concepts/codedoc/exception-tag.cs)]

L'attributo `cref` rappresenta un riferimento ad un'eccezione disponibile dall'ambiente di compilazione corrente.
Ciò può essere qualsiasi tipo definito nel progetto o in un assembly di riferimento. Il compilatore genererà un avviso se il relativo valore non può essere risolto.

### <a name="ltseegt"></a>&lt;see&gt;

Il tag `<see>` consente di creare un collegamento selezionabile per una pagina di documentazione per un altro elemento di codice. Nel prossimo esempio, verrà creato un collegamento selezionabile tra i due metodi `Add`.

[!code-csharp[Tag see](../../samples/snippets/csharp/concepts/codedoc/see-tag.cs)]

L'attributo `cref` è **obbligatorio** e rappresenta un riferimento a un tipo o al suo membro disponibile dall'ambiente di compilazione corrente. Ciò può essere qualsiasi tipo definito nel progetto o in un assembly di riferimento.

### <a name="ltseealsogt"></a>&lt;seealso&gt;

Il tag `<seealso>` si usa allo stesso modo del tag `<see>`. L'unica differenza è che il relativo contenuto viene in genere inserito in una sezione "Vedere anche". Di seguito si aggiungerà un tag `seealso` al metodo `Add` integer per fare riferimento ad altri metodi della classe che accettano parametri integer:

[!code-csharp[Tag seealso](../../samples/snippets/csharp/concepts/codedoc/seealso-tag.cs)]

L'attributo `cref` rappresenta un riferimento a un tipo o al suo membro disponibile dall'ambiente di compilazione corrente.
Ciò può essere qualsiasi tipo definito nel progetto o in un assembly di riferimento.

### <a name="ltparamgt"></a>&lt;param&gt;

Il tag `<param>` viene usato per descrivere i parametri del metodo. Di seguito viene illustrato un esempio sul metodo `Add` double. Il parametro descritto dal tag viene specificato nell'attributo `name` **obbligatorio**.

[!code-csharp[Tag param](../../samples/snippets/csharp/concepts/codedoc/param-tag.cs)]

### <a name="lttypeparamgt"></a>&lt;typeparam&gt;

Il tag `<typeparam>` viene usato allo stesso modo del tag `<param>`, ma in dichiarazioni di tipo o di metodo generico per descrivere un parametro generico.
Aggiungere un metodo generico semplice alla classe `Math` per verificare se una quantità è maggiore di un'altra.

[!code-csharp[Tag typeparam](../../samples/snippets/csharp/concepts/codedoc/typeparam-tag.cs)]

### <a name="ltparamrefgt"></a>&lt;paramref&gt;

A volte è possibile che durante la descrizione dell'operazione di un metodo in un tag `<summary>` si vuole fare un riferimento a un parametro. Il tag `<paramref>` è molto utile per questa operazione. Ora si aggiorna il riepilogo del metodo `Add` basato su double. Analogamente al tag `<param>`, il nome del parametro viene specificato nell'attributo `name` **obbligatorio**.

[!code-csharp[Tag paramref](../../samples/snippets/csharp/concepts/codedoc/paramref-tag.cs)]

### <a name="lttypeparamrefgt"></a>&lt;typeparamref&gt;

Il tag `<typeparamref>` viene usato allo stesso modo del tag `<paramref>`, ma in dichiarazioni di tipo o di metodo generico per descrivere un parametro generico.
È possibile usare lo stesso metodo generico creato in precedenza.

[!code-csharp[Tag typeparamref](../../samples/snippets/csharp/concepts/codedoc/typeparamref-tag.cs)]

### <a name="ltlistgt"></a>&lt;list&gt;

Il tag `<list>` viene usato per formattare le informazioni sulla documentazione come elenco ordinato, elenco non ordinato o tabella.
Creare un elenco non ordinato di ogni operazione matematica supportata dalla libreria `Math`.

[!code-csharp[Tag list](../../samples/snippets/csharp/concepts/codedoc/list-tag.cs)]

È possibile creare un elenco ordinato o una tabella sostituendo l'attributo `type` con `number` o `table` rispettivamente.

### <a name="putting-it-all-together"></a>Riassumendo

Dopo aver eseguito questa esercitazione e applicato i tag al codice, dove necessario, il codice dovrebbe ora essere simile al seguente:

[!code-csharp[Libreria con tag](../../samples/snippets/csharp/concepts/codedoc/tagged-library.cs)]

Dal codice, è possibile generare un sito Web di documentazione dettagliata completa di riferimenti incrociati. Ciò però potrebbe rendere il codice più difficile da leggere.
In quanto la presenza di un numero elevato di informazioni costituisce un problema molto serio per gli sviluppatori che vogliono contribuire al codice. Fortunatamente c'è un tag XML che consente di affrontare questo problema:

### <a name="ltincludegt"></a>&lt;include&gt;

Il tag `<include>` consente di fare riferimento ai commenti in un file XML separato che descrivono i tipi e i membri nel codice sorgente anziché inserire commenti in formato documentazione direttamente nel file del codice sorgente.

Ora si spostano tutti i tag XML in un file XML separato denominato `docs.xml`. È possibile assegnare al file un nome qualsiasi.

[!code-xml[Codice XML di esempio](../../samples/snippets/csharp/concepts/codedoc/include.xml)]

Nel codice XML precedente, i commenti in formato documentazione di ogni membro vengono visualizzati direttamente all'interno di un tag denominato dopo le operazioni eseguite. È possibile scegliere una strategia personalizzata. Ora che i commenti XML si trovano in un file separato, di seguito viene illustrato come il codice può essere reso più leggibile usando il tag `<include>`:

[!code-csharp[Tag include](../../samples/snippets/csharp/concepts/codedoc/include-tag.cs)]

Infine si avrà un codice di nuovo leggibile e nessuna informazione sulla documentazione è andata persa. 

L'attributo `filename` rappresenta il nome del file XML che contiene la documentazione.

L'attributo `path` rappresenta una query [XPath](https://msdn.microsoft.com/library/ms256115.aspx) nel presente `tag name` del `filename` specificato.

L'attributo `name` rappresenta l'identificatore di nome nel tag che precede i commenti.

L'attributo `id` che può essere usato al posto di `name` rappresenta l'ID per il tag che precede i commenti.

### <a name="user-defined-tags"></a>Tag definiti dall'utente

Tutti i tag specificati in precedenza rappresentano i tag riconosciuti dal compilatore C#. Gli utenti comunque possono definire tag personalizzati.
Alcuni strumenti, ad esempio Sandcastle, offrono supporto per altri tag, ad esempio [`<event>`](http://ewsoftware.github.io/XMLCommentsGuide/html/81bf7ad3-45dc-452f-90d5-87ce2494a182.htm), [`<note>`](http://ewsoftware.github.io/XMLCommentsGuide/html/4302a60f-e4f4-4b8d-a451-5f453c4ebd46.htm) e per [documentare gli spazi dei nomi](http://ewsoftware.github.io/XMLCommentsGuide/html/BD91FAD4-188D-4697-A654-7C07FD47EF31.htm).
Gli strumenti di creazione della documentazione interna o personalizzata possono anche essere usati con i tag standard e con più formati di output da HTML a PDF.

## <a name="recommendations"></a>Suggerimenti

La documentazione del codice è consigliabile per vari motivi. Di seguito vengono illustrate alcune procedure consigliate, scenari di uso generale e altre operazioni che è necessario conoscere quando si usano i tag in formato documentazione XML nel codice C#.

* Per mantenere una certa coerenza, tutti i tipi visibili pubblicamente e i loro membri devono essere documentati. Se necessario, è consigliabile eseguire un'operazione completa.
* I membri private possono anche essere documentati con commenti XML. Ciò espone tuttavia il funzionamento interno della libreria che potrebbe essere riservato.
* Il minimo necessario è che i tipi e i loro membri abbiano i tag `<summary>` perché il loro contenuto è necessario per IntelliSense.
* Il testo della documentazione deve essere scritto usando frasi complete che terminano con un punto.
* Le classi parziali sono completamente supportate e le informazioni sulla documentazione verranno concatenate in una singola voce per tale tipo.
* Il compilatore verifica la sintassi dei tag `<exception>`, `<include>`, `<param>`, `<see>`, `<seealso>` e `<typeparam>`.
- Il compilatore convalida i parametri che contengono i percorsi dei file e i riferimenti ad altre parti del codice.

## <a name="see-also"></a>Vedere anche
[Commenti in formato documentazione XML (Guida per programmatori C#)](programming-guide/xmldoc/xml-documentation-comments.md)

[Tag consigliati per i commenti della documentazione (Guida per programmatori C#)](programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)


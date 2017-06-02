---
title: "Creazione di file di risorse per applicazioni desktop | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "RESOURCES (file)"
  - "risorse delle applicazioni, creazione di file"
  - "file di risorse, RESOURCES (file)"
  - "file di risorse, creazione"
ms.assetid: 6c5ad891-66a0-4e7a-adcf-f41863ba6d8d
caps.latest.revision: 25
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 25
---
# Creazione di file di risorse per applicazioni desktop
È possibile includere risorse, ad esempio stringhe, immagini o dati oggetto, nei file di risorse per renderli facilmente disponibili all'applicazione.  .NET Framework offre cinque modi per creare i file di risorse:  
  
-   Creare un file di testo che contiene risorse di tipo stringa.  È possibile utilizzare il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per convertire il file di testo in un file di risorse binario, con estensione resources.  È possibile incorporare quindi il file di risorse binario in un eseguibile dell'applicazione o una libreria dell'applicazione tramite un compilatore del linguaggio oppure è possibile incorporarlo in un assembly satellite tramite [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md).  Per ulteriori informazioni, vedere la sezione [Risorse nei file di testo](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md#TextFiles).  
  
-   Creare un file di risorse XML, con estensione resx, che contiene dati di tipo stringa, immagine o oggetto.  È possibile utilizzare il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per convertire il file con estensione resx in un file di risorse binario, con estensione resources.  È possibile incorporare quindi il file di risorse binario in un eseguibile dell'applicazione o una libreria dell'applicazione tramite un compilatore del linguaggio oppure è possibile incorporarlo in un assembly satellite tramite [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md).  Per ulteriori informazioni, vedere la sezione [Risorse nei file con estensione resx](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md#ResxFiles).  
  
-   Creare un file di risorse XML, con estensione resx, a livello di codice utilizzando i tipi nello spazio dei nomi <xref:System.Resources>.  È possibile creare un file, con estensione resx, enumerarne le risorse e recuperare le risorse specifiche per nome.  Per ulteriori informazioni, vedere l'argomento [Uso dei file RESX a livello di codice](../../../docs/framework/resources/working-with-resx-files-programmatically.md).  
  
-   Creare un file di risorse binario, con estensione resources, a livello di codice.  È possibile incorporare quindi il file in un eseguibile dell'applicazione o una libreria dell'applicazione tramite un compilatore del linguaggio oppure è possibile incorporarlo in un assembly satellite tramite [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md).  Per ulteriori informazioni, vedere la sezione [Risorse nei file con estensione resources](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md#ResourcesFiles).  
  
-   Utilizzare Visual Studio per creare un file di risorse e includerlo nel progetto.  Visual Studio fornisce un editor di risorse che consente di aggiungere, eliminare e modificare le risorse.  In fase di compilazione, il file di risorse viene convertito automaticamente in un file binario con estensione resources e viene incorporato in un assembly dell'applicazione o un assembly satellite.  Per ulteriori informazioni, vedere la sezione [File di risorse in Visual Studio](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md#VSResFiles).  
  
<a name="TextFiles"></a>   
## Risorse nei file di testo  
 È possibile utilizzare file di testo \(.txt or .restext\) per archiviare solo risorse di tipo stringa; per le risorse non di tipo stringa, utilizzare file con estensione .resx o crearli a livello di codice.  I file di testo che contengono risorse di tipo stringa hanno il seguente formato:  
  
```  
# This is an optional comment.  
name = value  
  
; This is another optional comment.  
name = value  
  
; The following supports conditional compilation if X is defined.  
#ifdef X  
name1=value1  
name2=value2  
#endif  
  
# The following supports conditional compilation if Y is undefined.  
#if !Y  
name1=value1  
name2=value2  
#endif  
  
```  
  
 Il formato del file di risorse di file .txt e .restext è identico.  L'estensione .restext consente solo di rendere i file di testo immediatamente identificabili come file di risorse basati su testo.  
  
 Le risorse di tipo stringa appaiono come coppie *name\/value*, dove *name* è una stringa che identifica la risorsa e *value* è la stringa di risorsa restituita quando si passa *name* ad un metodo di recupero delle risorse, quale <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>.  *name* e *value* devono essere separati da un segno di uguale \(\=\).  Ad esempio:  
  
```  
  
FileMenuName=File  
EditMenuName=Edit  
ViewMenuName=View  
HelpMenuName=Help  
  
```  
  
> [!CAUTION]
>  Non utilizzare file di risorse per archiviare password, informazioni riservate o dati personali.  
  
 Le stringhe vuote \(ovvero una risorsa il cui valore è <xref:System.String.Empty?displayProperty=fullName>\) sono consentite nei file di testo.  Ad esempio:  
  
```  
EmptyString=  
```  
  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], i file di testo supportano la compilazione condizionale con `#ifdef` *symbol*...  `#endif` e `#if !`*symbol*...  `#endif` costrutti.  È quindi possibile utilizzare l'opzione `/define` con [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per definire i simboli.  Ogni risorsa richiede il proprio `#ifdef` *symbol*...  `#endif` o `#if !`*symbol*...  `#endif` costrutto.  Se si utilizza un'istruzione `#ifdef` e *symbol* è definito, la risorsa associata è inclusa nel file con estensione resources, in caso contrario, non è inclusa.  Se si utilizza un'istruzione `#if !` e *symbol* non è definito, la risorsa associata è inclusa nel file con estensione resources, in caso contrario, non è inclusa.  
  
 I commenti sono facoltativi nei file di testo e vengono preceduti da un punto e virgola \(;\) o da un simbolo cancelletto \(\#\) all'inizio di una riga.  È possibile posizionare le righe che contengono i commenti dovunque nel file.  I commenti non sono inclusi in un file con estensione .resources compilato che è stato creato utilizzando il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).  
  
 Ogni riga vuota nei file di testo viene considerata come uno spazio vuoto e viene ignorata.  
  
 Nell'esempio seguente vengono definite due risorse di tipo stringa denominate `OKButton` e `CancelButton`.  
  
```  
#Define resources for buttons in the user interface.  
OKButton=OK  
CancelButton=Cancel  
```  
  
 Se il file di testo contiene occorrenze duplicate di *name*, il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) visualizza un avviso e ignora il secondo nome.  
  
 *value* non può contenere caratteri di nuova riga, tuttavia è possibile utilizzare caratteri di escape di tipo C, quali `\n` per rappresentare una nuova riga e `\t` per rappresentare una tabulazione.  È anche possibile includere una barra rovesciata se viene utilizzato il carattere di escape \(ad esempio, "\\\\"\).  È inoltre possibile utilizzare una stringa vuota.  
  
 È necessario salvare le risorse in formato di file di testo tramite la codifica UTF\-8 o la codifica UTF\-16 nell'ordine dei byte little\-endian o big\-endian.  Tuttavia, per impostazione predefinita, il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) che converte un file con estensione txt in un file con estensione resources considera i file come UTF\-8.  Se si desidera che Resgen.exe riconosca un file codificato con UTF\-16, è necessario includere un BOM \(byte order mark\) Unicode \(U\+FEFF\) all'inizio del file.  
  
 Per incorporare un file di risorse in formato di testo in un assembly .NET Framework, è necessario convertire il file in un file di risorse binario, con estensione resources, utilizzando il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md),  È possibile incorporare quindi il file con estensione resources in un assembly .NET Framework utilizzando un compilatore del linguaggio oppure è possibile incorporarlo in un assembly satellite tramite [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md).  
  
 Nell'esempio seguente viene utilizzato un file di risorse in formato testo denominato GreetingResources.txt per un'applicazione console "Hello World" semplice.  Il file di testo definisce due stringhe, `prompt` e `greeting`, questo suggerisce all'utente di immettere il proprio nome e visualizzare un saluto.  
  
```  
# GreetingResources.txt   
# A resource file in text format for a "Hello World" application.  
#  
# Initial prompt to the user.  
prompt=Enter your name:   
# Format string to display the result.  
greeting=Hello, {0}!  
```  
  
 Il file di testo viene convertito in un file con estensione resources tramite il comando seguente:  
  
 **resgen GreetingResources.txt**  
  
 Nell'esempio seguente viene mostrato il codice sorgente per un'applicazione console che utilizza il file con estensione resources per visualizzare i messaggi all'utente.  
  
 [!code-csharp[Conceptual.Resources.TextFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.textfiles/cs/greeting.cs#1)]
 [!code-vb[Conceptual.Resources.TextFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.textfiles/vb/greeting.vb#1)]  
  
 Se si utilizza Visual Basic e il file di codice sorgente è denominato Greeting.vb, nel comando seguente viene creato un file eseguibile che include il file con estensione resources incorporato:  
  
 **vbc greeting.vb \/resource:GreetingResources.resources**  
  
 Se si sta utilizzando C\# e il file di codice sorgente è denominato Greeting.cs, il comando seguente crea un file eseguibile che include il file con estensione resources incorporato:  
  
 **csc greeting.cs \/resource:GreetingResources.resources**  
  
<a name="ResxFiles"></a>   
## Risorse nei file con estensione resx  
 A differenza dei file di testo che possono archiviare solo risorse di tipo stringa, i file di risorse XML con estensione resx possono archiviare stringhe, dati binari quali immagini, icone e clip audio e oggetti a livello di codice.  Un file con estensione resx contiene un'intestazione standard che descrive il formato delle voci di risorsa e specifica le informazioni del controllo delle versioni per l'XML utilizzato per l'analisi dei dati.  I dati del file di risorse seguono l'intestazione XML.  Ogni elemento di dati è costituito da una coppia nome\/valore contenuta nel tag `data`.  Il relativo attributo `name` definisce il nome risorsa e il tag `value` annidato contiene il valore della risorsa.  Per i dati di tipo stringa, il tag `value` contiene la stringa.  
  
 Ad esempio, il seguente tag `data` definisce una risorsa di tipo stringa denominata `prompt` il cui valore è "Immetti nome utente: ".  
  
```  
<data name="prompt" xml:space="preserve">  
  <value>Enter your name:</value>  
</data>  
```  
  
> [!WARNING]
>  Non utilizzare file di risorse per archiviare password, informazioni riservate o dati personali.  
  
 Per gli oggetti risorsa, il tag **data** include un attributo di `type` che indica il tipo di dati della risorsa.  Per gli oggetti costituiti da dati binari, il tag `data` include anche un attributo `mimetype` che indica il tipo di dati binari `base64`.  
  
> [!NOTE]
>  Tutti i file RESX utilizzano un formattatore di serializzazione binario per generare e analizzare i dati binari relativi a un tipo specifico.  Di conseguenza, un file RESX può perdere di validità se il formato di serializzazione binario di un oggetto diventa incompatibile.  
  
 Nell'esempio seguente viene mostrata una parte di un file con estensione resx che include una risorsa <xref:System.Int32> e un'immagine bitmap.  
  
```  
  
<data name="i1" type="System.Int32, mscorlib">  
  <value>20</value>  
</data>  
  
<data name="flag" type="System.Drawing.Bitmap, System.Drawing,     
    Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"   
    mimetype="application/x-microsoft.net.object.bytearray.base64">  
  <value>  
    AAEAAAD/////AQAAAAAAAAAMAgAAADtTeX…  
  </value>  
</data>  
```  
  
> [!IMPORTANT]
>  Poiché i file con estensione resx devono essere costituiti da un XML ben formato in un formato predefinito, non si consiglia di utilizzare i file con estensione resx manualmente, specialmente quando tali file contengono risorse diverse da quelle di tipo stringa.  Visual Studio invece fornisce un'interfaccia trasparente per la creazione e la modifica di file con estensione resx; per ulteriori informazioni, vedere la sezione [File di risorse in Visual Studio](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md#VSResFiles).  È possibile inoltre creare e modificare i file con estensione resx a livello di codice.  Per ulteriori informazioni, vedere [Uso dei file RESX a livello di codice](../../../docs/framework/resources/working-with-resx-files-programmatically.md).  
  
<a name="ResourcesFiles"></a>   
## Risorse nei file con estensione resources  
 È possibile utilizzare la classe <xref:System.Resources.ResourceWriter?displayProperty=fullName> per creare, a livello di codice, un file di risorse binario con estensione resources direttamente dal codice.  È possibile inoltre utilizzare il [Generatore di file di risorse \(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per creare un file con estensione resources da un file di testo o un file con estensione resx.  Il file con estensione resources può contenere dati binari \(matrici di byte\) e dati oggetto oltre a dati di tipo stringa.  Sono necessarie le seguenti operazioni per creare un file con estensione resources a livello di codice:  
  
1.  Creare un oggetto <xref:System.Resources.ResourceWriter> con un nome file univoco.  È possibile procedere specificando un nome file o un flusso di file a un costruttore di classe <xref:System.Resources.ResourceWriter>.  
  
2.  Chiamare uno degli overload del metodo <xref:System.Resources.ResourceWriter.AddResource%2A?displayProperty=fullName> per ogni risorsa denominata da aggiungere al file.  La risorsa può essere una stringa, un oggetto o una raccolta di dati binari \(una matrice di byte\).  
  
3.  Chiamare il metodo <xref:System.Resources.ResourceWriter.Close%2A?displayProperty=fullName> per scrivere le risorse nel file e chiudere l'oggetto <xref:System.Resources.ResourceWriter>.  
  
> [!NOTE]
>  Non utilizzare file di risorse per archiviare password, informazioni riservate o dati personali.  
  
 Nell'esempio seguente viene creato un file con estensione resources a livello di codice denominato CarResources.resources che archivia sei stringhe, un'icona e due oggetti definiti dall'applicazione \(due oggetti `Automobile`\).  Notare che la classe `Automobile` definita e di cui è stata creata un'istanza nell'esempio, viene contrassegnata con l'attributo <xref:System.SerializableAttribute> che consente che sia resa persistente dal formattatore della serializzazione binaria.  
  
 [!code-csharp[Conceptual.Resources.Resources#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resources/cs/resources1.cs#1)]
 [!code-vb[Conceptual.Resources.Resources#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resources/vb/resources1.vb#1)]  
  
 Dopo aver creato il file con estensione resources, è possibile incorporarlo in un eseguibile di runtime o in una libreria, includendo l'opzione `/resource` del compilatore del linguaggio, oppure in un assembly satellite tramite [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md).  
  
<a name="VSResFiles"></a>   
## File di risorse in Visual Studio  
 Quando si aggiunge un file di risorse a un progetto di Visual Studio, in Visual Studio viene creato un file con estensione resx nella directory del progetto.  In Visual Studio vengono forniti editor di risorse che consentono di aggiungere stringhe, immagini e oggetti binari.  Poiché gli editor vengono progettati per gestire solo dati statici, non possono essere utilizzati per archiviare oggetti a livello di codice; è necessario scrivere i dati oggetto in un file con estensione resx o resources a livello di codice.  Vedere l'argomento [Uso dei file RESX a livello di codice](../../../docs/framework/resources/working-with-resx-files-programmatically.md) e la sezione [Risorse nei file con estensione resources](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md#ResourcesFiles) per maggiori informazioni.  
  
 Se si stanno aggiungendo risorse localizzate, è necessario attribuirgli lo stesso nome file radice del file di risorse principale ed è inoltre necessario definire le impostazioni cultura nel nome file.  Ad esempio, se si aggiunge un file di risorse denominato Resources.resx, si potrebbero creare anche i file di risorse denominati Resources.en\-US.resx e Resources.fr\-FR.resx per mantenere le risorse localizzate per le impostazioni cultura inglesi \(Stati Uniti\) e francesi \(Francia\), rispettivamente.  È necessario definire anche le impostazioni cultura predefinite della propria applicazione.  Si tratta delle impostazioni cultura le cui risorse sono utilizzate se non è possibile trovare le risorse localizzate per impostazioni cultura particolari.  Per specificare le impostazioni cultura predefinite, in Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sul nome del progetto, scegliere Applicazione, fare clic su **Informazioni assembly** e selezionare il linguaggio o le impostazioni cultura appropriate all'elenco **Lingua di sistema**.  
  
 In fase di compilazione, Visual Studio prima converte i file con estensione resx di un progetto in file di risorse binari con estensione resources e li archivia in una sottodirectory della directory obj del progetto.  Visual Studio incorpora ogni file di risorse che non contiene risorse localizzate nell'assembly principale generato dal progetto.  Se tutti i file di risorse contengono risorse localizzate, Visual Studio li incorpora in assembly satellite separati per ogni impostazione cultura localizzata.  Archivia quindi ogni assembly satellite in una directory il cui nome corrisponde alle impostazioni cultura localizzate.  Ad esempio, le risorse dell'inglese localizzato \(Stati Uniti\) vengono archiviate in un assembly satellite nella sottodirectory en\-US.  
  
## Vedere anche  
 <xref:System.Resources>   
 [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md)   
 [Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)
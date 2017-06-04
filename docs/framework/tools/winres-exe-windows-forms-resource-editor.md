---
title: "Winres.exe (Windows Forms Resource Editor) | Microsoft Docs"
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
  - "Winres.exe"
  - "Windows Forms Resource Editor"
  - "localization"
  - "Windows Forms, localization"
  - "forms, localizing"
  - "resx files"
  - ".resx files"
ms.assetid: cb8bc835-9221-4888-af53-1a4f5fad6c48
caps.latest.revision: 23
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 23
---
# Winres.exe (Windows Forms Resource Editor)
Winres.exe, l'editor di risorse di Windows Form, è uno strumento di layout visivo appositamente studiato per facilitare la localizzazione delle risorse dell'interfaccia utente di Windows Form usate dai form.  I file .resx o .resources usati come input per Winres.exe possono essere creati mediante un ambiente di progettazione visiva quale Microsoft Visual Studio.  Per informazioni sulla distribuzione delle risorse in applicazioni .NET Framework, vedere [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md).  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
winres resourceFile   
winres /?   
```  
  
## Note  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|`resourceFile`|File di risorse da localizzare.  Deve essere un form di Windows Form con estensione .resx o .resources generato dalla finestra di progettazione di Visual Studio.  Winres.exe non è in grado di aprire file .resx o .resources generici.|  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
 Lo stato degli elementi dell'interfaccia utente di un form in un progetto Windows Form viene in genere archiviato nei file di risorse, che possono essere file basati su XML con estensione .resx oppure le corrispondenti versioni binarie compilate con estensione .resources.  Winres.exe fornisce funzionalità di modifica limitate per questi tipi di file all'esterno dell'ambiente di progettazione Visual Studio.  In particolare, consente i seguenti tipi di operazioni di modifica:  
  
-   È possibile modificare un file di risorse di impostazioni cultura specifiche o indipendente da tali impostazioni per cambiare le proprietà di interfaccia utente del form o dei relativi controlli, ad esempio il testo, le dimensioni o la posizione.  
  
-   È possibile generare i file di risorse di impostazioni cultura specifiche o indipendenti da tali impostazioni a partire dal file di risorse predefinito.  
  
-   Un file di risorse di determinate impostazioni cultura può essere salvato come file di risorse per altre impostazioni cultura.  Un file di risorse per l'inglese può ad esempio essere salvato come file di risorse per il polacco.  Il nuovo file viene in genere successivamente modificato in modo da essere compatibile con le nuove impostazioni cultura.  
  
 Vedere anche [Organizzazione gerarchica di risorse per la localizzazione](http://msdn.microsoft.com/library/756hydy4\(v=vs.110\)) o [Organizzazione gerarchica di risorse per la localizzazione](http://msdn.microsoft.com/library/756hydy4\(v=vs.120\)).  
  
 Non è possibile usare Winres.exe per convertire un file .resx nel file .resources corrispondente. Per effettuare questa operazione, usare lo strumento Resgen.exe.  Per altre informazioni, vedere [Resgen.exe \(Resource File Generator\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).  
  
 Winres.exe è un'applicazione grafica che consente di ricreare una versione della fase di progettazione di un form di Windows Form solo dal file di risorse, senza accedere al codice sorgente.  Winres.exe ospita la finestra delle proprietà e la finestra di progettazione Windows Form di Visual Studio.  Queste funzionalità consentono di modificare visivamente un file .resources o .resx contenente un form di Windows Form.  Winres.exe viene in genere usato per modificare le etichette, la posizione e le dimensioni dei controlli durante la fase di localizzazione dell'applicazione, per consentire la corretta visualizzazione delle etichette in base alle impostazioni cultura di destinazione.  
  
 Se Winres.exe non è in grado di risolvere il tipo di un controllo, nel file RESX o RESOURCES localizzato verrà creato un controllo segnaposto  che verrà visualizzato nel form di Windows Form sotto forma di finestra tratteggiata,  con dimensioni e posizione identiche a quelle del controllo reale.  Nella finestra delle proprietà sono visualizzate tutte le proprietà localizzabili disponibili per il controllo segnaposto.  Le eventuali modifiche apportate al controllo segnaposto vengono salvate per il controllo reale.  
  
## Confronto tra Winres.exe e Visual Studio  
 Prima di iniziare la localizzazione dei form di Windows Form per un'applicazione, è opportuno decidere se usare come strumento di localizzazione Visual Studio oppure Winres.exe.  La compatibilità tra versioni, come illustrato di seguito, può infatti impedire di passare da uno strumento all'altro.  
  
 Visual Studio presenta il vantaggio di poter essere usato sia per lo sviluppo che per la localizzazione di un'applicazione.  Per localizzare un form al termine della fase di sviluppo, impostare il valore di <xref:System.ComponentModel.LocalizableAttribute> del form \(corrispondente alla proprietà **Localizable** nell'editor delle proprietà\) su `true` e modificare la proprietà **Language** specificando le impostazioni cultura di destinazione desiderate.  Modificare quindi le stringhe, nonché la posizione e le dimensioni dei controlli, in base alle stringhe delle impostazioni cultura di destinazione.  Al momento del salvataggio del file .resx localizzato, nel file verranno scritte solo le proprietà localizzabili, ossia quelle che sono variate in base alle impostazioni cultura di destinazione.  Verrà inoltre creato automaticamente un assembly satellite per il file .resx localizzato nella directory appropriata.  Vedere anche [Procedura dettagliata: Localizzazione di Windows Form](http://msdn.microsoft.com/library/y99d1cd3\(v=vs.110\))  
  
 Anche se Visual Studio fornisce un ambiente integrato per lo sviluppo e la localizzazione, si consiglia di usare Winres.exe se il processo di localizzazione viene eseguito da terze parti.  Essendo uno specifico strumento di localizzazione, Winres.exe consente di distinguere più chiaramente il codice dell'applicazione dai form da localizzare e risulta quindi più funzionale per la gestione di progetti di grandi dimensioni.  
  
## Uso di Winres.exe  
 Per poter essere localizzata con Winres.exe, l'applicazione deve essere sviluppata con una finestra di progettazione visiva come Progettazione Windows Form in Visual Studio.  Al termine della fase di sviluppo, impostare il valore di <xref:System.ComponentModel.LocalizableAttribute> del form \(corrispondente alla proprietà **Localizable** nell'editor delle proprietà\) su `true`, quindi passare al team di localizzazione il file .resx per le impostazioni cultura predefinite.  Questo file contiene informazioni aggiuntive che consentono a Winres.exe di ricreare una versione della fase di progettazione del form originale.  
  
> [!CAUTION]
>  Winres.exe non può essere usato per modificare il file di risorse predefinito.  Tutte le proprietà modificate vengono interpretate come proprietà localizzate e salvate nel file di risorse delle impostazioni cultura di destinazione.  
  
 Le versioni finali dei file di risorse delle impostazioni cultura possono essere usate per creare le versioni localizzate dell'applicazione.  Per altre informazioni, vedere [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md).  
  
 Nella versione 2.0 di Winres.exe sono disponibili le seguenti funzionalità:  
  
-   Winres può essere eseguito in modalità file unico o in modalità file di Visual Studio.  La prima è la modalità legacy in base alla quale informazioni complete sul form e sul suo contenuto vengono archiviate nel file di risorse.  Con la seconda, invece, nel file di risorse vengono archiviate solo le modifiche relative alle impostazioni cultura.  
  
-   All'interfaccia è stata aggiunta una finestra di segnalazione degli errori, ancorata nell'area in basso a sinistra della finestra principale.  
  
-   È possibile verificare se sono presenti tasti di scelta duplicati scegliendo **Controlla tasti di scelta** dal menu Formato.  
  
## Compatibilità tra versioni  
 Poiché il formato dei file di risorse è stato aggiornato tra Visual Studio .NET 2002 e Visual Studio 2005, anche Winres.exe è stato modificato per motivi di compatibilità.  Pertanto, come regola generale si consiglia di usare la versione di Winres.exe rilasciata con la versione di .NET Framework usata per la creazione dell'applicazione.  Nella tabella riportata di seguito sono elencate le versioni compatibili.  
  
|Visual Studio|.NET Framework|Winres.exe|  
|-------------------|--------------------|----------------|  
|Visual Studio .NET 2002|1.0|1.0|  
|Visual Studio .NET 2003|1.1|1.1|  
|Visual Studio 2005|2.0|2.0|  
|Visual Studio 2008|3.0 e 3.5|3.0 e 3.5|  
|Visual Studio 2010|4.0|4.0|  
  
 Se si tenta di aprire un file di risorse meno recente con la versione 2.0 di Winres.exe, verrà chiesto di aggiornare il formato del file in modo che sia compatibile con la versione 2.0 di .NET Framework.  
  
 Nelle versioni di .NET Framework precedenti alla 2.0, i file di risorse \(specifici delle impostazioni cultura e indipendenti dalle impostazioni cultura\) creati con Winres.exe e con Progettazione form di Visual Studio erano incompatibili.  Una volta avviato il processo di localizzazione, era quindi necessario continuare a usare lo stesso strumento.  Con la versione 2.0 di Winres.exe è stata aggiunta la modalità file di Visual Studio,  che consente di salvare un file di risorse in modo da poter essere modificato con entrambi gli strumenti.  
  
> [!NOTE]
>  Pur offrendo il vantaggio della compatibilità con Visual Studio, la modalità file di Visual Studio consente di archiviare solo i valori modificati nel file di risorse. È pertanto necessario che i file padre del file di risorse corrente si trovino nella stessa directory.  Ad esempio, per modificare `TestApp.de-DE.resources`, un file di risorse per la lingua tedesca in Germania, è necessario disporre del file di risorse predefinito, `TestApp.resx`, ed eventualmente anche del file di risorse indipendente dalle impostazioni cultura, ossia `TestApp.de.resources`.  
  
## Esempi  
  
#### Per localizzare un file .resx o .resources associato a un form  
  
1.  Per eseguire Winres.exe, al prompt dei comandi per gli sviluppatori digitare `winres`.  
  
2.  Per aprire il file di risorse predefinito relativo a un form da localizzare, scegliere il comando **Apri** dal menu **File** e selezionare il file desiderato.  
  
     \-oppure\-  
  
     All'avvio di Winres.exe, specificare il file da aprire dalla riga di comando.  
  
     Il seguente comando avvia Winres.exe e carica il form associato a `TestApp.resx` in Progettazione Form.  
  
    ```  
    winres TestApp.resx  
    ```  
  
     Il seguente comando avvia Winres.exe e carica il form associato a `TestApp.resources` in Progettazione Form.  
  
    ```  
    winres TestApp.resources  
    ```  
  
    > [!NOTE]
    >  Se il form di cui si modificano le risorse è un form ereditato, l'assembly contenuto nel form ereditato e quello incluso nel form di derivazione devono essere entrambi registrati nella Global Assembly Cache \(GAC\) oppure devono trovarsi nella stessa directory di WinRes.exe.  Per altre informazioni sull'installazione dei componenti di .NET Framework nella GAC, vedere [Global Assembly Cache](../../../docs/framework/app-domains/gac.md).  
  
3.  Selezionare i controlli nel form e modificarne la proprietà <xref:System.Windows.Forms.Control.Text%2A> e le altre proprietà in base alla lingua e alle impostazioni cultura di destinazione.  Spostare o ridimensionare i controlli in base al testo localizzato.  
  
4.  Per salvare la versione localizzata del file .resx o .resources, fare clic sull'icona **Salva** o scegliere il comando corrispondente dal menu **File**.  Verrà visualizzata la finestra **Seleziona impostazioni cultura**.  
  
5.  Selezionare le impostazioni cultura e la modalità file appropriate, quindi scegliere **OK**.  Il file verrà salvato secondo le convenzioni di denominazione previste per i file di risorse localizzati.  Se si localizza, ad esempio, il file `TestApp.resources` per la lingua tedesca in Germania, il file verrà salvato come `TestApp.de-DE.resources`.  Se si localizza `TestApp.resx` per la lingua tedesca in Germania, il file verrà salvato come `TestApp.de-DE.resx`.  Per altre informazioni sulle convenzioni di denominazione dei file di risorse, vedere [Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  Per un elenco dei nomi di impostazioni cultura predefiniti usati dal runtime, vedere la [classe CultureInfo](https://msdn.microsoft.com/en-us/library/system.globalization.cultureinfo.aspx).  
  
## Vedere anche  
 <xref:System.ComponentModel.LocalizableAttribute>   
 <xref:System.Globalization.CultureInfo>   
 <xref:System.Resources.ResourceManager>   
 <xref:System.Resources.ResourceReader>   
 <xref:System.Resources.ResourceWriter>   
 [Tools](../../../docs/framework/tools/index.md)   
 [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md)   
 [Globalizzazione e localizzazione](../../../docs/standard/globalization-localization/index.md)
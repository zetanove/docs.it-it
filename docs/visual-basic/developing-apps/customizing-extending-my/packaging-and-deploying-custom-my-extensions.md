---
title: "Packaging and Deploying Custom My Extensions (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "My namespace, customizing"
  - "My namespace"
  - "My namespace, extending"
ms.assetid: fd89c54b-0290-4c50-95a3-ff17d4487a21
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Packaging and Deploying Custom My Extensions (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Visual Basic fornisce un modo semplice per distribuire le estensioni personalizzate dello spazio dei nomi `My` utilizzando modelli di Visual Studio.  Se si sta creando un modello di progetto per il quale le estensioni `My` fanno parte integrante del nuovo tipo di progetto, è possibile includere il codice delle estensioni personalizzate `My` con il progetto quando si esporta il modello.  Per ulteriori informazioni sull'esportazione dei moduli di progetto, vedere [Procedura: creare modelli di progetto](../Topic/How%20to:%20Create%20Project%20Templates.md).  
  
 Se l'estensione personalizzata `My` è in un solo file di codice, è possibile esportare il file come modello di elemento che gli utenti possono aggiungere a qualsiasi tipo di progetto di Visual Basic.  È quindi possibile personalizzare il modello di elemento per abilitare funzionalità e comportamento ulteriori per l'estensione personalizzata `My` in un progetto di Visual Basic.  Tali funzionalità permettono di:  
  
-   Abilitare gli utenti a gestire l'estensione personalizzata `My` dalla pagina **Estensioni My** di Progettazione progetti di Visual Basic.  
  
-   Aggiungere automaticamente l'estensione personalizzata `My` quando un riferimento a un assembly specificato viene aggiunto a un progetto.  
  
-   Nascondere il modello di elemento dell'estensione `My` nella finestra di dialogo **Aggiungi elemento** in modo che non venga incluso nell'elenco degli elementi di progetto.  
  
 In questo argomento viene illustrato come assemblare un'estensione personalizzata `My` come un modello di elemento nascosto che può essere gestito dalla pagina **Estensioni My** di Progettazione progetti di Visual Basic.  L'estensione personalizzata `My` può inoltre essere aggiunta automaticamente quando un riferimento a un assembly specificato viene aggiunto a un progetto.  
  
## Creare un'estensione dello spazio dei nomi My  
 Il primo passaggio per creare un pacchetto di distribuzione per un'estensione personalizzata `My` consiste nel creare l'estensione come un singolo file di codice.  Per dettagli e istruzione sulla creazione di un'estensione personalizzata `My`, vedere [Extending the My Namespace in Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md).  
  
## Esportare un'estensione dello spazio dei nomi My come modello di elemento  
 Una volta creato un file di codice che includa l'estensione dello spazio dei nomi `My`, è possibile esportare il file di codice come modello di elemento di Visual Studio.  Per istruzioni sull'esportazione di un file come modello di elemento di Visual Studio, vedere [Procedura: creare modelli di elementi](../Topic/How%20to:%20Create%20Item%20Templates.md).  
  
> [!NOTE]
>  Se l'estensione dello spazio dei nomi `My` ha una dipendenza su un particolare assembly, è possibile personalizzare il modello di elemento per installare automaticamente l'estensione dello spazio dei nomi `My` quando viene aggiunto un riferimento a quell'assembly.  Di conseguenza, sarà opportuno escludere quel riferimento all'assembly quando si esporta il file di codice come modello di elemento di Visual Studio.  
  
## Personalizzare il modello di elemento  
 È possibile abilitare la gestione del modello di elemento dalla pagina **Estensioni My** di Progettazione progetti di Visual Basic.  Inoltre, è possibile abilitare l'aggiunta automatica del modello di elemento quando a un progetto viene aggiunto un riferimento all'assembly specificato.  Per attivare queste personalizzazioni, aggiungere un nuovo file nuovo chiamato CustomData al modello e quindi aggiungere un nuovo elemento all'XML nel file vstemplate.  
  
### Aggiungere il file CustomData  
 Il file CustomData è un file di testo con l'estensione CustomData \(il nome file può essere impostato su qualsiasi valore significativo per il modello\) contenente XML.  Il codice XML contenuto nel file CustomData indica di includere l'estensione `My` quando gli utenti utilizzano la pagina **Estensioni My** di Progettazione progetti di Visual Basic.  È anche possibile aggiungere l'attributo `AssemblyFullName>` all'XML del file CustomData  per installare automaticamente l'estensione personalizzata `My` quando un riferimento a un particolare assembly viene aggiunto al progetto.  È possibile utilizzare qualsiasi editor di testo o editor XML per creare il file CustomData e quindi aggiungerlo alla cartella compressa \(file zip\) del modello di elemento.  
  
 Ad esempio, il codice XML seguente indica il contenuto di un file CustomData che aggiunge l'elemento di modello alla cartella Estensioni My di un progetto di Visual Basic quando un riferimento all'assembly Microsoft.VisualBasic.PowerPacks.Vs.dll viene aggiunto al progetto.  
  
```  
<VBMyExtensionTemplate   
    ID="Microsoft.VisualBasic.Samples.MyExtensions.MyPrinterInfo"   
    Version="1.0.0.0"  
    AssemblyFullName="Microsoft.VisualBasic.PowerPacks.vs"  
/>  
```  
  
 Il file CustomData contiene un elemento `VBMyExtensionTemplate>` con attributi, come indicato nella tabella seguente.  
  
|||  
|-|-|  
|Attributo|Descrizione|  
|`ID`|Obbligatorio.  L'identificatore univoco per l'estensione.  Se l'estensione con questo ID è già stata aggiunta al progetto, all'utente non verrà richiesto di aggiungerla nuovamente.|  
|`Version`|Obbligatorio.  Un numero di versione per il modello di elemento.|  
|`AssemblyFullName`|Parametro facoltativo.  Un nome assembly.  Quando un riferimento a questo assembly viene aggiunto al progetto, all'utente verrà richiesto di aggiungere l'estensione `My` da questo modello di elemento.|  
  
### Aggiungere l'elemento \< CustomDataSignature \> al file vstemplate  
 Per identificare il modello di elemento di Visual Studio come estensione dello spazio dei nomi `My`, è necessario anche modificare il file vstemplate per il modello di elemento  aggiungendo l'elemento `<CustomDataSignature>` all'elemento `<TemplateData>`.  L'elemento `<CustomDataSignature>` deve contenere il testo `Microsoft.VisualBasic.MyExtension`, come indicato nel seguente esempio.  
  
```  
<CustomDataSignature>Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
```  
  
 Non è possibile modificare direttamente i file in una cartella compressa \(file zip\).  È necessario copiare il file vstemplate dalla cartella compressa, modificarlo e quindi sostituire il file vstemplate nella cartella compressa con la copia aggiornata.  
  
 Nell'esempio seguente è indicato il contenuto di un file vstemplate con l'elemento `<CustomDataSignature>` aggiunto.  
  
```  
<VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">  
  <TemplateData>  
    <DefaultName>MyCustomExtensionModule.vb</DefaultName>  
    <Name>MyPrinterInfo</Name>  
    <Description>Custom My Extensions Item Template</Description>  
    <ProjectType>VisualBasic</ProjectType>  
    <SortOrder>10</SortOrder>  
    <Icon>__TemplateIcon.ico</Icon>  
    <CustomDataSignature       >Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
  </TemplateData>  
  <TemplateContent>  
    <References />  
    <ProjectItem SubType="Code"   
                 TargetFileName="$fileinputname$.vb"  
                 ReplaceParameters="true"  
     >MyCustomExtensionModule.vb</ProjectItem>  
  </TemplateContent>  
</VSTemplate>  
```  
  
## Installare il modello  
 Per installare il modello è possibile copiare la cartella compressa \(file zip\) nella cartella dei modelli di elemento di Visual Basic \(ad esempio, Documenti\\Visual Studio 2008\\Templates\\Item Templates\\Visual Basic\).  In alternativa, è possibile pubblicare il modello come file di programma di installazione di Visual Studio \(vsi\).  Per informazioni sulla pubblicazione del modello come file di programma di installazione di Visual Studio, vedere [NIB: How to: Publish Project Templates](http://msdn.microsoft.com/it-it/b9087f58-64e9-4767-bf54-e3bf40d63b20).  
  
## Vedere anche  
 [Extending the My Namespace in Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md)   
 [Extending the Visual Basic Application Model](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [Customizing Which Objects are Available in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [Pagina Estensioni My, Progettazione progetti](/visual-studio/ide/reference/my-extensions-page-project-designer-visual-basic)
---
title: "Risorse app per librerie destinate a pi&#249; piattaforme | Microsoft Docs"
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
  - ".NET Framework, risorse per la destinazione a piattaforme multiple"
  - "piattaforme multiple, risorse"
  - "risorse [.NET Framework]"
  - "risorse, piattaforme multiple"
  - "destinazione a piattaforme multiple, risorse"
ms.assetid: 72c76f0b-7255-4576-9261-3587f949669c
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# Risorse app per librerie destinate a pi&#249; piattaforme
Per assicurarsi che le risorse nelle librerie di classi siano accessibili da più piattaforme, è possibile usare il tio di progetto [Libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) di .NET Framework.  Il tipo di progetto è disponibile in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] e fa riferimento al subset portabile della libreria di classi di .NET Framework.  Usando la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] viene garantito che sia possibile accedere alla libreria da applicazioni desktop, applicazioni Silverlight, applicazioni Windows Phone e da applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
 Il progetto [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] crea solo un subset molto limitato dei tipi nello spazio dei nomi di <xref:System.Resources> disponibile per l'applicazione, ma consente di usare la classe <xref:System.Resources.ResourceManager> per recuperare le risorse.  Tuttavia, se si crea un'applicazione tramite Visual Studio, è necessario usare il wrapper fortemente tipizzato creato da Visual Studio anziché usare la classe <xref:System.Resources.ResourceManager> direttamente.  
  
 Per creare un wrapper fortemente tipizzato in Visual Studio, impostare **Modificatore di accesso** del file di risorse principale in Progettazione risorse di Visual Studio su **Pubblico**.  Ciò crea un file \[resourceFileName\].designer.cs o \[resourceFileName\].designer.vb che contiene il wrapper ResourceManager fortemente tipizzato.  Per altre informazioni sull'uso di un wrapper di risorse fortemente tipizzate, vedere la sezione "Generazione di una classe di risorse fortemente tipizzata" nell'argomento [Resgen.exe \(Resource File Generator\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).  
  
## Gestione risorse in [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]  
 In un progetto [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], tutti gli accessi alle risorse sono gestiti dalla classe <xref:System.Resources.ResourceManager>.  Poiché i tipi nello spazio dei nomi <xref:System.Resources>, come <xref:System.Resources.ResourceReader> e <xref:System.Resources.ResourceSet>, non sono accessibili da un progetto [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], non possono essere usati per accedere alle risorse.  
  
 Il progetto [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] include i quattro membri <xref:System.Resources.ResourceManager> elencati nella tabella seguente.  Questi costruttori e metodi consentono di creare un'istanza di un oggetto <xref:System.Resources.ResourceManager> e recuperare le risorse di tipo stringa.  
  
|Membro `ResourceManager`|Descrizione|  
|------------------------------|-----------------|  
|<xref:System.Resources.ResourceManager.%23ctor%28System.String%2CSystem.Reflection.Assembly%29>|Crea un'istanza di <xref:System.Resources.ResourceManager> per accedere al file di risorse denominato individuato nell'assembly specificato.|  
|<xref:System.Resources.ResourceManager.%23ctor%28System.Type%29>|Crea un'istanza di <xref:System.Resources.ResourceManager> che corrisponde al tipo specificato.|  
|<xref:System.Resources.ResourceManager.GetString%28System.String%29>|Recupera una risorsa denominata per impostazioni cultura specifiche.|  
|<xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29>|Recupera una risorse denominata per impostazioni cultura specifiche.|  
  
 L'esclusione di altri membri <xref:System.Resources.ResourceManager> da [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] significa che oggetti serializzati, dati non di tipo stringa e immagini non possono essere recuperati da un file di risorse.  Per usare le risorse da [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], è necessario memorizzare tutti i dati oggetto in forma di stringa.  Ad esempio, è possibile archiviare valori numerici in un file di risorse convertendoli in stringhe e recuperarli per poi riconvertirli in numeri usando il metodo `Parse` o `TryParse` del tipo di dati numerico.  È possibile convertire immagini o altri dati binari in una rappresentazione di stringa chiamando il metodo <xref:System.Convert.ToBase64String%2A?displayProperty=fullName> e ripristinarli in una matrice di byte chiamando il metodo <xref:System.Convert.FromBase64String%2A?displayProperty=fullName>.  
  
## [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] e applicazioni Windows Store  
 I progetti [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] archiviano le risorse in file .resx, che vengono quindi compilati in file .resources e incorporati nell'assembly principale o in assembly satellite in fase di compilazione.  Le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], invece, richiedono che le risorse vengano archiviate nei file .resw, che vengono compilati in un singolo file di indice risorse \(PRI\).  Tuttavia, nonostante l'incompatibilità dei formati dei file, la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] funzionerà in un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
 Per usare la libreria di classi da un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], aggiungere un riferimento al progetto di applicazione Windows Store.  Visual Studio estrarrà in modo trasparente le risorse dall'assembly in un file .resw e le userà per generare un file PRI da cui [!INCLUDE[wrt](../../../includes/wrt-md.md)] potranno essere estratte le risorse.  In fase di esecuzione, [!INCLUDE[wrt](../../../includes/wrt-md.md)] esegue il codice nella [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], ma recupera le risorse della Libreria di classi portabile dal file PRI.  
  
 Se il progetto [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] include risorse localizzate, usare il modello hub and spoke per distribuirle proprio come avviene per una libreria in un'applicazione desktop.  Per usare il file di risorse principale e qualunque file di risorse localizzate in un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], aggiungere un riferimento all'assembly originale.  In fase di compilazione, Visual Studio estrae le risorse dal file di risorse principale ed ogni file di risorse localizzate in file .resw separati.  Vengono quindi compilate i file .resw in un singolo file PRI a cui [!INCLUDE[wrt](../../../includes/wrt-md.md)] accede in fase di esecuzione.  
  
<a name="NonLoc"></a>   
## Esempio: [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] non localizzata  
 Il seguente semplice esempio di [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] non localizzata usa le risorse per archiviare i nomi delle colonne e per determinare il numero di caratteri da riservare ai dati tabulari.  Nell'esempio viene usato un file denominato LibResources.resx per archiviare le risorse di tipo stringa elencate nella tabella seguente.  
  
|Nome della risorsa|Valore della risorsa|  
|------------------------|--------------------------|  
|Born|Birthdate|  
|BornLength|12|  
|Hired|Data assunzione|  
|HiredLength|12|  
|ID|ID|  
|ID.Length|12|  
|Nome|Nome|  
|NameLength|25|  
|Titolo|Employee Database|  
  
 Il codice seguente definisce una classe `UILibrary` che usa il wrapper di Gestione risorse denominato `resources` generato da Visual Studio quando **Modificatore di accesso** per il file viene modificato in **Pubblico**.  La classe UILibrary analizza i dati della stringa, se necessario.  .  Notare che la classe si trova nello spazio dei nomi `MyCompany.Employees`.  
  
 [!code-csharp[Conceptual.Resources.Portable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/uilibrary.cs#1)]
 [!code-vb[Conceptual.Resources.Portable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/uilibrary.vb#1)]  
  
 Nell'esempio di codice riportato di seguito viene illustrato come sia possibile accedere alla classe `UILibrary` e alle relative risorse da una applicazione in modalità console.  Richiede che venga aggiunto un riferimento a UILIbrary.dll al progetto di applicazione console.  
  
 [!code-csharp[Conceptual.Resources.Portable#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program.cs#2)]
 [!code-vb[Conceptual.Resources.Portable#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module1.vb#2)]  
  
 Il codice seguente mostra come sia possibile accedere alla classe `UILibrary` e alle relative risorse da un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  Richiede che venga aggiunto un riferimento a UILIbrary.dll al progetto di applicazione Windows Store.  
  
 [!code-csharp[Conceptual.Resources.PortableMetro#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetro/cs/blankpage.xaml.cs#1)]  
  
## Esempio: [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] localizzata  
 Il seguente esempio di [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] localizzata include le risorse per le impostazioni cultura francesi \(Francia\) e inglesi \(Stati Uniti\).  Le impostazioni cultura inglese \(Stati Uniti\) sono le impostazioni cultura predefinite dell'applicazione. Le risorse vengono illustrate nella tabella della [sezione precedente](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md#NonLoc).  Il file di risorse per le impostazioni cultura francesi \(Francia\) è denominato LibResources.fr\-FR.resx ed è costituito dalle risorse di tipo stringa elencate nella tabella seguente.  Il codice sorgente per la classe `UILibrary` è lo stesso di quello riportato nella sezione precedente.  
  
|Nome della risorsa|Valore della risorsa|  
|------------------------|--------------------------|  
|Born|Date de naissance|  
|BornLength|20|  
|Hired|Date embauché|  
|HiredLength|16|  
|ID|ID|  
|Nome|Nom|  
|Titolo|Base de données des employés|  
  
 Nell'esempio di codice riportato di seguito viene illustrato come sia possibile accedere alla classe `UILibrary` e alle relative risorse da una applicazione in modalità console.  Richiede che venga aggiunto un riferimento a UILIbrary.dll al progetto di applicazione console.  
  
 [!code-csharp[Conceptual.Resources.Portable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program2.cs#3)]
 [!code-vb[Conceptual.Resources.Portable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module2.vb#3)]  
  
 Il codice seguente mostra come sia possibile accedere alla classe `UILibrary` e alle relative risorse da un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  Richiede che venga aggiunto un riferimento a UILIbrary.dll al progetto di applicazione Windows Store.  Usa la proprietà statica `ApplicationLanguages.PrimaryLanguageOverride` per impostare la lingua preferita dell'applicazione in francese.  
  
 [!code-csharp[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetroloc/cs/blankpage.xaml.cs#1)]
 [!code-vb[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portablemetroloc/vb/blankpage.xaml.vb#1)]  
  
## Vedere anche  
 <xref:System.Resources.ResourceManager>   
 [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md)   
 [Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)
---
title: "How to: Configure .NET Framework-Based COM Components for Registration-Free Activation | Microsoft Docs"
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
  - "components [.NET Framework], manifest"
  - "application manifests [.NET Framework]"
  - "manifests [.NET Framework]"
  - "registration-free COM interop, configuring .NET-based components"
  - "activation, registration-free"
ms.assetid: 32f8b7c6-3f73-455d-8e13-9846895bd43b
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Configure .NET Framework-Based COM Components for Registration-Free Activation
L'attivazione senza registrazione per i componenti basati su .NET Framework risulta solo leggermente più complessa rispetto a quella per i componenti COM.  Per la configurazione sono richiesti due manifesti:  
  
-   Le applicazioni COM devono disporre di un manifesto dell'applicazione di tipo Win32 per identificare il componente gestito.  
  
-   I componenti basati su .NET Framework devono disporre di un manifesto del componente per le informazioni sull'attivazione necessarie in fase di esecuzione.  
  
 Nel presente argomento viene descritto come associare un manifesto dell'applicazione a un'applicazione, come associare un manifesto del componente a un componente e come incorporare un manifesto del componente in un assembly.  
  
### Per creare un manifesto dell'applicazione  
  
1.  Utilizzando un editor XML, creare o modificare il manifesto dell'applicazione di proprietà dell'applicazione COM che interagisce con uno o più componenti gestiti.  
  
2.  Inserire la seguente intestazione standard all'inizio del file:  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
    ```  
  
     Per informazioni sugli elementi del manifesto e sui relativi attributi, cercare "Application Manifests Reference" in MSDN Library \(informazioni in lingua inglese\).  
  
3.  Identificare il proprietario del manifesto.  Nell'esempio seguente il proprietario del file manifesto è `myComApp` versione 1.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
      <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myComApp"   
                        version="1.0.0.0"   
                        processorArchitecture="msil"   
      />  
    ```  
  
4.  Identificare gli assembly dipendenti.  Nell'esempio riportato di seguito, `myComApp` dipende da `myManagedComp`.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
      <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myComApp"   
                        version="1.0.0.0"   
                        processorArchitecture="x86"   
                        publicKeyToken="8275b28176rcbbef"  
      />  
      <dependency>  
        <dependentAssembly>  
          <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myManagedComp"   
                        version="6.0.0.0"   
                        processorArchitecture="X86"   
                        publicKeyToken="8275b28176rcbbef"  
          />  
        </dependentAssembly>  
      </dependency>  
    </assembly>  
    ```  
  
5.  Salvare e denominare il file manifesto.  Il nome di un manifesto dell'applicazione è costituito dal nome dell'eseguibile dell'assembly seguito dall'estensione MANIFEST.  Il nome file del manifesto dell'applicazione per myComApp.exe, ad esempio, è myComApp.exe.manifest.  
  
 Un manifesto dell'applicazione può essere installato nella stessa directory dell'applicazione COM.  In alternativa, può essere aggiunto come risorsa al file EXE dell'applicazione.  Per ulteriori informazioni, cercare "Side\-by\-side Assemblies" in MSDN Library \(informazioni in lingua inglese\).  
  
#### Per creare un manifesto del componente  
  
1.  Utilizzando un editor XML, creare un manifesto del componente per descrivere l'assembly gestito.  
  
2.  Inserire la seguente intestazione standard all'inizio del file:  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
    ```  
  
3.  Identificare il proprietario del file.  L'elemento `<assemblyIdentity>` dell'elemento `<dependentAssembly>` nel file manifesto dell'applicazione deve corrispondere a quello contenuto nel manifesto del componente.  Nell'esempio seguente il proprietario del file manifesto è `myManagedComp` versione 1.2.3.4.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
           <assemblyIdentity  
                        name="myOrganization.myDivision.myManagedComp"  
                        version="1.2.3.4"  
                        publicKeyToken="8275b28176rcbbef"  
                        processorArchitecture="msil"  
           />  
    ```  
  
4.  Identificare ogni classe nell'assembly.  Utilizzare l'elemento `<clrClass>` per identificare in modo univoco ogni classe nell'assembly gestito.  L'elemento, che costituisce un sottoelemento di `<assembly>`, dispone degli attributi descritti nella tabella seguente.  
  
    |Attributo|Descrizione|Obbligatorio|  
    |---------------|-----------------|------------------|  
    |`clsid`|Identificatore che specifica la classe da attivare.|Sì|  
    |`description`|Stringa contenente informazioni sul componente.  Il valore predefinito è una stringa vuota.|No|  
    |`name`|Stringa che rappresenta la classe gestita.|Sì|  
    |`progid`|Identificatore da utilizzare per l'attivazione con associazione tardiva.|No|  
    |`threadingModel`|Modello di threading COM. "Both" è il valore predefinito.|No|  
    |`runtimeVersion`|Specifica la versione di Common Language Runtime \(CLR\) da utilizzare.  Se questo attributo non viene specificato, e il CLR non è ancora stato caricato, il componente viene caricato con l'ultimo CLR installato prima della versione 4.  Se si specifica v1.0.3705, v1.1.4322 o v2.0.50727, la versione esegue automaticamente il roll forward all'ultima versione CLR installata prima della versione 4 \(di solito v2.0.50727\).  Se è già stata caricata un'altra versione di CLR ed è possibile caricare la versione specificata side\-by\-side in\-process, la versione specificata viene caricata; in caso contrario, viene utilizzato il CLR caricato.  Potrebbe verificarsi un errore di caricamento.|No|  
    |`tlbid`|Identificatore della libreria dei tipi contenente informazioni sui tipi per la classe.|No|  
  
     In tutti i tag di attributi viene effettuata la distinzione tra maiuscole e minuscole.  È possibile ottenere i CLSID, i ProgID, i modelli di threading e la versione del runtime visualizzando la libreria dei tipi esportata per l'assembly con il Visualizzatore oggetti OLE\/COM \(Oleview.exe\).  
  
     Nel manifesto del componente seguente vengono identificate due classi, `testClass1` e `testClass2`.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
           <assemblyIdentity  
                        name="myOrganization.myDivision.myManagedComp"  
                        version="1.2.3.4" />  
                        publicKeyToken="8275b28176rcbbef"  
           />  
           <clrClass  
                        clsid="{65722BE6-3449-4628-ABD3-74B6864F9739}"  
                        progid="myManagedComp.testClass1"  
                        threadingModel="Both"  
                        name="myManagedComp.testClass1"  
                        runtimeVersion="v1.0.3705">  
           </clrClass>  
           <clrClass  
                        clsid="{367221D6-3559-3328-ABD3-45B6825F9732}"  
                        progid="myManagedComp.testClass2"  
                        threadingModel="Both"  
                        name="myManagedComp.testClass2"  
                        runtimeVersion="v1.0.3705">  
           </clrClass>  
           <file name="MyManagedComp.dll">  
           </file>  
    </assembly>  
    ```  
  
5.  Salvare e denominare il file manifesto.  Il nome di un manifesto del componente è costituito dal nome della libreria dell'assembly seguito dall'estensione MANIFEST.  La libreria myManagedComp.dll, ad esempio, corrisponde a myManagedComp.manifest.  
  
 È necessario incorporare il manifesto del componente come risorsa nell'assembly.  
  
#### Per incorporare un manifesto del componente in un assembly gestito  
  
1.  Creare uno script di risorse contenente la seguente istruzione:  
  
     `RT_MANIFEST 1 myManagedComp.manifest`  
  
     In questa istruzione, `myManagedComp.manifest` rappresenta il nome del manifesto del componente da incorporare.  Nell'esempio, il nome file dello script è `myresource.rc`.  
  
2.  Compilare lo script mediante il compilatore di risorse di Microsoft Windows \(Rc.exe\).  Al prompt dei comandi digitare il seguente comando:  
  
     `rc myresource.rc`  
  
     Mediante Rc.exe viene creato il file di risorse `myresource.res`.  
  
3.  Compilare di nuovo il file di origine dell'assembly e specificare il file di risorse utilizzando l'opzione **\/win32res**:  
  
    ```  
    /win32res:myresource.res  
    ```  
  
     Anche in questo caso, `myresource.res` rappresenta il nome del file di risorse contenente la risorsa incorporata.  
  
## Vedere anche  
 [Registration\-Free COM Interop](../../../docs/framework/interop/registration-free-com-interop.md)   
 [Requirements for Registration\-Free COM Interop](http://msdn.microsoft.com/it-it/0c43bc57-eecf-4e6c-8114-490141cce4da)   
 [Configuring COM Components for Registration\-Free Activation](http://msdn.microsoft.com/it-it/bfe9b02f-d964-4784-960e-a1f94692fbfe)   
 [L'attivazione senza registrazione di componenti basati su.NET: Una procedura dettagliata](http://go.microsoft.com/fwlink/?LinkId=158812)
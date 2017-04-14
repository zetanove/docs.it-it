---
title: "Ritardo della firma di un assembly | Microsoft Docs"
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
  - "rinvio della firma dell'assembly"
  - "firma di assembly"
  - "assembly [.NET Framework], firma"
  - "assembly con nome sicuro, ritardo della firma dell'assembly"
  - "firma parziale dell'assembly"
ms.assetid: 9d300e17-5bf1-4360-97da-2aa55efd9070
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Ritardo della firma di un assembly
È possibile che in un'organizzazione venga utilizzata una coppia di chiavi sottoposta a una rigorosa sicurezza e quindi non accessibile giornalmente agli sviluppatori.  La chiave pubblica è spesso disponibile, ma l'accesso alla chiave privata è consentito solo ad alcune persone.  Quando si sviluppano assembly con nome sicuro, in ogni assembly che fa riferimento all'assembly con nome sicuro di destinazione è contenuto un token della chiave pubblica utilizzata per assegnare un nome sicuro all'assembly di destinazione.  È quindi necessario che la chiave pubblica risulti disponibile durante il processo di sviluppo.  
  
 È possibile utilizzare la firma ritardata o parziale in fase di compilazione per riservare nel file eseguibile trasportabile \(PE, Portable Executable\) lo spazio per la firma con nome sicuro, ma posticipare la firma effettiva a una fase successiva \(solitamente prima della consegna dell'assembly\).  
  
 Nei passaggi successivi viene descritto il processo che consente di ritardare la firma di un assembly.  
  
1.  Ottenere la parte pubblica della coppia di chiavi dall'organizzazione da cui verrà effettivamente apposta la firma.  Tale chiave si presenta solitamente sotto forma di file con estensione snk. È possibile creare questo file mediante lo [strumento Nome sicuro \(Sn.exe\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md), disponibile in [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
2.  Apporre annotazioni al codice sorgente per l'assembly utilizzando due attributi personalizzati da <xref:System.Reflection>:  
  
    -   <xref:System.Reflection.AssemblyKeyFileAttribute>, che consente di passare il nome del file contenente la chiave pubblica come parametro al costruttore.  
  
    -   <xref:System.Reflection.AssemblyDelaySignAttribute>, che indica che si sta utilizzando il ritardo della firma passando **true** come parametro al costruttore.  Di seguito è riportato un esempio.  
  
         [!code-cpp[AssemblyDelaySignAttribute#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#4)]
         [!code-csharp[AssemblyDelaySignAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#4)]
         [!code-vb[AssemblyDelaySignAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#4)]  
  
3.  La chiave pubblica viene inserita dal compilatore nel manifesto dell'assembly e nel file PE viene riservato spazio per la firma completa con nome sicuro.  È necessario che la vera chiave pubblica sia memorizzata in fase di compilazione, in modo che gli altri assembly contenenti riferimenti a questo assembly siano in grado di ottenere la chiave da memorizzare nei relativi riferimenti di assembly.  
  
4.  Poiché l'assembly non dispone di una firma con nome sicuro valida, è necessario disattivare la verifica di tale assembly.  Per effettuare questa operazione, è possibile utilizzare l'opzione **–Vr** con lo strumento Nome sicuro.  
  
     L'esempio seguente consente di disattivare la verifica per un assembly denominato `myAssembly.dll`.  
  
    ```  
    sn –Vr myAssembly.dll  
    ```  
  
     Per disattivare la verifica delle piattaforme in cui non è possibile eseguire lo strumento Nome sicuro, come microprocessori avanzati del computer RISC \(ARM\), utilizzare l'opzione **–Vk** per creare un file di Registro.  Importare il file di Registro nel Registro di sistema sul computer in cui si desidera disattivare la verifica.  Nell'esempio seguente viene creato un file di Registro per `myAssembly.dll`.  
  
    ```  
    sn –Vk myRegFile.reg myAssembly.dll  
    ```  
  
     Con **–Vr** o l'opzione **–Vk**, è possibile includere un file SNK per la firma della chiave di test.  
  
    > [!CAUTION]
    >  Utilizzare l'opzione **\-Vr** oppure l'opzione **–Vk** solo in fase di sviluppo.  L'aggiunta di un assembly all'elenco di omissione della verifica rende vulnerabile il sistema di sicurezza.  Un assembly dannoso potrebbe utilizzare il nome completamente specificato \(nome assembly, versione, impostazioni cultura e token della chiave pubblica\) dell'assembly aggiunto all'elenco di omissione della verifica per camuffare la propria identità.  La verifica verrebbe omessa quindi anche per l'assembly dannoso.  
  
    > [!NOTE]
    >  Se si utilizza la firma ritardata durante lo sviluppo con Visual Studio su un computer a 64 bit e si compila un assembly per **Qualsiasi CPU**, potrebbe essere necessario applicare due volte l'opzione **\-Vr**. \(In Visual Studio, **Qualsiasi CPU** è un valore della proprietà di compilazione **Piattaforma di destinazione**; quando si compila dalla riga di comando, è l'impostazione predefinita\). Per eseguire l'applicazione dalla riga di comando o da Esplora risorse, utilizzare la versione a 64 bit di [Sn.exe \(Strong Name Tool\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md) per applicare l'opzione **\-Vr** all'assembly.  Per caricare in fase di progettazione l'assembly in Visual Studio, \(ad esempio, se l'assembly contiene componenti utilizzati dagli altri assembly nell'applicazione\) utilizzare la versione a 32 bit dello strumento con nome sicuro.  Questo perché il compilatore just\-in\-time \(JIT\) compila l'assembly nel codice nativo a 64 bit quando l'assembly viene eseguito dalla riga di comando e nel codice nativo a 32 bit quando l'assembly viene caricato nell'ambiente di progettazione.  
  
5.  Successivamente, di solito prima della consegna, sottoporre l'assembly all'autorità di firma dell'organizzazione per la firma con nome sicuro effettiva tramite l'opzione **–R** con lo strumento Nome sicuro.  
  
     L'esempio seguente consente di firmare un assembly denominato `myAssembly.dll` con un nome sicuro utilizzando la coppia di chiavi `sgKey.snk`.  
  
    ```  
    sn -R myAssembly.dll sgKey.snk  
    ```  
  
## Vedere anche  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Procedura: creare una coppia di chiavi pubblica\/privata](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)   
 [Sn.exe \(Strong Name Tool\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)
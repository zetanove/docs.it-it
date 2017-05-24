---
title: Strumenti di .NET framework | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- command line, .NET Framework tools
- .NET Framework, tools
- tools [.NET Framework]
- running .NET Framework tools
ms.assetid: a2ca532d-91f7-426a-9303-417c2ee1247c
caps.latest.revision: 65
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: baaf365a21661b377f8151e5d97ac16542aa2c36
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="net-framework-tools"></a>Strumenti di .NET Framework
Gli strumenti di .NET Framework facilitano la creazione, la distribuzione e la gestione di applicazioni e componenti destinati a .NET Framework.  
  
 La maggior parte degli strumenti di .NET Framework descritti in questa sezione vengono installati automaticamente con Visual Studio. Per informazioni sull'installazione, vedere [Download di Visual Studio](http://go.microsoft.com/fwlink/?LinkID=325532).  
  
 Tutti gli strumenti possono essere eseguiti dalla riga di comando, ad eccezione di Visualizzatore Assembly Cache (Shfusion.dll). Per accedere a Shfusion.dll occorre usare Esplora file.  
  
 Il modo migliore per eseguire gli strumenti da riga di comando è tramite il prompt dei comandi per gli sviluppatori per Visual Studio. Queste utilità consentono di eseguire gli strumenti facilmente, senza dover passare alla cartella di installazione. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
> [!NOTE]
>  Alcuni strumenti sono specifici per computer a 32 bit o computer a 64 bit. Assicurarsi di eseguire la versione dello strumento appropriata per il computer.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Al.exe (Assembly Linker)](../../../docs/framework/tools/al-exe-assembly-linker.md)  
 Genera un file che dispone di un manifesto dell'assembly ricavato da moduli o file di risorse.  
  
 [Aximp.exe (utilità di importazione di controlli ActiveX di Windows Form)](../../../docs/framework/tools/aximp-exe-windows-forms-activex-control-importer.md)  
 Consente di convertire le definizioni dei tipi in una libreria di tipi COM per un controllo ActiveX in un controllo Windows Form.  
  
 [Caspol.exe (strumento per i criteri di sicurezza dall'accesso di codice)](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)  
 Consente di visualizzare e configurare i criteri di sicurezza stabiliti a livello di computer, di utente o dell'intera azienda. In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] e versioni successive questo strumento influisce sui criteri di sicurezza dall'accesso di codice solo se l'elemento [\<legacyCasPolicy>](../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md) è impostato su `true`. Per altre informazioni, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
 [Cert2spc.exe (strumento di test dei certificati del distributore di software)](../../../docs/framework/tools/cert2spc-exe-software-publisher-certificate-test-tool.md)  
 Crea un certificato dell'editore del software (SPC, Software Publisher's Certificate) da uno o più certificati X.509. Questo strumento è finalizzato unicamente ai test.  
  
 [Certmgr.exe (strumento di gestione certificati)](../../../docs/framework/tools/certmgr-exe-certificate-manager-tool.md)  
 Consente di gestire certificati, elenchi di certificati attendibili (CTL, Certificate Trust List) ed elenchi di certificati revocati (CRL, Certificate Revocation List).  
  
 [Clrver.exe (Strumento della versione CLR)](../../../docs/framework/tools/clrver-exe-clr-version-tool.md)  
 Segnala tutte le versioni di CLR (Common Language Runtime) installate nel computer.  
  
 [CorFlags.exe (strumento di conversione CorFlags)](../../../docs/framework/tools/corflags-exe-corflags-conversion-tool.md)  
 Consente di configurare la sezione CorFlags dell'intestazione di un'immagine PE.  
  
 [Fuslogvw.exe (Visualizzatore log binding assembly)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md)  
 Visualizza informazioni sulle associazioni di assembly per consentire di diagnosticare per quale motivo non sia possibile individuare un assembly in fase di esecuzione.  
  
 [Gacutil.exe (strumento Global Assembly Cache)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)  
 Consente di visualizzare e modificare il contenuto della Global Assembly Cache e della Download Cache.  
  
 [Ilasm.exe (Assembler IL)](../../../docs/framework/tools/ilasm-exe-il-assembler.md)  
 Genera un file eseguibile di tipo PE dal linguaggio intermedio (IL). È possibile eseguire il file eseguibile così ottenuto per determinare se il codice IL funziona come previsto.  
  
 [Ildasm.exe (Disassembler IL)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)  
 Accetta un file eseguibile di tipo PE contenente codice del linguaggio intermedio (IL) e crea un file di testo utilizzabile come input per l'assembler IL (Ilasm.exe).  
  
 [Installutil.exe (Strumento Programma di installazione)](../../../docs/framework/tools/installutil-exe-installer-tool.md)  
 Consente di installare e disinstallare le risorse del server eseguendo i componenti del programma di installazione di un assembly specificato. Funziona con le classi dello spazio dei nomi <xref:System.Configuration.Install>. Consente di installare e disinstallare le risorse del server eseguendo i componenti del programma di installazione di un assembly specificato. Funziona con le classi dello spazio dei nomi <xref:System.Configuration.Install>.  
  
 [Lc.exe (Compilatore licenze)](../../../docs/framework/tools/lc-exe-license-compiler.md)  
 Legge i file di testo che contengono informazioni sulla licenza e genera un file con estensione licenses che è possibile incorporare come risorsa in un eseguibile di Common Language Runtime. Legge i file di testo che contengono informazioni sulla licenza e genera un file con estensione licenses che è possibile incorporare come risorsa in un eseguibile di Common Language Runtime.  
  
 [Mage.exe (Strumento per la generazione e la modifica di manifesti)](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md)  
 Consente di creare, modificare e firmare manifesti dell'applicazione e di distribuzione. Come strumento della riga di comando, Mage.exe può essere eseguito sia da script batch sia da altre applicazioni basate su Windows, incluse le applicazioni ASP.NET.  
  
 [MageUI.exe (Strumento per la generazione e la modifica di manifesti, client grafico)](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)  
 Supporta le stesse funzionalità dello strumento della riga di comando Mage.exe, ma usa un'interfaccia utente basata su Windows. Supporta le stesse funzionalità dello strumento della riga di comando Mage.exe, ma usa un'interfaccia utente basata su Windows.  
  
 [MDbg.exe (Debugger della riga di comando di .NET Framework)](../../../docs/framework/tools/mdbg-exe.md)  
 Consente ai fornitori di strumenti e agli sviluppatori di applicazioni di individuare e correggere i bug dei programmi basati sul Common Language Runtime di .NET Framework. Questo strumento usa l'API di debug del runtime per offrire servizi di debug.  
  
 [Mgmtclassgen.exe (Generatore di classi di gestione fortemente tipizzate)](../../../docs/framework/tools/mgmtclassgen-exe.md)  
 Consente di generare una classe gestita con associazione anticipata per una classe Windows Management Instrumentation (WMI) specificata.  
  
 [Mpgo.exe (strumento per l'ottimizzazione guidata da profilo gestito)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md)  
 Consente di ottimizzare gli assembly di immagini native usando scenari comuni dell'utente finale. Mpgo.exe consente la generazione e l'utilizzo di dati di profilatura per gli assembly di applicazioni di immagini native (non gli assembly .NET Framework) usando scenari di training selezionati dallo sviluppatore di applicazioni.  
  
 [Ngen.exe (generatore di immagini native)](../../../docs/framework/tools/ngen-exe-native-image-generator.md)  
 Migliora le prestazioni delle applicazioni gestite tramite l'utilizzo di immagini native, ovvero file che contengono codice macchina compilato specifico del processore. Il runtime può usare le immagini native della cache anziché il compilatore Just-In-Time (JIT) per compilare l'assembly originale.  
  
 [Peverify.exe (strumento PEVerify)](../../../docs/framework/tools/peverify-exe-peverify-tool.md)  
 Consente di verificare se il codice Microsoft Intermediate Language (MSIL) e i metadati associati soddisfano i requisiti di indipendenza dai tipi. Consente di verificare se il codice Microsoft Intermediate Language (MSIL) e i metadati associati soddisfano i requisiti di indipendenza dai tipi.  
  
 [Regasm.exe (strumento di registrazione di assembly)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md)  
 Legge i metadati in un assembly e aggiunge le voci necessarie nel Registro di sistema. In questo modo i client COM vengono visualizzati come classi .NET Framework.  
  
 [Regsvcs.exe (strumento di installazione dei servizi .NET)](../../../docs/framework/tools/regsvcs-exe-net-services-installation-tool.md)  
 Carica e registra un assembly, genera e installa una libreria dei tipi in un'applicazione specificata della versione 1.0 di COM+ e configura i servizi aggiunti a livello di codice a una classe.  
  
 [Resgen.exe (generatore di file di risorse)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)  
 Converte i file di testo (con estensione txt o restxt) e i file di formato di risorsa basato su XML (con estensione resx) in file binari di Common Language Runtime (con estensione resources) che è possibile incorporare in un eseguibile binario di runtime o compilare in assembly satellite.  
  
 [SecAnnotate.exe (strumento .NET Security Annotator)](../../../docs/framework/tools/secannotate-exe-net-security-annotator-tool.md)  
 Identifica le parti SecurityCritical e SecuritySafeCritical di un assembly. Identifica le parti `SecurityCritical` e `SecuritySafeCritical` di un assembly.  
  
 [SignTool.exe (strumento per la firma)](../../../docs/framework/tools/signtool-exe.md)  
 Consente di apporre una firma digitale ai file, di verificare le firme nei file e di apporre un timestamp ai file.  
  
 [Sn.exe (strumento Nome sicuro)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)  
 Consente di creare assembly con nomi sicuri. In questo strumento sono disponibili opzioni per la gestione delle chiavi nonché per la generazione e la verifica delle firme.  
  
 [SOS.dll (estensione del debugger SOS)](../../../docs/framework/tools/sos-dll-sos-debugging-extension.md)  
 Facilita l'esecuzione del debug di programmi gestiti nel debugger WinDbg.exe e in Visual Studio fornendo informazioni sull'ambiente Common Language Runtime interno.  
  
 [SqlMetal.exe (strumento per la generazione del codice)](../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)  
 Genera codice e attributi di mapping per il componente LINQ to SQL di .NET Framework.  
  
 [Storeadm.exe (strumento per lo spazio di memorizzazione isolato)](../../../docs/framework/tools/storeadm-exe-isolated-storage-tool.md)  
 Gestisce lo spazio di memorizzazione isolato, fornisce opzioni per elencare ed eliminare le archiviazioni dell'utente.  
  
 [Tlbexp.exe (utilità di esportazione della libreria dei tipi)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)  
 Genera una libreria dei tipi che descrive i tipi definiti in un assembly di Common Language Runtime.  
  
 [Tlbimp.exe (utilità di importazione della libreria dei tipi)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)  
 Converte le definizioni dei tipi presenti in una libreria dei tipi COM nelle definizioni equivalenti di un assembly di Common Language Runtime.  
  
 [Winmdexp.exe (strumento di esportazione di metadati di Windows Runtime)](../../../docs/framework/tools/winmdexp-exe-windows-runtime-metadata-export-tool.md)  
 Esporta un assembly .NET Framework che viene compilato come file .winmdobj in un componente Windows Runtime, il quale viene assemblato come file .winmd contenente sia i metadati Windows Runtime che le informazioni di implementazione.  
  
 [Winres.exe (editor di risorse di Windows Form)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)  
 Consente di localizzare risorse dell'interfaccia utente (file con estensione resx o resources) usate da Windows Form. È possibile tradurre stringhe e quindi ridimensionare, spostare e nascondere i controlli per adattarli alle stringhe localizzate.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Strumenti](http://msdn.microsoft.com/library/f533241c-317c-445e-88ca-c80c8d078fca)  
 Include strumenti quali lo strumento di conformità isXPS (isXPS.exe) e gli strumenti di profilatura delle prestazioni.  
  
 [Strumenti Windows Communication Foundation](../../../docs/framework/wcf/tools.md)  
 Include strumenti che semplificano la creazione, la distribuzione e la gestione di applicazioni Windows Communication Foundation (WCF).

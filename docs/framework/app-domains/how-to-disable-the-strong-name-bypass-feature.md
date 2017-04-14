---
title: "Procedura: disabilitare la funzionalit&#224; che consente di ignorare il nome sicuro | Microsoft Docs"
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
  - "funzionalità che consente di ignorare la verifica del nome sicuro"
  - "assembly con nome sicuro, caricamento in domini dell'applicazione trusted"
ms.assetid: 234e088c-3b11-495a-8817-e0962be79d82
caps.latest.revision: 30
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 30
---
# Procedura: disabilitare la funzionalit&#224; che consente di ignorare il nome sicuro
A partire da .NET Framework versione 3.5 Service Pack 1 \(SP1\), le firme con nome sicuro non vengono convalidate quando un assembly viene caricato in un oggetto <xref:System.AppDomain> con attendibilità totale, ad esempio l'oggetto <xref:System.AppDomain> predefinito per la zona `MyComputer`.  Questa novità viene definita funzionalità che consente di ignorare il nome sicuro.  In un ambiente di attendibilità totale le richieste di <xref:System.Security.Permissions.StrongNameIdentityPermission> hanno sempre esito positivo per gli assembly firmati con attendibilità totale, indipendentemente dalla firma.  L'unica restrizione è che l'assembly deve essere completamente completamente attendibile perché la relativa area è completamente attendibile.  Poiché il nome sicuro non è un fattore determinante in queste condizioni, non esiste alcun motivo per cui venga validato.  Se la convalida di firme con nome sicuro viene ignorata, si ottengono miglioramenti significativi delle prestazioni.  
  
 La funzionalità che consente di ignorare il nome sicuro si applica a qualsiasi assembly completamente attendibile che non abbia la firma ritardata e che sia caricato in un oggetto <xref:System.AppDomain> con attendibilità totale dalla directory specificata dalla proprietà <xref:System.AppDomainSetup.ApplicationBase%2A>.  
  
 È possibile ignorare questa funzionalità per tutte le applicazioni di un computer impostando il valore di una chiave del Registro di sistema.  È possibile ignorare l'impostazione per una singola applicazione utilizzando il relativo file di configurazione.  Non è possibile ripristinare questa funzionalità per una singola applicazione se è stata disabilitata dalla chiave del Registro di sistema.  
  
 Quando si ignora la funzionalità, il nome sicuro viene convalidato solo per verificare che sia corretto. Non viene controllata la presenza di un oggetto <xref:System.Security.Permissions.StrongNameIdentityPermission>.  Se si desidera verificare un nome sicuro specifico, è necessario eseguire il controllo separatamente.  
  
> [!IMPORTANT]
>  La possibilità per forzare la convalida del nome sicuro dipende da una chiave del Registro di sistema, come descritto nella procedura seguente.  Se un'applicazione è in esecuzione con un account che non dispone di un'autorizzazione ACL \(Access Control List, elenco di controllo di accesso\) per l'accesso alla chiave del Registro di sistema, l'impostazione non ha alcun effetto.  Assicurarsi che siano configurati diritti ACL per questa chiave, in modo che sia leggibile per tutti gli assembly.  
  
### Per disabilitare la funzionalità che consente di ignorare il nome sicuro per tutte le applicazioni  
  
-   Nei computer a 32 bit creare nel Registro di sistema una voce DWORD con un valore di 0 denominata `AllowStrongNameBypass` nella chiave HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework.  
  
-   Nei computer a 64 bit creare nel Registro di sistema una voce DWORD con un valore di 0 denominata `AllowStrongNameBypass` nelle chiavi HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework e HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\.NETFramework.  
  
### Per disabilitare la funzionalità che consente di ignorare il nome sicuro per una singola applicazione  
  
1.  Aprire o creare il file di configurazione dell'applicazione.  
  
     Per ulteriori informazioni su questo file, vedere la sezione relativa ai file di configurazione dell'applicazione in [Configurazione di app](../../../docs/framework/configure-apps/index.md).  
  
2.  Aggiungere la voce seguente:  
  
    ```  
    <configuration>  
      <runtime>  
         < bypassTrustedAppStrongNames enabled="false" />  
      </runtime>  
    </configuration>  
    ```  
  
 È possibile ripristinare la funzionalità per l'applicazione rimuovendo l'impostazione del file di configurazione oppure impostando l'attributo su "true".  
  
> [!NOTE]
>  È possibile attivare e disabilitare la convalida dei nomi sicuri per un'applicazione solo se nel computer è attivata la funzionalità che consente di ignorare il nome sicuro.  Se tale funzionalità è stata disabilitata per il computer, i nomi sicuri vengono convalidati per tutte le applicazioni e non è possibile ignorare la convalida per una singola applicazione.  
  
## Vedere anche  
 [Sn.exe \(Strong Name Tool\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)   
 [Elemento \<bypassTrustedAppStrongNames\>](../../../docs/framework/configure-apps/file-schema/runtime/bypasstrustedappstrongnames-element.md)   
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
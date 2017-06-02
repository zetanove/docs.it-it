---
title: "How to: Run Partially Trusted Code in a Sandbox | Microsoft Docs"
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
  - "partially trusted code"
  - "sandboxing"
  - "partial trust"
  - "restricted security environment"
  - "code security, sandboxing"
ms.assetid: d1ad722b-5b49-4040-bff3-431b94bb8095
caps.latest.revision: 27
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 25
---
# How to: Run Partially Trusted Code in a Sandbox
Il termine sandboxing si riferisce all'esecuzione di codice in un ambiente di sicurezza con restrizioni che limita le autorizzazioni di accesso concesse al codice.  Se, ad esempio, si dispone di una libreria gestita proveniente da un'origine non considerata completamente attendibile, è consigliabile non eseguirla come completamente attendibile.  Inserire invece il codice in un ambiente sandbox che limita le autorizzazioni a quelle che si prevede siano necessarie \(ad esempio, l'autorizzazione <xref:System.Security.Permissions.SecurityPermissionFlag>\).  
  
 È anche possibile usare il sandboxing per testare il codice da distribuire che verrà eseguito in ambienti parzialmente attendibili.  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta.  Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
 Un oggetto <xref:System.AppDomain> costituisce un modo efficace per fornire un ambiente sandbox per le applicazioni gestite.  I domini applicazione usati per l'esecuzione di codice parzialmente attendibile dispongono di autorizzazioni che definiscono le risorse protette disponibili durante l'esecuzione in <xref:System.AppDomain>.  Il codice eseguito in <xref:System.AppDomain> è vincolato dalle autorizzazioni associate a <xref:System.AppDomain> e può accedere solo alle risorse specificate.  <xref:System.AppDomain> include anche una matrice <xref:System.Security.Policy.StrongName> usata per identificare gli assembly da caricare come completamente attendibili.  In questo modo, il creatore di un oggetto <xref:System.AppDomain> può avviare un nuovo dominio in modalità sandbox tramite cui gli assembly helper vengono considerati completamente attendibili.  Un'altra opzione per il caricamento degli assembly come completamente attendibili consiste nel collocarli nella Global Assembly Cache. In questo modo, tuttavia, gli assembly verranno caricati come completamente attendibili in tutti i domini applicazione creati in tale computer.  L'elenco di nomi sicuri consente di prendere una decisione per ogni oggetto <xref:System.AppDomain>, offrendo quindi caratteristiche più restrittive.  
  
 È possibile usare l'overload del metodo [AppDomain.CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=fullName> per specificare il set di autorizzazioni per le applicazioni eseguite in un ambiente sandbox.  Questo overload consente di specificare il livello esatto di sicurezza dall'accesso di codice desiderato.  Gli assembly caricati in un oggetto <xref:System.AppDomain> usando questo overload possono solo disporre del set di autorizzazioni specificato o essere considerati completamente attendibili.  L'assembly viene considerato completamente attendibile se è presente nella Global Assembly Cache o elencato nel parametro della matrice `fullTrustAssemblies` \(<xref:System.Security.Policy.StrongName>\).  Solo gli assembly completamente attendibili devono essere aggiunti all'elenco `fullTrustAssemblies`.  
  
 L'overload ha la firma seguente:  
  
```  
AppDomain.CreateDomain( string friendlyName,  
                        Evidence securityInfo,  
                        AppDomainSetup info,  
                        PermissionSet grantSet,  
                        params StrongName[] fullTrustAssemblies);  
```  
  
 I parametri per l'overload del metodo [CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29> specificano il nome di <xref:System.AppDomain>, l'evidenza per <xref:System.AppDomain>, l'oggetto <xref:System.AppDomainSetup> che identifica la base dell'applicazione per l'ambiente sandbox, il set di autorizzazioni da usare e i nomi sicuri per gli assembly completamente attendibili.  
  
 Per motivi di sicurezza, la base dell'applicazione specificata nel parametro `info` non deve corrispondere alla base dell'applicazione host.  
  
 Per il parametro `grantSet`, è possibile specificare un set di autorizzazioni creato in modo esplicito o un set di autorizzazioni standard creato dal metodo <xref:System.Security.SecurityManager.GetStandardSandbox%2A>.  
  
 A differenza della maggior parte dei caricamenti di <xref:System.AppDomain>, l'evidenza per <xref:System.AppDomain> \(fornita dal parametro `securityInfo`\) non viene usata per determinare il set di autorizzazioni per gli assembly parzialmente attendibili.  Viene invece specificata in modo indipendente dal parametro `grantSet`.  L'evidenza può essere usata per altri scopi, ad esempio per determinare l'ambito dello spazio di memorizzazione isolato.  
  
### Per eseguire un'applicazione in un ambiente sandbox  
  
1.  Creare il set di autorizzazioni da concedere all'applicazione non attendibile.  L'autorizzazione minima che è possibile concedere è <xref:System.Security.Permissions.SecurityPermissionFlag>.  È anche possibile concedere autorizzazioni aggiuntive che si ritengono sicure per il codice non attendibile, ad esempio <xref:System.Security.Permissions.IsolatedStorageFilePermission>.  Il codice seguente crea un nuovo set di autorizzazioni con solo l'autorizzazione <xref:System.Security.Permissions.SecurityPermissionFlag>.  
  
    ```  
    PermissionSet permSet = new PermissionSet(PermissionState.None);  
    permSet.AddPermission(new SecurityPermission(SecurityPermissionFlag.Execution));  
    ```  
  
     In alternativa, è possibile usare un set di autorizzazioni denominato esistente, ad esempio Internet.  
  
    ```  
    Evidence ev = new Evidence();  
    ev.AddHostEvidence(new Zone(SecurityZone.Internet));  
    PermissionSet internetPS = SecurityManager.GetStandardSandbox(ev);  
    ```  
  
     Il metodo <xref:System.Security.SecurityManager.GetStandardSandbox%2A> restituisce un set di autorizzazioni `Internet` o un set di autorizzazioni `LocalIntranet`, a seconda dell'area nell'evidenza.  <xref:System.Security.SecurityManager.GetStandardSandbox%2A> crea inoltre autorizzazioni di identità per alcuni degli oggetti evidenza passati come riferimenti.  
  
2.  Firmare l'assembly contenente la classe host \(in questo esempio `Sandboxer`\) che chiama il codice non attendibile.  Aggiungere l'oggetto <xref:System.Security.Policy.StrongName> usato per firmare l'assembly alla matrice <xref:System.Security.Policy.StrongName> del parametro `fullTrustAssemblies` della chiamata a <xref:System.AppDomain.CreateDomain%2A>.  La classe host deve essere eseguita come completamente attendibile per consentire l'esecuzione del codice parzialmente attendibile o per offrire servizi per l'applicazione parzialmente attendibile.  Ecco come viene letto l'oggetto <xref:System.Security.Policy.StrongName> di un assembly:  
  
    ```  
    StrongName fullTrustAssembly = typeof(Sandboxer).Assembly.Evidence.GetHostEvidence<StrongName>();  
    ```  
  
     Non è necessario aggiungere gli assembly .NET Framework, come mscorlib e System. dll, all'elenco di elementi completamente attendibili, in quanto vengono caricati come completamente attendibili dalla Global Assembly Cache.  
  
3.  Inizializzare il parametro <xref:System.AppDomainSetup> del metodo <xref:System.AppDomain.CreateDomain%2A>.  Con questo parametro, è possibile controllare numerose impostazioni del nuovo oggetto <xref:System.AppDomain>.  La proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> è un'impostazione importante e deve essere diversa dalla proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> per l'oggetto <xref:System.AppDomain> dell'applicazione host.  Se le impostazioni di <xref:System.AppDomainSetup.ApplicationBase%2A> corrispondono, l'applicazione parzialmente attendibile può fare in modo che l'applicazione host carichi \(come completamente attendibile\) un'eccezione definita, che può quindi essere sfruttata.  Questo è un altro motivo per cui non è consigliabile l'uso di un elemento catch \(eccezione\).  Impostando la base dell'applicazione dell'host in modo diverso dalla base dell'applicazione in modalità sandbox, è possibile ridurre il rischio di exploit.  
  
    ```  
    AppDomainSetup adSetup = new AppDomainSetup();  
    adSetup.ApplicationBase = Path.GetFullPath(pathToUntrusted);  
    ```  
  
4.  Chiamare l'overload del metodo [CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29> per creare il dominio dell'applicazione usando i parametri specificati.  
  
     La firma per il metodo è la seguente:  
  
    ```  
    public static AppDomain CreateDomain(string friendlyName,   
        Evidence securityInfo, AppDomainSetup info, PermissionSet grantSet,   
        params StrongName[] fullTrustAssemblies)  
    ```  
  
     Informazioni aggiuntive:  
  
    -   Questo è l'unico overload del metodo <xref:System.AppDomain.CreateDomain%2A> che accetta un oggetto <xref:System.Security.PermissionSet> come parametro e pertanto l'unico overload che consente di caricare un'applicazione con un'impostazione di attendibilità parziale.  
  
    -   Il parametro `evidence` non viene usato per calcolare un set di autorizzazioni, ma per l'identificazione da parte di altre funzionalità di .NET Framework.  
  
    -   L'impostazione della proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> del parametro `info` è obbligatoria per questo overload.  
  
    -   Il parametro `fullTrustAssemblies` dispone della parola chiave `params`, pertanto non è necessario creare una matrice <xref:System.Security.Policy.StrongName>.  È possibile passare 0, 1 o più nomi sicuri come parametri.  
  
    -   Il codice per creare il dominio applicazione è il seguente:  
  
    ```  
    AppDomain newDomain = AppDomain.CreateDomain("Sandbox", null, adSetup, permSet, fullTrustAssembly);  
    ```  
  
5.  Caricare il codice nell'oggetto <xref:System.AppDomain> sandbox creato.  Questa operazione può essere eseguita nei due modi seguenti.  
  
    -   Chiamare il metodo <xref:System.AppDomain.ExecuteAssembly%2A> per l'assembly.  
  
    -   Usare il metodo <xref:System.Activator.CreateInstanceFrom%2A> per creare un'istanza di una classe derivata da <xref:System.MarshalByRefObject> nel nuovo oggetto <xref:System.AppDomain>.  
  
     Il secondo metodo è preferibile, in quanto consente di passare in modo più semplice i parametri alla nuova istanza di <xref:System.AppDomain>.  Il metodo <xref:System.Activator.CreateInstanceFrom%2A> offre due funzionalità importanti:  
  
    -   È possibile usare una codebase che punta a una posizione che non contiene l'assembly.  
  
    -   È possibile eseguire la creazione in un oggetto <xref:System.Security.CodeAccessPermission.Assert%2A> per l'attendibilità totale \(<xref:System.Security.Permissions.PermissionState?displayProperty=fullName>\), per poter creare un'istanza di una classe critica.  Ciò avviene ogni volta che l'assembly non dispone di contrassegni di trasparenza e viene caricato come completamente attendibile. È pertanto necessario prestare attenzione a creare solo codice attendibile con questa funzione e si consiglia di creare solo istanze di classi completamente attendibili nel nuovo dominio applicazione.  
  
    ```  
    ObjectHandle handle = Activator.CreateInstanceFrom(  
    newDomain, typeof(Sandboxer).Assembly.ManifestModule.FullyQualifiedName,  
           typeof(Sandboxer).FullName );  
    ```  
  
     Si noti che per creare un'istanza di una classe in un nuovo dominio, la classe deve estendere la classe <xref:System.MarshalByRefObject>.  
  
    ```  
    class Sandboxer:MarshalByRefObject  
    ```  
  
6.  Annullare il wrapping dell'istanza del nuovo dominio in un riferimento in questo dominio.  Questo riferimento viene usato per eseguire codice non attendibile.  
  
    ```  
    Sandboxer newDomainInstance = (Sandboxer) handle.Unwrap();  
    ```  
  
7.  Chiamare il metodo `ExecuteUntrustedCode` nell'istanza della classe `Sandboxer` appena creata.  
  
    ```  
    newDomainInstance.ExecuteUntrustedCode(untrustedAssembly, untrustedClass, entryPoint, parameters);  
    ```  
  
     Questa chiamata viene eseguita nel dominio applicazione in modalità sandbox, con autorizzazioni limitate.  
  
    ```  
    public void ExecuteUntrustedCode(string assemblyName, string typeName, string entryPoint, Object[] parameters)  
        {  
            //Load the MethodInfo for a method in the new assembly. This might be a method you know, or   
            //you can use Assembly.EntryPoint to get to the entry point in an executable.  
            MethodInfo target = Assembly.Load(assemblyName).GetType(typeName).GetMethod(entryPoint);  
            try  
            {  
                // Invoke the method.  
                target.Invoke(null, parameters);  
            }  
            catch (Exception ex)  
            {  
            //When information is obtained from a SecurityException extra information is provided if it is   
            //accessed in full-trust.  
                (new PermissionSet(PermissionState.Unrestricted)).Assert();  
                Console.WriteLine("SecurityException caught:\n{0}", ex.ToString());  
    CodeAccessPermission.RevertAssert();  
                Console.ReadLine();  
            }  
        }  
    ```  
  
     Viene usato <xref:System.Reflection> per ottenere un handle di un metodo nell'assembly parzialmente attendibile.  L'handle può essere usato per eseguire codice in modo sicuro con autorizzazioni minime.  
  
     Nel codice precedente, osservare l'oggetto <xref:System.Security.PermissionSet.Assert%2A> per l'autorizzazione di attendibilità totale prima di stampare <xref:System.Security.SecurityException>.  
  
    ```  
    new PermissionSet(PermissionState.Unrestricted)).Assert()  
    ```  
  
     L'asserzione di attendibilità totale viene usata per ottenere informazioni estese da <xref:System.Security.SecurityException>.  Senza l'oggetto <xref:System.Security.PermissionSet.Assert%2A>, il metodo <xref:System.Security.SecurityException.ToString%2A> di <xref:System.Security.SecurityException> individuerebbe la presenza di codice parzialmente attendibile nello stack e limiterebbe le informazioni restituite.  Ciò potrebbe causare problemi di sicurezza se il codice parzialmente attendibile potesse leggere tali informazioni, ma i rischi vengono attenuati non concedendo <xref:System.Security.Permissions.UIPermission>.  L'asserzione di attendibilità totale deve essere usata con cautela e solo quando si è certi di non consentire l'elevazione di codice parzialmente attendibile a codice completamente attendibile.  Di norma, non chiamare codice non considerato attendibile nella stessa funzione e dopo avere chiamato un'asserzione di attendibilità totale.  È consigliabile annullare sempre l'asserzione dopo averla usata.  
  
## Esempio  
 Nell'esempio seguente viene implementata la procedura della sezione precedente.  Nell'esempio un progetto denominato `Sandboxer` in una soluzione di Visual Studio contiene un progetto denominato `UntrustedCode`, che implementa la classe `UntrustedClass`.  Questo scenario presuppone che sia stato scaricato un assembly di librerie contenente un metodo che restituisce `true` o `false` per indicare se il numero fornito è un numero di Fibonacci.  Il metodo tenta invece di leggere un file dal computer.  L'esempio seguente mostra il codice non attendibile.  
  
```  
using System;  
using System.IO;  
namespace UntrustedCode  
{  
    public class UntrustedClass  
    {  
        // Pretend to be a method checking if a number is a Fibonacci  
        // but which actually attempts to read a file.  
        public static bool IsFibonacci(int number)  
        {  
           File.ReadAllText("C:\\Temp\\file.txt");  
           return false;  
        }  
    }  
}  
```  
  
 L'esempio seguente mostra il codice dell'applicazione `Sandboxer` che esegue il codice non attendibile.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Security;  
using System.Security.Policy;  
using System.Security.Permissions;  
using System.Reflection;  
using System.Runtime.Remoting;  
  
//The Sandboxer class needs to derive from MarshalByRefObject so that we can create it in another   
// AppDomain and refer to it from the default AppDomain.  
class Sandboxer : MarshalByRefObject  
{  
    const string pathToUntrusted = @"..\..\..\UntrustedCode\bin\Debug";  
    const string untrustedAssembly = "UntrustedCode";  
    const string untrustedClass = "UntrustedCode.UntrustedClass";  
    const string entryPoint = "IsFibonacci";  
    private static Object[] parameters = { 45 };  
    static void Main()  
    {  
        //Setting the AppDomainSetup. It is very important to set the ApplicationBase to a folder   
        //other than the one in which the sandboxer resides.  
        AppDomainSetup adSetup = new AppDomainSetup();  
        adSetup.ApplicationBase = Path.GetFullPath(pathToUntrusted);  
  
        //Setting the permissions for the AppDomain. We give the permission to execute and to   
        //read/discover the location where the untrusted code is loaded.  
        PermissionSet permSet = new PermissionSet(PermissionState.None);  
        permSet.AddPermission(new SecurityPermission(SecurityPermissionFlag.Execution));  
  
        //We want the sandboxer assembly's strong name, so that we can add it to the full trust list.  
        StrongName fullTrustAssembly = typeof(Sandboxer).Assembly.Evidence.GetHostEvidence<StrongName>();  
  
        //Now we have everything we need to create the AppDomain, so let's create it.  
        AppDomain newDomain = AppDomain.CreateDomain("Sandbox", null, adSetup, permSet, fullTrustAssembly);  
  
        //Use CreateInstanceFrom to load an instance of the Sandboxer class into the  
        //new AppDomain.   
        ObjectHandle handle = Activator.CreateInstanceFrom(  
            newDomain, typeof(Sandboxer).Assembly.ManifestModule.FullyQualifiedName,  
            typeof(Sandboxer).FullName  
            );  
        //Unwrap the new domain instance into a reference in this domain and use it to execute the   
        //untrusted code.  
        Sandboxer newDomainInstance = (Sandboxer) handle.Unwrap();  
        newDomainInstance.ExecuteUntrustedCode(untrustedAssembly, untrustedClass, entryPoint, parameters);  
    }  
    public void ExecuteUntrustedCode(string assemblyName, string typeName, string entryPoint, Object[] parameters)  
    {  
        //Load the MethodInfo for a method in the new Assembly. This might be a method you know, or   
        //you can use Assembly.EntryPoint to get to the main function in an executable.  
        MethodInfo target = Assembly.Load(assemblyName).GetType(typeName).GetMethod(entryPoint);  
        try  
        {  
            //Now invoke the method.  
            bool retVal = (bool)target.Invoke(null, parameters);  
        }  
        catch (Exception ex)  
        {  
            // When we print informations from a SecurityException extra information can be printed if we are   
            //calling it with a full-trust stack.  
            (new PermissionSet(PermissionState.Unrestricted)).Assert();  
            Console.WriteLine("SecurityException caught:\n{0}", ex.ToString());  
            CodeAccessPermission.RevertAssert();  
            Console.ReadLine();  
        }  
    }  
}  
  
```  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)
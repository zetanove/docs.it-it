---
title: "Applicazioni client protette | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6239592e-fa7d-4dea-9f00-d296d0048b01
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Applicazioni client protette
Le applicazioni sono costituite in genere da molte parti che è necessario proteggere da vulnerabilità che potrebbero causare la perdita di dati o compromettere in altro modo il sistema.  La creazione di interfacce utente protette consente di impedire molti problemi bloccando gli utenti non autorizzati prima che accedano ai dati o alle risorse del sistema.  
  
## Convalidare l'input dell'utente  
 Quando si crea un'applicazione che accede a dati, è opportuno presupporre che tutto l'input dell'utente sia dannoso fino a prova contraria.  In caso contrario, si espone l'applicazione a potenziali attacchi.  In .NET Framework sono incluse classi che consentono di applicare un dominio di valori per i controlli di input, ad esempio limitando il numero di caratteri che è possibile immettere.  Gli hook di evento consentono di scrivere procedure per verificare la validità dei valori.  I dati dell'input dell'utente possono essere convalidati e fortemente tipizzati, limitando l'esposizione di un'applicazione ad attacchi tramite script e di tipo SQL injection.  
  
> [!IMPORTANT]
>  È inoltre necessario convalidare l'input dell'utente nell'origine dati nonché nell'applicazione dati.  Un utente non autorizzato può scegliere di aggirare l'applicazione e attaccare direttamente l'origine dati.  
  
 [Security and User Input](../../../../docs/standard/security/security-and-user-input.md)  
 Viene descritto come gestire i bug di difficile individuazione e potenzialmente pericolosi che riguardano l'input dell'utente.  
  
 [Validating User Input in ASP.NET Web Pages](../Topic/Validating%20User%20Input%20in%20ASP.NET%20Web%20Pages.md)  
 Viene fornita una panoramica della convalida dell'input dell'utente tramite gli appositi controlli di ASP.NET.  
  
 [User Input in Windows Forms](../../../../docs/framework/winforms/user-input-in-windows-forms.md)  
 Vengono forniti collegamenti e informazioni per la convalida dell'input da mouse e tastiera nelle applicazioni Windows Form.  
  
 [Espressioni regolari di .NET Framework](../../../../docs/standard/base-types/regular-expressions.md)  
 Viene descritto come usare la classe <xref:System.Text.RegularExpressions.Regex> per verificare la validità dell'input dell'utente.  
  
## Applicazioni Windows  
 In passato, le applicazioni Windows venivano in genere eseguite con autorizzazioni complete.  Con .NET Framework viene fornita l'infrastruttura necessaria per limitare l'esecuzione di codice in un'applicazione Windows tramite la sicurezza dall'accesso di codice.  Questa funzionalità non è tuttavia sufficiente, da sola, a proteggere l'applicazione.  
  
 [Windows Forms Security](../../../../docs/framework/winforms/windows-forms-security.md)  
 Viene illustrato come proteggere le applicazioni Windows Form e vengono forniti collegamenti ad argomenti correlati.  
  
 [Windows Forms and Unmanaged Applications](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)  
 Viene descritto come interagire con applicazioni non gestite in un'applicazione Windows Form.  
  
 [ClickOnce Deployment for Windows Forms Applications](http://msdn.microsoft.com/it-it/34d8c770-48f2-460c-8d67-4ea5684511df)  
 Viene descritto come usare la distribuzione `ClickOnce` in un'applicazione Windows Form e ne vengono illustrate le implicazioni per la sicurezza.  
  
## Servizi Web ASP.NET e XML  
 In genere, nelle applicazioni ASP.NET è necessario limitare l'accesso ad alcune parti del sito Web e fornire meccanismi diversi per la protezione dei dati e la sicurezza del sito.  Questi collegamenti forniscono informazioni utili per la protezione dell'applicazione ASP.NET.  
  
 Un servizio Web XML fornisce dati che possono essere usati da un'applicazione ASP.NET, un'applicazione Windows Form o un altro servizio Web.  È necessario gestire la sicurezza per il servizio Web stesso così come quella per l'applicazione client.  
  
 Per altre informazioni, vedere le seguenti risorse.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[NIB: ASP.NET Security](http://msdn.microsoft.com/it-it/04b37532-18d9-40b4-8e5f-ee09a70b311d)|Viene illustrato come proteggere le applicazioni ASP.NET.|  
|[Securing XML Web Services Created Using ASP.NET](http://msdn.microsoft.com/it-it/354b2ab1-2782-4542-b32a-dc560178b90c)|Viene illustrato come implementare la sicurezza per un servizio Web ASP.NET.|  
|[Script Exploits Overview](../Topic/Script%20Exploits%20Overview.md)|Viene descritto come salvaguardarsi da attacchi tramite script, in cui si tenta di inserire caratteri dannosi in una pagina Web.|  
|[NIB:Basic Security Practices for ASP.NET Web Applications](http://msdn.microsoft.com/it-it/94a52ab8-731d-417e-b997-721baf43df38)|Informazioni generali sulla sicurezza e collegamenti ad ulteriori argomenti.|  
  
## Servizi remoti  
 Con .NET Remoting è possibile compilare facilmente applicazioni ampiamente distribuite, sia che i componenti dell'applicazione si trovino tutti nello stesso computer o dislocati in varie parti del mondo.  È possibile compilare applicazioni client che usano oggetti di altri processi nello stesso computer o in qualsiasi altro computer disponibile sulla rete.  È anche possibile usare .NET Remoting per comunicare con altri domini applicazione nello stesso processo.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Configuration of Remote Applications](http://msdn.microsoft.com/it-it/92c0c097-d984-4315-835b-7490ecdf1097)|Viene descritto come configurare le applicazioni remote per evitare problemi comuni.|  
|[Security in Remoting](http://msdn.microsoft.com/it-it/9574262c-d4b1-41c5-8600-24ff147c0add)|Vengono descritte l'autenticazione e la crittografia e sono riportati altri argomenti sulla sicurezza relativi ai servizi remoti.|  
|[Security and Remoting Considerations](../../../../docs/framework/misc/security-and-remoting-considerations.md)|Vengono descritti i problemi di sicurezza con gli oggetti protetti e l'uso di più domini di applicazioni.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Recommendations for Data Access Strategies](http://msdn.microsoft.com/it-it/72411f32-d12a-4de8-b961-e54fca7faaf5)   
 [Protezione delle applicazioni](../Topic/Securing%20Applications.md)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
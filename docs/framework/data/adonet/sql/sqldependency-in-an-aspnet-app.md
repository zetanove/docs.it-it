---
title: "SqlDependency in un&#39;applicazione ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# SqlDependency in un&#39;applicazione ASP.NET
Nell'esempio riportato in questa sezione viene illustrato l'uso di <xref:System.Data.SqlClient.SqlDependency> in modo indiretto sfruttando l'oggetto <xref:System.Web.Caching.SqlCacheDependency> di ASP.NET.  L'oggetto <xref:System.Web.Caching.SqlCacheDependency> usa un oggetto <xref:System.Data.SqlClient.SqlDependency> per ascoltare le notifiche e aggiornare correttamente la cache.  
  
> [!NOTE]
>  Nel codice di esempio si presuppone che le notifiche di query siano state abilitate eseguendo gli script descritti in [Abilitazione di notifiche di query](../../../../../docs/framework/data/adonet/sql/enabling-query-notifications.md).  
  
## Informazioni sull'applicazione di esempio  
 Nell'applicazione di esempio viene usata una singola pagina Web ASP.NET per visualizzare in un controllo <xref:System.Web.UI.WebControls.GridView> le informazioni sul prodotto disponibili nel database **AdventureWorks** di SQL Server.  Durante il caricamento della pagina, il codice scrive l'ora corrente in un controllo <xref:System.Web.UI.WebControls.Label>.  Viene quindi definito un oggetto <xref:System.Web.Caching.SqlCacheDependency> e vengono impostate le proprietà nell'oggetto <xref:System.Web.Caching.Cache> per archiviare i dati della cache per un massimo di tre minuti.  Viene quindi eseguita la connessione al database e vengono recuperati i dati.  Quando viene caricata la pagina e l'applicazione è in esecuzione, ASP.NET recupererà i dati dalla cache, come è possibile verificare osservando che l'ora della pagina rimane invariata.  Se i dati da monitorare cambiano, ASP.NET invalida la cache e ripopola il controllo `GridView` con nuovi dati, aggiornando l'ora visualizzata nel controllo `Label`.  
  
## Creazione dell'applicazione di esempio  
 Per creare ed eseguire l'applicazione di esempio, eseguire la procedura seguente:  
  
1.  Creare un nuovo sito Web ASP.NET.  
  
2.  Aggiungere un controllo <xref:System.Web.UI.WebControls.Label> e un controllo <xref:System.Web.UI.WebControls.GridView> alla pagina Default.aspx.  
  
3.  Aprire il modulo di classe della pagina e aggiungere le direttive seguenti:  
  
    ```vb  
  
    Option Strict On  
    Option Explicit On  
  
    Imports System.Data.SqlClient  
    ```  
  
    ```csharp  
    using System.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4.  Aggiungere il codice seguente nell'evento `Page_Load` della pagina:  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#1)]
     [!code-vb[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#1)]  
  
5.  Aggiungere due metodi di supporto, `GetConnectionString` e `GetSQL`.  La stringa di connessione definita usa la sicurezza integrata.  Sarà necessario verificare che l'account in uso disponga delle autorizzazioni del database richieste e che siano abilitate le notifiche nel database di esempio **AdventureWorks**.  Per altre informazioni, vedere [Special Considerations When Using Query Notifications](http://msdn.microsoft.com/it-it/a83c8dc8-4fb9-4ffd-a2a5-c07cf4a203c7).  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#2)]
     [!code-vb[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#2)]  
  
### Verifica dell'applicazione  
 L'applicazione memorizza nella cache i dati visualizzati sul form Web e li aggiorna ogni tre minuti in assenza di attività.  Se il database viene modificato, la cache viene immediatamente aggiornata.  Eseguire l'applicazione da Visual Studio per caricare la pagina nel browser.  L'ora di aggiornamento della cache visualizzata indica quando la cache è stata aggiornata per l'ultima volta.  Attendere tre minuti e quindi aggiornare la pagina, in modo da causare un evento postback.  Notare che l'ora visualizzata nella pagina è cambiata.  Se si aggiorna la pagina prima dei tre minuti, l'ora visualizzata nella pagina rimarrà la stessa.  
  
 A questo punto aggiornare i dati nel database, usando un comandi UPDATE Transact\-SQL, quindi aggiornare la pagina.  Adesso l'ora visualizzata indica che la cache è stata aggiornata automaticamente con i nuovi dati del database.  Notare che, anche se la cache è stata aggiornata, l'ora visualizzata nella pagina non cambia finché non si verifica un evento postback.  
  
## Vedere anche  
 [Notifiche di query in SQL Server](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
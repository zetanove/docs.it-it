---
title: "GUID di cartella nota per percorsi personalizzati della finestra di dialogo File. | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Percorsi personalizzati, GUID della cartella nota"
  - "GUID della cartella nota, Percorsi personalizzati"
  - "GUID della cartella nota di Windows Vista, Percorsi personalizzati"
ms.assetid: d8d8b544-8b4d-4da5-ba3a-b05e93244778
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# GUID di cartella nota per percorsi personalizzati della finestra di dialogo File.
Utilizzare <xref:System.Guid> per specificare una cartella nota di [!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)] quando si aggiungono cartelle a una raccolta <xref:System.Windows.Forms.FileDialog.CustomPlaces%2A>.  Per i GUID di cartella nota non viene effettuata la distinzione tra maiuscole e minuscole e vengono definiti nel file KnownFolders.h di [!INCLUDE[winSDK](../../../../includes/winsdk-md.md)].  
  
> [!NOTE]
>  In alcuni casi, una cartella nota aggiunta a <xref:System.Windows.Forms.FileDialogCustomPlacesCollection> non verrà visualizzata nell'area **Collegamenti preferiti**.  Ad esempio, se la cartella nota specificata non è presente nel computer che sta eseguendo l'applicazione, non viene visualizzata.  
  
## Elenco di GUID  
 Nella tabella seguente sono elencate le cartelle note di [!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)] e i relativi <xref:System.Guid> associati.  
  
 AddNewPrograms  
 DE61D971\-5EBC\-4F02\-A3A9\-6C82895E5C04  
  
 AdminTools  
 724EF170\-A42D\-4FEF\-9F26\-B60E846FBA4F  
  
 AppDataLow  
 A520A1A4\-1780\-4FF6\-BD18\-167343C5AF16  
  
 AppUpdates  
 A305CE99\-F527\-492B\-8B1A\-7E76FA98D6E4  
  
 CDBurning  
 9E52AB10\-F80D\-49DF\-ACB8\-4330F5687855  
  
 ChangeRemovePrograms  
 DF7266AC\-9274\-4867\-8D55\-3BD661DE872D  
  
 CommonAdminTools  
 D0384E7D\-BAC3\-4797\-8F14\-CBA229B392B5  
  
 CommonOEMLinks  
 C1BAE2D0\-10DF\-4334\-BEDD\-7AA20B227A9D  
  
 CommonPrograms  
 0139D44E\-6AFE\-49F2\-8690\-3DAFCAE6FFB8  
  
 CommonStartMenu  
 A4115719\-D62E\-491D\-AA7C\-E74B8BE3B067  
  
 CommonStartup  
 82A5EA35\-D9CD\-47C5\-9629\-E15D2F714E6E  
  
 CommonTemplates  
 B94237E7\-57AC\-4347\-9151\-B08C6C32D1F7  
  
 Computer  
 0AC0837C\-BBF8\-452A\-850D\-79D08E667CA7  
  
 Conflitto  
 4BFEFB45\-347D\-4006\-A5BE\-AC0CB0567192  
  
 Connessioni  
 6F0CD92B\-2E97\-45D1\-88FF\-B0D186B8DEDD  
  
 Contatti  
 56784854\-C6CB\-462B\-8169\-88E350ACB882  
  
 ControlPanel  
 82A74AEB\-AEB4\-465C\-A014\-D097EE346D63  
  
 Cookie  
 2B0F765D\-C0E9\-4171\-908E\-08A611B84FF6  
  
 Desktop  
 B4BFCC3A\-DB2C\-424C\-B029\-7FE99A87C641  
  
 Documenti  
 FDD39AD0\-238F\-46AF\-ADB4\-6C85480369C7  
  
 Download  
 374DE290\-123F\-4565\-9164\-39C4925E467B  
  
 Preferiti  
 1777F761\-68AD\-4D8A\-87BD\-30B759FA33DD  
  
 Tipi di carattere  
 FD228CB7\-AE11\-4AE3\-864C\-16F3910AB8FE  
  
 Giochi  
 CAC52C1A\-B53D\-4EDC\-92D7\-6B2E8AC19434  
  
 GameTasks  
 054FAE61\-4DD8\-4787\-80B6\-090220C4B700  
  
 Cronologia  
 D9DC8A3B\-B784\-432E\-A781\-5A1130A75963  
  
 Internet  
 4D9F7874\-4E0C\-4904\-967B\-40B0D20C3E4B  
  
 InternetCache  
 352481E8\-33BE\-4251\-BA85\-6007CAEDCF9D  
  
 Collegamenti  
 BFB9D5E0\-C6A9\-404C\-B2B2\-AE6DB6AF4968  
  
 LocalAppData  
 F1B32785\-6FBA\-4FCF\-9D55\-7B8E7F157091  
  
 LocalizedResourcesDir  
 2A00375E\-224C\-49DE\-B8D1\-440DF7EF3DDC  
  
 Musica  
 4BD8D571\-6D19\-48D3\-BE97\-422220080E43  
  
 NetHood  
 C5ABBF53\-E17F\-4121\-8900\-86626FC2C973  
  
 Network  
 D20BEEC4\-5CA8\-4905\-AE3B\-BF251EA09B53  
  
 OriginalImages  
 2C36C0AA\-5812\-4B87\-BFD0\-4CD0DFB19B39  
  
 PhotoAlbums  
 69D2CF90\-FC33\-4FB7\-9A0C\-EBB0F0FCB43C  
  
 Immagini  
 33E28130\-4E1E\-4676\-835A\-98395C3BC3BB  
  
 Playlist  
 DE92C1C7\-837F\-4F69\-A3BB\-86E631204A23  
  
 Stampanti  
 76FC4E2D\-D6AD\-4519\-A663\-37BD56068185  
  
 PrintHood  
 9274BD8D\-CFD1\-41C3\-B35E\-B13F55A758F4  
  
 Profilo  
 5E6C858F\-0E22\-4760\-9AFE\-EA3317B67173  
  
 ProgramData  
 62AB5D82\-FDC1\-4DC3\-A9DD\-070D1D495D97  
  
 ProgramFiles  
 905E63B6\-C1BF\-494E\-B29C\-65B732D3D21A  
  
 ProgramFilesCommon  
 F7F1ED05\-9F6D\-47A2\-AAAE\-29D317C6F066  
  
 ProgramFilesCommonX64  
 6365D5A7\-0F0D\-45E5\-87F6\-0DA56B6A4F7D  
  
 ProgramFilesCommonX86  
 DE974D24\-D9C6\-4D3E\-BF91\-F4455120B917  
  
 ProgramFilesX64  
 6D809377\-6AF0\-444B\-8957\-A3773F02200E  
  
 ProgramFilesX86  
 7C5A40EF\-A0FB\-4BFC\-874A\-C0F2E0B9FA8E  
  
 Programmi  
 A77F5D77\-2E2B\-44C3\-A6A2\-ABA601054A51  
  
 Public  
 DFDF76A2\-C82A\-4D63\-906A\-5644AC457385  
  
 PublicDesktop  
 C4AA340D\-F20F\-4863\-AFEF\-F87EF2E6BA25  
  
 PublicDocuments  
 ED4824AF\-DCE4\-45A8\-81E2\-FC7965083634  
  
 PublicDownloads  
 3D644C9B\-1FB8\-4F30\-9B45\-F670235F79C0  
  
 PublicGameTasks  
 DEBF2536\-E1A8\-4C59\-B6A2\-414586476AEA  
  
 PublicMusic  
 3214FAB5\-9757\-4298\-BB61\-92A9DEAA44FF  
  
 PublicPictures  
 B6EBFB86\-6907\-413C\-9AF7\-4FC2ABF07CC5  
  
 PublicVideos  
 2400183A\-6185\-49FB\-A2D8\-4A392A602BA3  
  
 QuickLaunch  
 52A4F021\-7B75\-48A9\-9F6B\-4B87A210BC8F  
  
 Recente  
 AE50C081\-EBD2\-438A\-8655\-8A092E34987A  
  
 RecordedTV  
 BD85E001\-112E\-431E\-983B\-7B15AC09FFF1  
  
 RecycleBin  
 B7534046\-3ECB\-4C18\-BE4E\-64CD4CB7D6AC  
  
 ResourceDir  
 8AD10C31\-2ADB\-4296\-A8F7\-E4701232C972  
  
 RoamingAppData  
 3EB685DB\-65F9\-4CF6\-A03A\-E3EF65729F3D  
  
 SampleMusic  
 B250C668\-F57D\-4EE1\-A63C\-290EE7D1AA1F  
  
 SamplePictures  
 C4900540\-2379\-4C75\-844B\-64E6FAF8716B  
  
 SamplePlaylists  
 15CA69B3\-30EE\-49C1\-ACE1\-6B5EC372AFB5  
  
 SampleVideos  
 859EAD94\-2E85\-48AD\-A71A\-0969CB56A6CD  
  
 SavedGames  
 4C5C32FF\-BB9D\-43B0\-B5B4\-2D72E54EAAA4  
  
 SavedSearches  
 7D1D3A04\-DEBB\-4115\-95CF\-2F29DA2920DA  
  
 SEARCH\_CSC  
 EE32E446\-31CA\-4ABA\-814F\-A5EBD2FD6D5E  
  
 SEARCH\_MAPI  
 98EC0E18\-2098\-4D44\-8644\-66979315A281  
  
 SearchHome  
 190337D1\-B8CA\-4121\-A639\-6D472D16972A  
  
 SendTo  
 8983036C\-27C0\-404B\-8F08\-102D10DCFD74  
  
 SidebarDefaultParts  
 7B396E54\-9EC5\-4300\-BE0A\-2482EBAE1A26  
  
 SidebarParts  
 A75D362E\-50FC\-4FB7\-AC2C\-A8BEAA314493  
  
 StartMenu  
 625B53C3\-AB48\-4EC1\-BA1F\-A1EF4146FC19  
  
 Avvio  
 B97D20BB\-F46A\-4C97\-BA10\-5E3608430854  
  
 SyncManager  
 43668BF8\-C14E\-49B2\-97C9\-747784D784B7  
  
 SyncResults  
 289A9A43\-BE44\-4057\-A41B\-587A76D7E7F9  
  
 SyncSetup  
 0F214138\-B1D3\-4A90\-BBA9\-27CBC0C5389A  
  
 Sistema  
 1AC14E77\-02E7\-4E5D\-B744\-2EB1AE5198B7  
  
 SystemX86  
 D65231B0\-B2F1\-4857\-A4CE\-A8E7C6EA7D27  
  
 Modelli  
 A63293E8\-664E\-48DB\-A079\-DF759E0509F7  
  
 TreeProperties  
 5B3749AD\-B49F\-49C1\-83EB\-15370FBD4882  
  
 UserProfiles  
 0762D272\-C50A\-4BB0\-A382\-697DCD729B80  
  
 UsersFiles  
 F3CE0F7C\-4901\-4ACC\-8648\-D5D44B04EF8F  
  
 Video  
 18989B1D\-99B5\-455B\-841C\-AB7C74E4DDFC  
  
 Windows  
 F38BF404\-1D43\-42F2\-9305\-67DE0B28FC23  
  
## Vedere anche  
 <xref:System.Windows.Forms.FileDialogCustomPlace>   
 [Procedura: aggiungere un percorso personalizzato a una finestra di dialogo File](../../../../docs/framework/winforms/controls/how-to-add-a-custom-place-to-a-file-dialog-box.md)
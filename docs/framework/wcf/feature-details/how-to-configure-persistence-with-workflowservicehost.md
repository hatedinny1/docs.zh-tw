---
title: "HOW TO：以 WorkflowServiceHost 設定持續性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# HOW TO：以 WorkflowServiceHost 設定持續性
本主題描述如何設定 SQL 工作流程執行個體存放區功能，透過使用組態檔以啟用裝載於 <xref:System.ServiceHost.Activities.WorkflowServiceHost> 中之工作流程的持續性。  使用 SQL 工作流程執行個體存放區功能前，您必須建立一個用於保存工作流程執行個體的 SQL 資料庫。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][HOW TO：啟用工作流程與工作流程服務的 SQL 持續性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).  
  
### 若要在組態中設定 SQL 工作流程執行個體存放區  
  
1.  您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過 XML 組態變更設定。  下列組態範例示範如何使用組態檔中的 \<`sqlWorkflowInstanceStore`\> 行為項目來設定 SQL 工作流程執行個體存放區。  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore   
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"   
                 runnableInstancesDetectionPeriod="00:00:05">  
            <sqlWorkflowInstanceStore/>  
        </behavior>  
    </serviceBehaviors>  
  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何設定 SQL 工作流程執行個體存放區的詳細資訊，請參閱 [HOW TO：啟用工作流程與工作流程服務的 SQL 持續性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] \<`sqlWorkflowInstanceStore`\> 行為項目個別設定的詳細資訊，請參閱 [SQL 工作流程執行個體存放區](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  Windows Server App Fabric 會提供它自己的持續性存放區。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Windows Server App Fabric 持續性概念](http://go.microsoft.com/fwlink/?LinkId=193121)。  
  
    > [!NOTE]
    >  上述組態範例會使用簡化的組態。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [簡化的組態](../../../../docs/framework/wcf/simplified-configuration.md)  
  
### 若要在程式碼中設定 SQL 工作流程執行個體存放區  
  
1.  您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過程式碼變更設定。  下列範例示範如何使用程式碼中的 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行為項目來設定 SQL 工作流程執行個體存放區。  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何設定 SQL 工作流程執行個體存放區的詳細資訊，請參閱 [HOW TO：啟用工作流程與工作流程服務的 SQL 持續性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行為元素個別設定的詳細資訊，請參閱 [SQL 工作流程執行個體存放區](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  Windows Server App Fabric 會提供它自己的持續性存放區。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Windows Server App Fabric 持續性概念](http://go.microsoft.com/fwlink/?LinkId=193121)。  
  
    > [!NOTE]
    >  上述組態範例會使用簡化的組態。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [簡化的組態](../../../../docs/framework/wcf/simplified-configuration.md)  
  
     如需如何以程式設計方式設定持續性的範例，請參閱 [HOW TO：啟用工作流程與工作流程服務的持續性](../../../../docs/framework/windows-workflow-foundation//how-to-enable-persistence-for-workflows-and-workflow-services.md)。  
  
## 請參閱  
 [工作流程服務](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [工作流程持續性](../../../../docs/framework/windows-workflow-foundation//workflow-persistence.md)   
 [Windows Server App Fabric 持續性概念](http://go.microsoft.com/fwlink/?LinkId=193121)
---
title: Modify controller and client services accounts
titleSuffix: SQL Server Distributed Replay
description: Learn how to modify the Distributed Replay controller and client service accounts, and then reapply the access control lists.
ms.prod: sql
ms.technology: distributed-replay
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 06/20/2022
monikerRange: ">= sql-server-2016 || >= sql-server-linux-2017"
---

# Modify the controller and client services accounts

[!INCLUDE [sqlserver2016-2019-only](../../includes/applies-to-version/sqlserver2016-2019-only.md)]

[!INCLUDE [distributed-replay-sql-server-2022](../../includes/distributed-replay-sql-server-2022.md)]

In this topic, you'll learn how to modify the Distributed Replay controller and client service accounts, and then reapply the access control lists (ACLs).

## To start or stop the Distributed Replay services using Computer Management

1. On the computer on which the Distributed Replay services are installed, from the command prompt, type **dcomcnfg**.

2. Double-click **Services**, scroll down and right-click **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay \<service name>**, and then click **Start** or **Stop**.

### To modify the Distributed Replay controller service

1. On the controller computer, stop the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay controller service.

2. Under **Services**, right-click **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller**, and then select **Properties**.

3. In the **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller Properties** window, on the **Log On** tab, select **This account**, type or select **Browse** to enter the new logon account, and then select **OK**.

     > [!IMPORTANT]  
     > When you configure Distributed Replay Controller, you can specify one or more user accounts that will be used to run the Distributed Replay Client services. The following is the list of supported accounts:

    - Domain user account

    - User created local user account

    - Administrator

    - Virtual account and MSA (Managed Service Account)

    - Network Services, Local Services, and System

     Group accounts (local or domain) and other built-in accounts (like Everyone) aren't accepted.

4. Start the Distributed Replay controller service.

### To modify the Distributed Replay client service

1. Before you modify the Distributed Replay client service, make sure the client service account you're changing was specified during setup (in the CTLRUSERS parameter on the controller computer). If the client service account you're changing wasn't specified during setup, you must perform the following steps first:

    1. Stop the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay controller service.

    2. On the controller computer on which the controller service is installed, from the command prompt, type **dcomcnfg**.

    3. In the **Component Services** window, navigate to **Console Root -> Component Services -> Computers -> My Computer -> DCOM Config ->DReplayController**.

    4. Right-click **DReplayController**, and then click **Properties**.

    5. In the **DReplayController Properties** window, on the **Security** tab, select **Edit** in the **Launch and Activation Permissions** section.

    6. Grant the new client service logon account **Local and Remote activation** permissions, and then select **OK**.

    7. Select **Edit** in the **Access Permissions** section, and grant the new client service logon account **Local and Remote access** permissions, and then select **OK**.

    8. Select **OK** to close the **DReplayController Properties** window.

    9. On the controller computer, add the changed client service logon account to the **Distributed COM Users** group.

    10. Start the SQL Server Distributed Replay controller service.

2. Stop the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay client service.

3. In the **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client Properties** window, on the **Log On** tab, select **This account**, type or select **Browse** to enter the new logon account, and then select **OK**.

4. Start the Distributed Replay client service.

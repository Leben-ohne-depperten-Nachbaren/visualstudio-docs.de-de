---
title: Zugreifen auf private Azure-Clouds
description: Erfahren Sie, wie Sie mithilfe von Visual Studio auf private Cloudressourcen zugreifen.
author: ghogen
manager: jillfra
assetId: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.custom: seodec18
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/13/2017
ms.author: ghogen
ms.openlocfilehash: 5f9ea7ac26742b0fc1c116dfe53e941f93358221
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2019
ms.locfileid: "55946833"
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Zugreifen auf private Azure-Clouds mit Visual Studio

Visual Studio unterstützt standardmäßig REST-Endpunkte der Azure-Cloud. In diesem Artikel erfahren Sie, wie Sie über das Zertifikat der privaten Cloud auf die private Cloud in Visual Studio zugreifen und mit dieser interagieren.

1. Laden Sie im Azure-Portal für die private Cloud die Datei mit den Veröffentlichungseinstellungen herunter, oder wenden Sie sich an Ihren Administrator, um eine Datei mit Veröffentlichungseinstellungen zu erhalten. (Die Datei hat die Erweiterung `.publishsettings`.)

1. Klicken Sie in Visual Studio im **Server-Explorer** mit der rechten Maustaste auf den Knoten **Azure**, und wählen Sie die Option **Abonnements verwalten und filtern** aus.

    ![Befehl „Abonnements verwalten“](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. Wählen Sie im Dialogfeld **Microsoft Azure-Abonnements verwalten** die Registerkarte **Zertifikate** und dann **Importieren** aus.

    ![Importieren von Azure-Zertifikaten](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. Wählen Sie im Dialogfeld **Microsoft Azure-Abonnements importieren** die Option **Durchsuchen** aus.

    ![Schaltfläche „Durchsuchen“ im Dialogfeld „Microsoft Azure-Abonnements importieren“](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. Navigieren Sie im Dialogfeld **Öffnen** zu dem Verzeichnis, in dem Sie die Datei mit den Veröffentlichungseinstellungen gespeichert haben, markieren Sie die Datei, und wählen Sie dann **Öffnen** aus.

    ![Auswählen der Datei mit den Veröffentlichungseinstellungen](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Kehren Sie zum Dialogfeld **Microsoft Azure-Abonnements importieren** zurück, und wählen Sie dort die Option **Importieren** aus.

    ![Importieren der Datei mit den Veröffentlichungseinstellungen](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Die Zertifikate aus der Datei mit den Veröffentlichungseinstellungen werden in Visual Studio importiert, und Sie können nun mit den Ressourcen der privaten Cloud interagieren.
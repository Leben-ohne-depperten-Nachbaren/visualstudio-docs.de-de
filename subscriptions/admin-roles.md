---
title: Superadministrator- und Administratorrolle im Verwaltungsportal
author: evanwindom
ms.author: lank
manager: lank
ms.date: 08/21/2019
ms.topic: conceptual
description: Erfahren Sie mehr über die Superadministrator- und Administratorrolle und das Zuweisen von Administratoren.
ms.openlocfilehash: 1beda505008815b87a0de98ee597d7b5ec97693d
ms.sourcegitcommit: c90a998716b3dfa614dedc61a1bea515364efbec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000940"
---
# <a name="super-admins-and-administrators-for-visual-studio-subscription-agreements"></a>Superadministratoren und Administratoren für Visual Studio-Abonnementverträge

Im neuen Portal zur Verwaltung von Visual Studio-Abonnements für Kunden mit Volumenlizenzen gibt es zwei verschiedene Rollen. Diese entsprechen den Rollen „Primary/Notices Contact“ (Hauptkontakt) und „Subscriptions Manager“ (Abonnementverwalter), die früher im VLSC verfügbar waren.

**Superadministratoren:** Bei der Ersteinrichtung einer Organisation wird der Hauptkontakt standardmäßig zum Superadministrator. Der primäre Kontakt kann weitere Superadministratoren oder Administratoren zuweisen. Ein Superadministrator kann andere Administratoren sowie Abonnenten hinzufügen und entfernen. Wenn im System mehr als zwei Superadministratoren existieren, kann jeder Superadministrator alle anderen bis auf die letzten zwei löschen, da diese aus Sicherheitsgründen nicht gelöscht werden können.

**Administratoren:** Administratoren können nur von einem Superadministrator zugewiesen werden. Ein Administrator kann ausschließlich Abonnenten innerhalb der Verträge verwalten, die der Superadministrator diesem zuweist.

## <a name="assigning-administrators"></a>Zuweisen von Administratoren
So weisen Sie neue Administratoren zu:
1. Melden Sie sich bei https://manage.visualstudio.com mit einer E-Mail-Adresse an, der die Rolle des Superadministrators entsprechend dem Vertrag zugewiesen ist, über den die Abonnements erworben wurden.
2. Klicken Sie auf die Registerkarte **Administratoren verwalten**.
3. Klicken Sie auf **Hinzufügen**.
   > [!div class="mx-imgBorder"]
   > ![Hinzufügen von Administratoren](_img/admin-roles/add-admins.png)
4. Füllen Sie das Formular mit den Informationen des neuen Administrators aus.  
   > [!div class="mx-imgBorder"]
   > ![Formular „Administrator hinzufügen“](_img/admin-roles/add-form.png)

   > [!NOTE]
   > Wenn dieser Administrator in der Lage sein soll, weitere Administratoren zuzuweisen, müssen Sie das Kontrollkästchen neben **Super Admin** (Superadministrator) aktivieren.

5. Klicken Sie auf **Hinzufügen**, um den neuen Administrator zuzuweisen. Dieser erhält dann eine E-Mail, in der er aufgefordert wird, sich beim Portal anzumelden.  

## <a name="resources"></a>Ressourcen
- [Support für die Verwaltung von Visual Studio und Abonnements](https://visualstudio.microsoft.com/support/support-overview-vs)

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie, wie Sie [Abonnements zuweisen](assign-license.md).
- Erfahren Sie mehr über die unterschiedlichen [Abonnementvorteile](https://visualstudio.microsoft.com/vs/benefits/).
- [Festlegen von Vereinbarungseinstellungen](admin-prefs.md) 



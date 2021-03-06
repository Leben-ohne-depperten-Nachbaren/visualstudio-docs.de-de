---
title: Das Anfügen an den Prozess ist nicht möglich | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.remote.unable2attach
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22d798d30d09cb509f53d093ae61bb1a02b414ec
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72728878"
---
# <a name="unable-to-attach-to-the-process"></a>Anfügen an den Prozess nicht möglich
Anfügen an den Prozess nicht möglich. Der Debuggerkomponente auf dem Server wurde beim Herstellen einer Verbindung zu diesem Computer der Zugriff verweigert.

 Es gibt zwei gängige Szenarios, durch die dieser Fehler verursacht wird:

 **Szenario 1:** Auf Computer A wird Windows XP ausgeführt. Auf Computer B wird Windows Server 2003 ausgeführt. Die Registrierung auf Computer B enthält den folgenden DWORD-Wert:

 `HKLM\Software\Microsoft\MachineDebugManager\AllowLaunchAsOtherUser=1`

 Benutzer 1 startet eine Terminal Server-Sitzung (Sitzung 1) auf Computer B und ruft in dieser Sitzung eine verwaltete Anwendung auf.

 Benutzer 2, der auf beiden Computern Administrator ist, ist auf Computer A angemeldet. Von dort aus versucht er, eine Anwendung an eine Anwendung anzufügen, die in Sitzung 1 auf Computer B ausgeführt wird.

 **Szenario 2:** Ein Benutzer hat sich in derselben Arbeitsgruppe unter Verwendung desselben Kennworts bei zwei Computern (A und B) angemeldet. Der Debugger wird auf Computer a ausgeführt und versucht, eine Verbindung mit einer verwalteten Anwendung herzustellen, die auf Computer B ausgeführt wird. Computer A verfügt über **Netzwerk Zugriff: Freigabe-und Sicherheitsmodell für lokale Konten** , die auf **Gast**festgelegt sind.

### <a name="to-solve-scenario-1"></a>So lösen Sie Szenario 1

- Führen Sie den Debugger und die verwaltete Anwendung unter Verwendung desselben Benutzerkontonamens und Kennworts aus.

### <a name="to-solve-scenario-2"></a>So lösen Sie Szenario 2

1. Wählen Sie im Menü **Start** die **Systemsteuerung** aus.

2. Doppelklicken Sie in der Systemsteuerung auf **Verwaltung**.

3. Doppelklicken Sie im Fenster „Verwaltung“ auf **Lokale Sicherheitsrichtlinie**.

4. Wählen Sie im Fenster „Lokale Sicherheitsrichtlinie“ die Option **Lokale Richtlinien**.

5. Doppelklicken Sie in der Spalte **Richtlinien** auf die Option **Netzwerkzugriff: Modell für gemeinsame Nutzung und Sicherheitsmodell für lokale Konten**.

6. Ändern Sie im Dialogfeld **Netzwerkzugriff: Modell für gemeinsame Nutzung und Sicherheitsmodell für lokale Konten** die lokale Sicherheitseinstellung in **Klassisch**, und klicken Sie auf **OK**.

    > [!CAUTION]
    > Das Ändern des Sicherheitsmodells in Klassisch kann zu unerwünschtem Zugriff auf freigegebene Dateien und DCOM-Komponenten führen. Wenn Sie diese Änderung vornehmen, kann sich ein Remotebenutzer mit Ihrem lokalen Benutzerkonto anstatt als Gast authentifizieren. Wenn ein Remote Benutzer mit dem Benutzernamen und dem Kennwort übereinstimmt, kann dieser Benutzer auf alle Ordner oder DCOM-Objekte zugreifen, die Sie freigegeben haben. Wenn Sie dieses Sicherheitsmodell verwenden, stellen Sie sicher, dass alle Benutzerkonten auf dem Computer über sichere Kenn Wörter verfügen, oder richten Sie eine isolierte Netzwerk Insel für das Debugging und die debuggten Computer ein, um nicht autorisierten Zugriff zu verhindern.

7. Schließen Sie alle Fenster.

## <a name="see-also"></a>Siehe auch
- [Debuggereinstellungen und -vorbereitung](../debugger/debugger-settings-and-preparation.md)
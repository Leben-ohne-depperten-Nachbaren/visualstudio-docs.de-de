---
title: -Out („devenv.exe“) | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio], builds
- Devenv, /out switch
- builds [Visual Studio], logs
- error logs [Visual Studio], command-line build errors
- error logs [Visual Studio]
- /out Devenv switch
- out Devenv switch
- builds [Visual Studio], errors
- output files, build errors
ms.assetid: 9002d8c2-36d4-451c-b489-8f01932f31f7
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 075746353440462a66133cd83ed9158470d8de5b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: de-DE
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662200"
---
# <a name="out-devenvexe"></a>/Out (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Gibt eine Datei an, die Fehler speichern und anzeigen soll, wenn Sie eine Projektmappe ausführen, erstellen, erneut erstellen oder bereitstellen.

## <a name="syntax"></a>Syntax

```
devenv /out FileName
```

## <a name="arguments"></a>Argumente
 `FileName` ist erforderlich. Der Pfad und der Name der Datei, die beim Erstellen einer ausführbaren Datei Fehler empfangen soll.

## <a name="remarks"></a>Anmerkungen
 Wenn ein nicht vorhandener Dateiname angegeben wird, wird die Datei automatisch erstellt. Wenn die Datei bereits vorhanden ist, werden die Ergebnisse an die vorhandenen Inhalte der Datei angefügt.

 Buildfehler in der Befehlszeile werden im **Befehlsfenster** und der Solution Builder-Ansicht des **Ausgabefensters** angezeigt. Diese Option erweist sich als nützlich, wenn Sie unbeaufsichtigte Builds ausführen und die Ergebnisse benötigen.

## <a name="example"></a>Beispiel
 In diesem Beispiel wird `MySolution` ausgeführt, und es werden Fehler in die `MyErrorLog.txt`-Datei geschrieben.

```
devenv /run "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /out "C:\MyErrorLog.txt"
```

## <a name="see-also"></a>Siehe auch
 Debug- [Befehls Zeilenschalter](../../ide/reference/devenv-command-line-switches.md) [/Run ("abvenv. exe")](../../ide/reference/run-devenv-exe.md) [/Build (](../../ide/reference/build-devenv-exe.md) "abvenv. exe") [/Rebuild (](../../ide/reference/rebuild-devenv-exe.md) "") [("](../../ide/reference/deploy-devenv-exe.md) ")

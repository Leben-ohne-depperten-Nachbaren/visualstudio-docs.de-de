---
title: Beim Kontaktieren des Remotecomputers ist ein DCOM-Fehler aufgetreten. Der Zugriff wird verweigert. | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.dcom_access_denied
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, DCOM error
- remote DCOM access denied error
- DCOM, access errors
ms.assetid: 9d7dfc1b-9fe0-4f54-9c50-9c0e0f8358c5
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0157b1ade2c38a2c10920b9674d7c9a58ac036b2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156528"
---
# <a name="a-dcom-error-occurred-trying-to-contact-the-remote-computer-access-is-denied"></a>Beim Kontaktieren des Remotecomputers ist ein DCOM-Fehler aufgetreten. Der Zugriff wird verweigert.
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Remotedebugging verwendet DCOM für die Kommunikation zwischen dem lokalen und dem Remotecomputer, wenn eine der folgenden Situationen vorliegt:  
  
- Der Debugger ist auf **Systemeigenen Kompatibilitätsmodus verwenden** festgelegt, oder auf der Seite **Extras / Optionen / Debugging** ist **Verwalteter Kompatibilitätsmodus** aktiviert.  
  
- Sie debuggen verwalteten C++-Code (C++/CLI).  
  
- In Visual Studio 2013 ist auf der Seite **Extras / Optionen / Debugging** die Option **Systemeigenes Bearbeiten und Fortfahren aktivieren** aktiviert.  
  
- Einige Debuggingszenarien von Drittanbietern  
  
  Dieser Fehler tritt auf, wenn der Visual Studio-Prozess sich nicht über DCOM beim Remotedebuggerprozess authentifizieren kann (oder die angegebenen Anmeldeinformationen für unzureichend angesehen wurden). Das Problem kann mit einer oder zwei der folgenden Methoden möglicherweise umgangen werden:  
  
- Deaktivieren Sie  **Systemeigenen Kompatibilitätsmodus verwenden** und **Verwalteter Kompatibilitätsmodus**.  
  
- Deaktivieren Sie in Visual Studio 2013 die Option **Systemeigenes Bearbeiten und Fortfahren aktivieren**.  
  
- Starten Sie beide Computer neu.  
  
- Wenn für das Remotedebugging die Eingabe von Anmeldeinformationen erforderlich ist, aktivieren Sie die Option zum Speichern der Anmeldeinformationen.  
  
## <a name="see-also"></a>Siehe auch  
 [Remote Debugging Errors and Troubleshooting (Remotedebuggen – Fehler und Problembehandlung)](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Remote Debugging](../debugger/remote-debugging.md)

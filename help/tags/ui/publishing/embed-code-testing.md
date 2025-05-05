---
title: Testen von Einbettungs-Codes mit Adobe Experience Platform Debugger
description: Erfahren Sie, wie Sie mit Experience Platform Debugger verschiedene Einbettungs-Codes für Adobe Experience Platform lokal auf Ihrer Website testen können.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 58%

---

# Testen von Einbettungs-Codes mit Adobe Experience Platform Debugger

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Wenn Sie Änderungen an Ihren Tag-Bibliotheks-Builds in Adobe Experience Platform vornehmen, sollten Sie diese Änderungen testen, bevor Sie den Build in Ihrer Betreibungsumgebung bereitstellen. Wenn Sie keine dedizierte Staging- oder Entwicklungs-Umgebung für Ihre Website haben, können Sie mit Adobe Experience Platform Debugger verschiedene Einbettungscodes lokal auf Ihrer Site testen.

## Voraussetzungen

Dieses Tutorial setzt Grundkenntnisse der Verwendung von Umgebungen und Einbettungs-Codes für Tags voraus. Weitere Informationen dazu finden Sie in der [Übersicht zu Umgebungen](./environments.md).

Für dieses Tutorial müssen Sie außerdem die Browser-Erweiterung Experience Platform Debugger installiert haben. Experience Platform Debugger ist für den Chrome-Browser verfügbar. Verwenden Sie den folgenden Link, um die Erweiterung zu installieren, bevor Sie mit dem Tutorial beginnen:

* [Experience Platform Debugger für Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Öffnen Sie Experience Platform Debugger auf Ihrer Website

Navigieren Sie mit einem beliebigen Browser zu Ihrer Website und öffnen Sie die Experience Platform Debugger-Erweiterung. Die Site, mit der Experience Platform Debugger derzeit verbunden ist, wird unten im Fenster angezeigt. Wenn auf Ihrer Website derzeit Tags ausgeführt werden, werden sie auf der Registerkarte [!UICONTROL Zusammenfassung] aufgeführt.

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Wenn Experience Platform Debugger zunächst keine Verbindung herstellt, müssen Sie möglicherweise die Browser-Registerkarte neu laden, auf der Ihre Website angezeigt wird, bevor Sie es erneut versuchen.

## Einbettungs-Codes ersetzen

Sobald Experience Platform Debugger mit Ihrer Site verbunden ist, wählen Sie **[!UICONTROL Launch]** im linken Navigationsbereich aus. Hier finden Sie Informationen zum derzeit auf Ihrer Site ausgeführten Bibliotheks-Build einschließlich der Umgebung und der zugehörigen Erweiterungen. Wählen Sie hier **[!UICONTROL Konfiguration]** aus, um die Steuerelemente zum Verwalten von Einbettungs-Codes anzuzeigen.

![](./images/embed-code-testing/launch-tab.png)

Unter [!UICONTROL Seiteneinbettungs-Code] wird der Einbettungs-Code angezeigt, den Ihre Site derzeit verwendet. Wählen Sie **[!UICONTROL Aktionen]** auf der rechten Seite des Einbettungs-Codes aus und wählen Sie dann **[!UICONTROL Ersetzen]**.

![](./images/embed-code-testing/replace.png)

Dann wird ein Popup angezeigt, in dem Sie aufgefordert werden, einen Einbettungs-Code anzugeben, der den aktuellen Code ersetzen soll. Beachten Sie, dass durch Ersetzen des Einbettungs-Codes mit Experience Platform Debugger der auf Ihrer Site bereitgestellte Einbettungs-Code nicht geändert wird. Stattdessen wird nur der lokal ausgeführte Einbettungscode ersetzt, um Ihnen das Testen und Debugging der Implementierung zu ermöglichen.

Fügen Sie den Einbettungs-Code, den Sie testen möchten, in das bereitgestellte Textfeld ein und wählen Sie dann **[!UICONTROL Übernehmen]**.

![](./images/embed-code-testing/paste-code.png)

Der Tab **[!UICONTROL Konfiguration]** wird wieder angezeigt und zeigt an, dass der Live-Einbettungs-Code durch den von Ihnen angegebenen ersetzt wurde. Sie können jetzt den Webbrowser verwenden, um zu sehen, ob der von Ihnen getestete Einbettungs-Code erwartungsgemäß funktioniert.

![](./images/embed-code-testing/code-replaced.png)

## Nächste Schritte

In diesem Tutorial wurde beschrieben, wie Sie mit Experience Platform Debugger zu Testzwecken lokal zwischen Einbettungs-Codes wechseln können. Weitere Informationen zu den verschiedenen Funktionen von finden [&#128279;](../../../debugger/home.md) in der Dokumentation zum Experience Platform-Debugger .

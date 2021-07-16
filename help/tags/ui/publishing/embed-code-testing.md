---
title: Testen von Einbettungs-Codes mit Adobe Experience Platform Debugger
description: Hier erfahren Sie, wie Sie mit Platform Debugger verschiedene Einbettungs-Codes für Adobe Experience Platform lokal auf Ihrer Website testen können.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 85%

---

# Testen von Einbettungs-Codes mit Adobe Experience Platform Debugger

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Wenn Sie Änderungen an Ihren Tag-Bibliotheks-Builds in Adobe Experience Platform vornehmen, sollten Sie diese Änderungen testen, bevor Sie den Build in Ihrer Produktionsumgebung bereitstellen. Wenn Sie keine dedizierte Staging- oder Entwicklungs-Umgebung für Ihre Website haben, können Sie mit Adobe Experience Platform Debugger verschiedene Einbettungscodes lokal auf Ihrer Site testen.

## Voraussetzungen

Dieses Tutorial setzt ein grundlegendes Verständnis der Verwendung von Umgebungen und Einbettungscodes in der Datenerfassungs-Benutzeroberfläche voraus. Weitere Informationen dazu finden Sie in der [Übersicht zu Umgebungen](./environments.md).

Für dieses Tutorial muss außerdem die Browser-Erweiterung „Platform Debugger“ installiert sein. Platform Debugger ist nur für Chrome- und Firefoxbrowser verfügbar. Verwenden Sie einen der folgenden Links, um die Erweiterung zu installieren, bevor Sie mit dem Tutorial beginnen:

* [Platform Debugger für Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [Platform Debugger für Firefox](https://addons.mozilla.org/de/firefox/addon/adobe-experience-platform-dbg/)

## Öffnen von Platform Debugger auf Ihrer Website

Navigieren Sie mit dem Browser Ihrer Wahl zu Ihrer Website und öffnen Sie die Platform Debugger-Erweiterung. Die Site, mit der Platform Debugger derzeit verbunden ist, wird unten im Fenster angezeigt. Wenn Tags derzeit auf Ihrer Site ausgeführt werden, wird sie auf der Registerkarte [!UICONTROL Zusammenfassung] aufgeführt.

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Falls Platform Debugger zunächst keine Verbindung herstellt, müssen Sie möglicherweise den Browsertab, der Ihre Website anzeigt, neu laden, bevor Sie es erneut versuchen.

## Einbettungs-Codes ersetzen

Sobald Platform Debugger mit Ihrer Site verbunden ist, wählen Sie **[!UICONTROL Launch]** im linken Navigationsbereich aus. Hier finden Sie Informationen zum derzeit auf Ihrer Site ausgeführten Bibliotheks-Build einschließlich der Umgebung und der zugehörigen Erweiterungen. Wählen Sie hier **[!UICONTROL Konfiguration]** aus, um die Steuerelemente zum Verwalten von Einbettungs-Codes anzuzeigen.

![](./images/embed-code-testing/launch-tab.png)

Unter [!UICONTROL Seiteneinbettungs-Code] wird der Einbettungs-Code angezeigt, den Ihre Site derzeit verwendet. Wählen Sie **[!UICONTROL Aktionen]** auf der rechten Seite des Einbettungs-Codes aus und wählen Sie dann **[!UICONTROL Ersetzen]**.

![](./images/embed-code-testing/replace.png)

Dann wird ein Popup angezeigt, in dem Sie aufgefordert werden, einen Einbettungs-Code anzugeben, der den aktuellen Code ersetzen soll. Beachten Sie, dass das Ersetzen des Einbettungs-Codes mit Platform Debugger den bereitgestellten Einbettungs-Code auf Ihrer Site nicht ändert. Stattdessen wird nur der lokal ausgeführte Einbettungscode ersetzt, um Ihnen das Testen und Debugging der Implementierung zu ermöglichen.

Fügen Sie den Einbettungs-Code, den Sie testen möchten, in das bereitgestellte Textfeld ein und wählen Sie dann **[!UICONTROL Übernehmen]**.

![](./images/embed-code-testing/paste-code.png)

Der Tab **[!UICONTROL Konfiguration]** wird wieder angezeigt und zeigt an, dass der Live-Einbettungs-Code durch den von Ihnen angegebenen ersetzt wurde. Sie können jetzt den Webbrowser verwenden, um zu sehen, ob der von Ihnen getestete Einbettungs-Code erwartungsgemäß funktioniert.

![](./images/embed-code-testing/code-replaced.png)

## Nächste Schritte

In diesem Tutorial wurde beschrieben, wie Sie mit Platform Debugger zu Testzwecken zwischen Einbettungs-Codes wechseln können. Weitere Informationen zu den verschiedenen Funktionen finden Sie in der [Dokumentation zum Platform Debugger](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html?lang=de).

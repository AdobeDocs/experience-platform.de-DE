---
title: Premium CDN-Unterstützung für Tags
description: Erfahren Sie mehr über die Premium-CDN-Funktion für Tags und wie Sie damit Ihre Inhalte in mehreren geografischen Regionen bereitstellen können.
source-git-commit: 530fc1ad3f389ffb5d77ddf6aa0b0b3208f1d532
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Premium-CDN-Unterstützung für Tags (Beta)

>[!IMPORTANT]
>
>Die Premium-CDN-Funktion für Tags befindet sich derzeit in der Betaphase und Ihr Unternehmen hat möglicherweise noch keinen Zugriff darauf. Diese Dokumentation kann sich ändern.

Wenn Sie eine [Von Adobe verwalteter Host](./hosts/managed-by-adobe-host.md) Um Ihre Adobe Experience Platform-Tags auf Ihrer Website bereitzustellen, werden diese Assets in verschiedenen Inhaltsbereitstellungsnetzwerken (Content Delivery Network, CDNs) auf der ganzen Welt verteilt, um die schnellste Download-Geschwindigkeit zu erzielen. Es gibt jedoch bestimmte Regionen, in denen alle Website-Assets repliziert und auf einem Server in dieser Region gehostet werden müssen.

Um dies zu berücksichtigen, bieten Tags in Experience Platform eine Premium-CDN-Funktion, mit der Sie Inhalte für diese Sonderregionen bereitstellen können.

Die Premium-CDN-Unterstützung ist eine gebührenpflichtige Funktion und muss von Ihrer Organisation erworben werden, um sie zu aktivieren und zu verwenden. In diesem Handbuch wird beschrieben, wie Sie diese Funktion nach dem Kauf in der Datenerfassungs-Benutzeroberfläche konfigurieren und verwenden.

## Premium-CDN für ein Unternehmen aktivieren

Premium-CDN ist auf Unternehmensebene aktiviert, d. h. Sie müssen über Berechtigungen zur Unternehmensbearbeitung verfügen, um die Funktion zu aktivieren.

Navigieren Sie in der Datenerfassungs-Benutzeroberfläche zu **[!UICONTROL Tags]** > **[!UICONTROL Unternehmen]**. Wählen Sie hier das Unternehmen aus, für das Sie die Funktion aktivieren möchten, und wählen Sie dann **[!UICONTROL Konfigurieren]** .

![Wählen Sie ein Unternehmen aus, das konfiguriert werden soll](../../images/ui/publishing/premium-cdn/configure-property.png)

Wählen Sie im angezeigten Konfigurationsdialogfeld die Option für **[!UICONTROL Premium CDN aktiviert]** vor der Auswahl **[!UICONTROL Speichern]** um Ihre Änderungen zu bestätigen.

![Premium-CDN-Option aktivieren](../../images/ui/publishing/premium-cdn/enable-premium-cdn.png)

## Tag-Bibliotheken mit aktualisierten Einbettungscodes neu erstellen und installieren

Die Aktivierung der Premium-CDN-Funktion bedeutet nicht, dass Ihre Tag-Assets sofort repliziert werden und in den neuen Regionen verwendet werden können. Dies bedeutet nur, dass Sie jetzt entscheiden können, wann Sie sich für diese Funktion anmelden möchten.

>[!IMPORTANT]
>
>Bibliotheken, die vor der Aktivierung des Premium-CDN erstellt wurden, funktionieren weiterhin genau so wie heute. Dies gilt auch für Bibliotheken, die nicht von Adobe verwaltet werden, da [archivierte Umgebungen](./environments.md#archive) nur relative URLs für ihre Asset-Pfade verwenden. Beachten Sie, dass sich nach der Aktivierung des Premium-CDN alle Bibliotheken, die Sie erstellen und die nicht von Adobe verwaltet werden, so verhalten, als ob die Premium-CDN-Funktion nicht aktiviert ist.

Nachdem Sie das Premium-CDN aktiviert und alle Bibliotheken neu erstellt haben, die Sie in den neuen Hosting-Regionen verwenden möchten, können Sie die neuen Einbettungscodes für die Hosting-Region abrufen, um sie zu Ihren Websites hinzuzufügen.

>[!NOTE]
>
>Der Bibliotheks-Einbettungscode, der unter der [!UICONTROL Standard] Hosting-Region funktioniert weiterhin wie bisher, ebenso wie alle Einbettungscodes &quot;Seitenanfang&quot;oder &quot;Seitenende&quot;, die bereits auf Ihren Websites vorhanden sind.

Besuchen Sie die **[!UICONTROL Umgebungen]** -Seite oder zeigen Sie im Bildschirm zur Bibliotheksbearbeitung die Installationsanweisungen für die Umgebung an, um die neuen Einbettungscodes zu finden. Jede neue unterstützte Hostingregion wird nach dem [!UICONTROL Standard] Hostingregion (wird für Gebiete auf der Welt verwendet, die ohne Premium-CDN unterstützt werden). Der folgende Screenshot zeigt einen Einbettungscode für die Region China, die `.cn` als Domäne der obersten Ebene (TLD).

![Einbettungscode für die chinesische Region](../../images/ui/publishing/premium-cdn/embed-codes.png)

Wählen Sie den entsprechenden Einbettungscode für die Webseite aus und fügen Sie ihn in die `<head>` -Tag Ihres Dokuments. Weitere Informationen zur Installation von Tag-Bibliotheken mithilfe von Einbettungscodes finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche von Umgebungen](./environments.md#installation).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie die Premium-CDN-Funktion für Ihre Tag-Implementierung aktivieren und installieren. Weitere Informationen zum Installieren und Testen von Tag-Bibliotheken in Ihren Web- und mobilen Eigenschaften finden Sie im Abschnitt [Publishing-Übersicht](./overview.md).

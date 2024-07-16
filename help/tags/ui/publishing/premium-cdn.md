---
title: Experience Platform-Tags (China)
description: Erfahren Sie mehr über die Funktion für Experience Platform-Tags (China) für Tags und wie Sie damit Ihre-Tags in mehreren geografischen Regionen bereitstellen können.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Experience Platform-Tags (China)

Wenn Sie einen [Adobe-verwalteten Host](./hosts/managed-by-adobe-host.md) verwenden, um Ihre Adobe Experience Platform-Tags-Assets auf Ihrer Website bereitzustellen, werden diese Assets auf verschiedene Inhaltsbereitstellungsnetzwerke (Content Delivery Network, CDNs) auf der ganzen Welt verteilt, um die schnellste Download-Geschwindigkeit zu erzielen. Es gibt jedoch bestimmte Regionen, in denen alle Website-Assets repliziert und auf einem Server in dieser Region gehostet werden müssen.

Um dies zu berücksichtigen, bieten Tags in Experience Platform eine Experience Platform-Tags-Funktion (China), mit der Sie Inhalte für diese speziellen Regionen bereitstellen können.

Experience Platform-Tags (China)-Unterstützung ist eine gebührenpflichtige Funktion und muss von Ihrem Unternehmen erworben werden, um sie zu aktivieren und zu verwenden. In diesem Handbuch wird beschrieben, wie Sie diese Funktion nach dem Kauf in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche konfigurieren und verwenden.

## Aktivieren von Experience Platform-Tags (China) für Ihre Organisation

Experience Platform Tags (China) ist auf Unternehmensebene aktiviert. Sobald Ihr Unternehmen die Funktion Experience Platform-Tags (China) erworben hat, aktiviert ein Adobe-Administrator die Funktion in der Benutzeroberfläche für Ihr Unternehmen.

## Tag-Bibliotheken mit aktualisierten Einbettungscodes neu erstellen und installieren

Sobald Experience Platform-Tags (China) aktiviert ist, bedeutet dies nicht, dass Ihre Tag-Assets sofort repliziert werden und in den neuen Regionen verwendet werden können. Dies bedeutet nur, dass Sie jetzt entscheiden können, wann Sie sich für diese Funktion entscheiden.

>[!IMPORTANT]
>
>Bibliotheken, die vor der Aktivierung von Tags in China erstellt wurden, werden weiterhin genau so funktionieren wie heute. Dies gilt auch für Bibliotheken, die nicht von Adobe verwaltet werden, da [archivierte Umgebungen](./environments.md#archive) nur relative URLs für ihre Asset-Pfade verwenden. Beachten Sie, dass sich nach der Aktivierung von Experience Platform-Tags (China) jede Bibliothek, die Sie erstellen und die nicht von Adobe verwaltet wird, so verhält, als ob die Tags in der China-Funktion nicht aktiviert wären.

Nachdem Sie Tags in China aktiviert und alle Bibliotheken neu erstellt haben, die Sie in den neuen Hosting-Regionen verwenden möchten, können Sie die neuen Einbettungscodes für die Hosting-Region abrufen, um sie zu Ihren Websites hinzuzufügen.

>[!NOTE]
>
>Der Bibliotheks-Einbettungscode, der unter dem Hosting-Bereich [!UICONTROL Standard] aufgeführt ist, funktioniert weiterhin wie gewohnt und alle Einbettungscodes für &quot;Seitenanfang&quot;oder &quot;Seitenende&quot;befinden sich bereits auf Ihren Websites.

Rufen Sie die Seite **[!UICONTROL Umgebungen]** auf oder zeigen Sie die Installationsanweisungen für die Umgebung im Bildschirm zum Bearbeiten der Bibliothek an, um die neuen Einbettungscodes zu finden. Jede neue unterstützte Hostingregion wird nach der Hostingregion [!UICONTROL Standard] angezeigt (wird für Gebiete weltweit verwendet, die ohne Experience Platform-Tags (China) unterstützt werden). Der folgende Screenshot zeigt einen Einbettungscode für die chinesische Region, die `.cn` als Domäne der obersten Ebene (TLD) verwendet.

![Einbettungscode für die chinesische Region](../../images/ui/publishing/premium-cdn/embed-codes.png)

Wählen Sie den entsprechenden Einbettungscode für die Webseite aus und fügen Sie ihn im Tag `<head>` Ihres Dokuments ein. Weitere Informationen zur Installation von Tag-Bibliotheken mithilfe von Einbettungscodes finden Sie im Handbuch [Umgebungen UI guide](./environments.md#installation) .

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie die Experience Platform-Tags-Funktion (China) für Ihre Tag-Implementierung aktivieren und installieren. Weitere Informationen zum Installieren und Testen von Tag-Bibliotheken in Ihren Web- und mobilen Eigenschaften finden Sie in der [Veröffentlichungsübersicht](./overview.md).

---
title: Experience Platform-Tags (China)
description: Erfahren Sie mehr über die Funktion "Experience Platform-Tags (China)“ für Tags und wie damit Ihre Inhalte in mehreren geografischen Regionen bereitgestellt werden können.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Experience Platform-Tags (China)

Wenn Sie einen [Adobe-verwalteten Host](./hosts/managed-by-adobe-host.md) verwenden, um Ihre Adobe Experience Platform-Tags-Assets auf Ihrer Website bereitzustellen, werden diese Assets auf verschiedene Content Delivery Network (CDNs) auf der ganzen Welt verteilt, um die schnellste Download-Geschwindigkeit zu erzielen. Es gibt jedoch bestimmte Regionen, in denen alle Website-Assets repliziert und auf einem Server innerhalb dieser Region gehostet werden müssen.

Um dies zu berücksichtigen, bietet Tags in Experience Platform eine Funktion für Experience Platform-Tags (China), mit der Sie Inhalte für diese speziellen Regionen bereitstellen können.

Der Support für Experience Platform-Tags (China) ist eine gebührenpflichtige Funktion und muss von Ihrem Unternehmen erworben werden, um sie zu aktivieren und zu verwenden. In diesem Handbuch wird beschrieben, wie Sie diese Funktion nach dem Kauf in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche konfigurieren und verwenden.

## Aktivieren von Experience Platform-Tags (China) für Ihr Unternehmen

Experience Platform-Tags (China) sind auf Unternehmensebene aktiviert. Nachdem Ihr Unternehmen die Funktion Experience Platform-Tags (China) erworben hat, aktiviert ein Adobe-Administrator diese Funktion in der Benutzeroberfläche für Ihr Unternehmen.

## Erstellen und installieren Sie Tag-Bibliotheken mit aktualisierten Einbettungs-Codes.

Sobald Experience Platform Tags (China) aktiviert ist, bedeutet dies nicht, dass Ihre Tag-Assets sofort repliziert und in den neuen Regionen verwendet werden können. Das bedeutet nur, dass Sie jetzt auswählen können, wann Sie diese Funktion aktivieren möchten.

>[!IMPORTANT]
>
>Bibliotheken, die vor der Aktivierung von Tags in China erstellt wurden, werden weiterhin wie bisher funktionieren. Dies gilt auch für Bibliotheken, die nicht von Adobe verwaltet werden, da [archivierte Umgebungen](./environments.md#archive) für ihre Asset-Pfade nur relative URLs verwenden. Beachten Sie, dass sich nach der Aktivierung von Experience Platform-Tags (China) alle Bibliotheken, die Sie erstellen und nicht von Adobe verwaltet werden, so verhalten, als ob die Funktion „Tags in China“ nicht aktiviert wäre.

Nachdem Sie Tags in China aktiviert und alle Bibliotheken neu erstellt haben, die Sie in den neuen Hosting-Regionen verwenden möchten, können Sie die neuen Einbettungs-Codes für die Hosting-Region abrufen, um sie zu Ihren Websites hinzuzufügen.

>[!NOTE]
>
>Der Bibliotheks-Einbettungs-Code, der unter der Hosting-Region [!UICONTROL Standard] aufgeführt ist, funktioniert weiterhin wie gehabt, sowie alle Seitenoberseiten- oder Seitenunterseiten-Einbettungs-Codes, die bereits auf Ihren Websites vorhanden sind.

Besuchen Sie die **[!UICONTROL Umgebungen]** Seite oder sehen Sie sich die Anweisungen zur Installation der Umgebung auf dem Bildschirm zum Bearbeiten der Bibliothek an, um die neuen Einbettungs-Codes zu finden. Jede neue unterstützte Hosting-Region wird nach der Hosting-Region [!UICONTROL Standard] angezeigt (für Bereiche in der Welt verwendet, die ohne Experience Platform-Tags unterstützt werden (China)). Der folgende Screenshot zeigt einen Einbettungs-Code für die Region China, die `.cn` als Top-Level-Domain (TLD) verwendet.

![Einbettungs-Code für die Region China](../../images/ui/publishing/premium-cdn/embed-codes.png)

Wählen Sie den entsprechenden Einbettungs-Code für die Web-Seite aus und fügen Sie ihn in das `<head>`-Tag Ihres Dokuments ein. Weitere Informationen zur Verwendung von Einbettungs-Codes zur Installation von Tag-Bibliotheken finden Sie im [Handbuch zur Benutzeroberfläche von Umgebungen](./environments.md#installation).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie die Funktion Experience Platform-Tags (China) für Ihre Tag-Implementierung aktivieren und installieren. Weitere Informationen zum Installieren und Testen von Tag-Bibliotheken in Ihren Web- und mobilen Eigenschaften finden Sie unter [Publishing-Übersicht](./overview.md).

---
keywords: Nielsen BSDK;nielsen bsdk;nielsen BSDK
title: Nielsen BSDK-Erweiterung
description: Die Nielsen BSDK-Erweiterung ist ein Analyseziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf Adobe Exchange.
exl-id: e1c10673-e3f4-474d-98d7-960124b2bfc7
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 88%

---

# [!DNL Nielsen BSDK]-Erweiterung  {#nielsen-bsdk-extension}

## Übersicht {#overview}

[!DNL Nielsen Digital SDK] Tag-Erweiterung bietet Zielgruppenmessungen über die folgenden digitalen Messprodukte:

DCR: Eine Messlösung, die eine tägliche Messung von nicht-linearen digitalen Inhalten einschließlich Inhalten mit Anzeigen ermöglicht; erlaubt eine umfassende Ansicht des Verbrauchs an digitalen Inhalten von Desktop-, Mobil-, Tablet- und vernetzten Geräten in Zielgruppen.

DTVR: Dies ermöglicht teilnehmenden Programmierquellen eine lineare Fernsehwiedergabe auf Desktop- und Mobilgeräten. Das ist die erste Lösung, die eine Akkreditierung des MRC für ihren Beitrag zur Messung der Zuschauerzahlen von auf Computern und Mobilgeräten angesehenen Programmen erhalten hat.

[!DNL Nielsen BSDK] ist eine Analyseerweiterung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Tag-Erweiterungen in Platform finden Sie in der [Übersicht zu Tag-Erweiterungen](../launch-extensions/overview.md).

![Nielsen BSDK-Erweiterung](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im [!DNL Destinations]-Katalog für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, müssen Sie Zugriff auf Tags in Adobe Experience Platform haben. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an den Admin Ihrer Organisation, um Zugriff auf Tags zu erhalten, und bitten Sie darum, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Nielsen BSDK] Erweiterung:

Gehen Sie in der [Platform-Oberfläche](https://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste die Option **[!UICONTROL Konfigurieren]** aus. Wenn das Feld **[!UICONTROL Konfigurieren]** ausgegraut ist, verfügen Sie nicht über die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie im [Eigenschaften-Seitenabschnitt](../../../tags/ui/administration/companies-and-properties.md#properties-page) der Tags-Dokumentation.

Der Workflow führt Sie durch die Schritte zum Abschließen der Installation.

Informationen zu den Konfigurationsoptionen für Erweiterungen und zur Installationsunterstützung finden Sie in der [Nielsen-BSDK-Seite auf Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Weitere Informationen finden Sie im Abschnitt zum Thema [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in der Tag-Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit dem Einrichten von Regeln beginnen.

Sie können Regeln für Ihre installierten Erweiterungen einrichten, damit nur in bestimmten Situationen Ereignisdaten an das Erweiterungsziel gesendet werden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Tags-Dokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Auch wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Platform-Benutzeroberfläche weiterhin **[!UICONTROL Installieren]** für die Erweiterung angezeigt. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie in der Anleitung zum [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tags-Dokumentation.

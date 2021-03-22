---
keywords: Google-Anzeigenmanager;Google-Anzeige;DoubleClick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google-Anzeigenmanager
title: Google Ad Manager-Verbindung
description: 'Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.  '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 30%

---


# [!DNL Google Ad Manager] connection

## Übersicht {#overview}

[!DNL Google Ad Manager], früher als für Herausgeber oder bekannt, ist eine AdX-Plattform von , die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.[!DNL DoubleClick][!DNL DoubleClick AdX][!DNL Google]

## Zielspezifikationen

Beachten Sie die folgenden Details, die für [!DNL Google Ad Manager]-Ziele spezifisch sind:

* Aktivierte Audiencen werden programmgesteuert auf der [!DNL Google]-Plattform erstellt.
* Die Plattform enthält derzeit keine Messungsmetrik zur Validierung einer erfolgreichen Aktivierung. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL Google Ad Manager] erstellen und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst in der Vergangenheit (mit Audience Manager oder anderen Anwendungen) nicht aktiviert haben, wenden Sie sich bitte an Adobe Consulting oder den Kundendienst, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL Google]-Integrationen in Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf Plattform übertragen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben sind.

| Zielgruppe | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein GAID-Namensraum ist. |
| IDFA | [!DNL Apple ID for Advertisers] | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein IDFA-Namensraum ist. |
| AAM UUUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), auch bekannt als  [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die der Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) für Zielgruppen in Kalifornien und die Google Cookie-ID für alle anderen Benutzer. |
| [!DNL Google] Cookie-ID | [!DNL Google] Cookie-ID | [!DNL Google] verwendet diese ID zur Zielgruppe von Benutzern außerhalb von Kalifornien. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising ID. Diese ID identifiziert Geräte mit Windows 10 eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) in das Google-Ziel.

## Voraussetzungen

### Zulassungsliste

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager]-Ziel in Platform einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene Vorgang der Zulassungsliste von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Ad Manager]-Ziel in Platform erstellen, müssen Sie sich an [!DNL Google] wenden, damit die Adobe auf die Liste der zulässigen Datenanbieter gesetzt wird und Ihr Konto der Zulassungsliste hinzugefügt werden kann. Wenden Sie sich an [!DNL Google] und geben Sie die folgenden Informationen ein:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Netzwerkkennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* **Zielgruppenverknüpfungskennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* Ihr Kontotyp. DFP von Google oder AdX Buyer.

## Ziel konfigurieren

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** **[!DNL Google Ad Manager]** aus und wählen Sie **[!UICONTROL Konfigurieren]**.

![Mit Google Ad Manager-Ziel verbinden](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

Geben Sie im Schritt **Setup** des Arbeitsablaufs zum Erstellen des Ziels [!UICONTROL Grundlegende Informationen] für das Ziel ein.

![Grundlegende Informationen – Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `DFP by Google` für for Publishers.[!DNL DoubleClick]
   * `AdX buyer` für [!DNL Google AdX] verwenden
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID ein  [!DNL Google]. Dies kann Ihre Netzwerkkennung oder Ihre Zielgruppenverknüpfungskennung sein. Normalerweise ist dies eine achtstellige Kennung.
* **[!UICONTROL Marketingaktion]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Wenn Sie ein [!DNL Google Ad Manager]-Ziel einrichten, wenden Sie sich an Ihren [!DNL Google Account Manager]- oder Kundenbetreuer, um zu verstehen, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten nach [!DNL Google Ad Manager]

Anweisungen zum Aktivieren von Segmenten in [!DNL Google Ad Manager] finden Sie unter [Daten in Ziele aktivieren](../../ui/activate-destinations.md).

## Exportierte Daten

Um zu überprüfen, ob Daten erfolgreich in das [!DNL Google Ad Manager]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ad Manager]-Konto. Wenn die Aktivierung erfolgreich war, werden Audiencen in Ihrem Konto ausgefüllt.
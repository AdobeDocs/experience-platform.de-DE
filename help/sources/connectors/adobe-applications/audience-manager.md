---
keywords: Experience Platform; Startseite; beliebte Themen; Audience Manager-Connector; Audience Manager; Audience Manager
solution: Experience Platform
title: Übersicht über Audience Manager Source
description: Die Adobe Audience Manager-Quelle streamt Erstanbieterdaten, die im Audience Manager erfasst wurden, an Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 8ef9fedcc77f39707ef5191988a5b7360e1118cc
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 1%

---

# Audience Manager-Quelle

>[!IMPORTANT]
>
>Bei der Ersteinrichtung gibt die Adobe Audience Manager-Quelle Fehlermeldungen zurück, die erklären, dass kein Identitäts-Namespace mit dem angegebenen `namespaceCode={VALUE}` vorhanden ist. **Hinweis**: Im Backend wird `namespaceCode` verwendet, um auf das Identitätssymbol zu verweisen. Um Ihre Integration abzuschließen, müssen Sie:
>
>- [Erstellen Sie einen benutzerdefinierten Namespace im Identity Service](../../../identity-service/features/namespaces.md#create-custom-namespaces) mit dem angegebenen Identitätssymbol (`VALUE`).
>- Erfassen Sie Ihre Daten erneut.

Die Adobe Audience Manager-Quelle streamt Erstanbieterdaten, die in Adobe Audience Manager zur Aktivierung in Adobe Experience Platform erfasst wurden. Die Audience Manager-Quelle erfasst zwei Datentypen in Platform:

- **Echtzeitdaten:** Daten, die in Echtzeit auf dem Datenerfassungsserver des Audience Managers erfasst werden. Diese Daten werden in Audience Manager zum Ausfüllen regelbasierter Eigenschaften verwendet und werden in Platform in der kürzesten Latenzzeit angezeigt.
- **Profildaten:** Audience Manager verwendet Echtzeitdaten und integrierte Daten, um Kundenprofile abzuleiten. Diese Profile werden zum Ausfüllen von Identitätsdiagrammen und Eigenschaften in Segmentrealisierungen verwendet.

Die Audience Manager-Quelle ordnet diese Datentypen einem Experience-Datenmodell (XDM)-Schema zu und sendet sie dann an Platform. Echtzeitdaten werden als XDM ExperienceEvent-Daten gesendet, während Profildaten als XDM Individual Profile-Daten gesendet werden.

Weitere Informationen finden Sie in der Anleitung zum [Erstellen einer Audience Manager-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Was ist Experience-Datenmodell (XDM)?

XDM ist eine öffentlich dokumentierte Spezifikation, die ein standardisiertes Framework bereitstellt, mit dem Platform Kundenerlebnisdaten organisiert.

Durch die Einhaltung von XDM-Standards können Kundenerlebnisdaten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weitere Informationen zur Verwendung von XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md). Weitere Informationen zur Struktur von XDM-Schemas zwischen Profilen und Ereignissen finden Sie in den [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md) .

## Beispiele für XDM-Schemas

Im Folgenden finden Sie Beispiele für die Audience Manager-Struktur, die XDM ExperienceEvent und XDM Individual Profile in Platform zugeordnet ist.

### ExperienceEvent - für Echtzeitdaten und integrierte Daten

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile - für Profildaten

![](images/aam-profile-xdm-for-profile-data.png)

Informationen dazu, wie Felder vom Audience Manager zu XDM zugeordnet werden, finden Sie in der Dokumentation zu den Feldern für die Zuordnung von Audience Managern [1}.](./mapping/audience-manager.md)

## Daten-Management in Platform

### Datensätze

Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält und über eine Datenverbindung zur Verfügung gestellt wird. Audience Manager-Daten bestehen aus Echtzeitdaten, eingehenden Daten und Profildaten. Um Ihre Audience Manager-Datensätze zu finden, verwenden Sie die Suchfunktion in der Benutzeroberfläche mit den angegebenen Benennungskonventionen für jeden Datentyp.

Audience Manager-Datensätze sind standardmäßig für Profil deaktiviert und Benutzer können Datensätze anhand ihrer Anwendungsfälle aktivieren oder deaktivieren. Es wird nicht empfohlen, Datensätze zu deaktivieren, die für die Segmentzugehörigkeit in Profil verwendet werden.

>[!NOTE]
>
>AAM Echtzeit ist der einzige Datensatz, der zum Data Lake gelangt. Alle anderen Audience Manager-Datensätze gehen an [!DNL Profile], wenn sie für [!DNL Profile] aktiviert sind. Wenn sie nicht für [!DNL Profile] aktiviert sind, erhalten sie keine Daten und werden als leer angezeigt.

| Name des Datensatzes | Beschreibung | Klasse |
| --- | --- | --- |
| AAM Echtzeit | Dieser Datensatz enthält Daten, die von direkten Treffern auf Audience Manager-DCS-Endpunkten erfasst werden, und Identitätszuordnungen für Audience Manager-Profile. Lassen Sie diesen Datensatz für die Profilaufnahme aktiviert. | Erlebnisereignis |
| AAM Echtzeit-Profilaktualisierungen | Dieser Datensatz ermöglicht das Echtzeit-Targeting von Audience Manager-Eigenschaften und -Segmenten. Es enthält Informationen zum regionalen Routing, zu Eigenschaften und zur Segmentzugehörigkeit von Edge. Lassen Sie diesen Datensatz für die Profilaufnahme aktiviert. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM Gerätedaten | Gerätedaten mit ECIDs und entsprechenden Segmentrealisierungen, die in Audience Manager aggregiert werden. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM Geräteprofildaten | Wird für die Audience Manager-Connector-Diagnose verwendet. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM authentifizierte Profile | Dieser Datensatz enthält vom Audience Manager authentifizierte Profile. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM Authentifizierte Profilmeta-Daten | Wird für die Audience Manager Connector-Diagnose verwendet. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| Datenaufstockung für AAM Geräte | Datensatz aus dem Einbringen von Daten früherer Geräte. Dies umfasst ECIDs und die entsprechenden in Audience Manager aggregierten Segmentrealisierungen. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| Aufstockung authentifizierter Profile AAM | Datensatz aus dem Einbringen authentifizierter Daten in die Vergangenheit. Hier sind vom Audience Manager authentifizierte Profile enthalten. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |

### Verbindungen

Adobe Audience Manager erstellt eine Verbindung im Katalog: Audience Manager-Verbindung. Catalog ist das System der Datensätze für Speicherort und Herkunft von Daten in Adobe Experience Platform. Eine Verbindung ist ein Catalog-Objekt, das eine kundenspezifische Instanz von Connectoren ist. Weitere Informationen zu Katalog, Verbindungen und Connectoren finden Sie in der [Übersicht über den Katalogdienst](../../../catalog/home.md) .

### Auswirkungen der Segmentpopulation auf das Profil

Die Segmentpopulationsgrößen wirken sich direkt auf die Profilzahlen aus, wenn Sie ein Audience Manager-Segment zum ersten Mal an Platform senden. Das bedeutet, dass die Auswahl aller Segmente möglicherweise zu Profilüberhöhungen führen kann, die Ihre Lizenznutzungsberechtigung überschreiten. Platform unterscheidet auch neue Daten von historischen Daten für die Profilaufnahme. Ein Segment mit 100 Erstanbieter-basierten Identitäten erstellt 100 Profile. Wenn jedoch die Population desselben Segments auf 150 erhöht und in Platform aufgenommen wurde, erhöht sich die Anzahl der Profile nur um 50, da es nur 50 neue Profile gibt.

Sie können auch die Profilnutzung Ihres Kontos über das Dashboard [Lizenznutzung](../../../dashboards/guides/license-usage.md) überprüfen.

## Wie hoch ist die erwartete Latenz für Audience Manager Data on Platform?

| Audience Manager Data | Typ | Latenz | Anmerkungen |
| --- | --- | --- | --- |
| Echtzeitdaten | Events | &lt;25 Minuten | Zeit, von der Erfassung im Audience Manager-Edge-Knoten bis zur Anzeige im Data Lake. |
| Echtzeitdaten | Profilaktualisierungen | &lt;10 Minuten | Zeit bis zum Start im Echtzeit-Kundenprofil. |
| Echtzeit- und integrierte Daten | Profilaktualisierungen | 24 bis 36 Stunden | Zeit, die von DCS-/PCS-Edge-Daten und integrierten Daten über die Verarbeitung zu einem Benutzerprofil bis zur anschließenden Anzeige im Echtzeit-Kundenprofil reicht. Derzeit landen diese Daten nicht direkt im Data Lake. Die Profilumschaltung kann für Audience Manager-Profil-Datensätze aktiviert werden, um diese Daten direkt in das Echtzeit-Kundenprofil aufzunehmen. |

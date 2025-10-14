---
keywords: Experience Platform;Startseite;beliebte Themen;Audience Manager-Connector;Audience Manager;Audience Manager
solution: Experience Platform
title: Übersicht über Audience Manager Source
description: Die Adobe Audience Manager-Quelle streamt in Audience Manager erfasste First-Party-Daten an Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Audience Manager-Quelle

>[!IMPORTANT]
>
>Bei der Ersteinrichtung gibt die Adobe Audience Manager-Quelle eine Fehlermeldung zurück, die erklärt, dass ein Identity-Namespace mit einer bestimmten `namespaceCode={VALUE}` nicht vorhanden ist. **Hinweis**: Im Back-End wird `namespaceCode` verwendet, um auf das Identitätssymbol zu verweisen. Um Ihre Integration abzuschließen, müssen Sie:
>
>- [Erstellen eines benutzerdefinierten Namespace in Identity Service](../../../identity-service/features/namespaces.md#create-custom-namespaces) mit dem angegebenen Identitätssymbol (`VALUE`) .
>- Nehmen Sie Ihre Daten erneut auf.

Die Adobe Audience Manager-Quelle streamt in Adobe Audience Manager erfasste First-Party-Daten zur Aktivierung in Adobe Experience Platform. Die Audience Manager-Quelle nimmt zwei Datentypen in Experience Platform auf:

- **Echtzeitdaten:** Daten, die in Echtzeit auf dem Datenerfassungsserver von Audience Manager erfasst werden. Diese Daten werden in Audience Manager verwendet, um regelbasierte Eigenschaften auszufüllen, und werden in Experience Platform in der kürzesten Latenzzeit angezeigt.
- **Profildaten:** Audience Manager verwendet Echtzeit- und integrierte Daten zur Ableitung von Kundenprofilen. Diese Profile werden verwendet, um Identitätsdiagramme und Eigenschaften bei der Segmentrealisierung zu füllen.

Die Audience Manager-Quelle ordnet diese Datentypen einem Experience-Datenmodell (XDM)-Schema zu und sendet sie dann an Experience Platform. Echtzeit-Daten werden als XDM ExperienceEvent-Daten gesendet, während Profildaten als XDM Individual Profile-Daten gesendet werden.

Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Audience Manager-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Was ist das Experience-Datenmodell (XDM)?

XDM ist eine öffentlich dokumentierte Spezifikation, die ein standardisiertes Framework bereitstellt, mit dem Experience Platform Kundenerlebnisdaten organisiert.

Durch die Einhaltung von XDM-Standards können Kundenerlebnisdaten einheitlich integriert werden, was die Bereitstellung von Daten und die Erfassung von Informationen erleichtert.

Weitere Informationen zur Verwendung von XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md). Weitere Informationen zur Strukturierung von XDM-Schemata zwischen Profilen und zur Strukturierung von Ereignissen finden Sie in den [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md).

## Beispiele für XDM-Schemata

Im Folgenden finden Sie Beispiele für die Audience Manager-Struktur, die XDM ExperienceEvent und XDM Individual Profile in Experience Platform zugeordnet ist.

### ExperienceEvent - für Echtzeitdaten und integrierte Daten

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Individuelles XDM-Profil - für Profildaten

![](images/aam-profile-xdm-for-profile-data.png)

Informationen zur Zuordnung von Feldern von Audience Manager zu XDM finden Sie in der Dokumentation zu [Audience Manager-Zuordnungsfeldern](./mapping/audience-manager.md).

## Daten-Management in Experience Platform

### Datensätze

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten - in der Regel eine Tabelle - erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) enthält und über eine Datenverbindung zur Verfügung gestellt wird. Audience Manager-Daten bestehen aus Echtzeitdaten, eingehenden Daten und Profildaten. Um Ihre Audience Manager-Datensätze zu finden, verwenden Sie die Suchfunktion in der Benutzeroberfläche mit den bereitgestellten Namenskonventionen für jeden Datentyp.

Audience Manager-Datensätze sind standardmäßig für Profile deaktiviert und Benutzerinnen und Benutzer können Datensätze basierend auf ihren Anwendungsfällen aktivieren oder deaktivieren. Es wird nicht empfohlen, Datensätze zu deaktivieren, die für die Segmentzugehörigkeit im Profil verwendet werden.

>[!NOTE]
>
>AAM Real-time ist der einzige Datensatz, der an den Data Lake gesendet wird. Alle anderen Audience Manager-Datensätze gehen zu [!DNL Profile], wenn sie für [!DNL Profile] aktiviert sind. Wenn sie nicht für die [!DNL Profile] aktiviert sind, erhalten sie keine Daten und werden als leer angezeigt.

| Name des Datensatzes | Beschreibung | Klasse |
| --- | --- | --- |
| AAM Echtzeit | Dieser Datensatz enthält Daten, die durch direkte Treffer auf Audience Manager-DCS-Endpunkten erfasst wurden, sowie Identitätszuordnungen für Audience Manager-Profile. Lassen Sie diesen Datensatz für die Profilaufnahme aktiviert. | Erlebnisereignis |
| Echtzeit-Profilaktualisierungen in AAM | Dieser Datensatz ermöglicht das Targeting von Audience Manager-Eigenschaften und -Segmenten in Echtzeit. Sie enthält Informationen zu regionalem Routing, Eigenschaften und Segmentzugehörigkeit von Edge. Lassen Sie diesen Datensatz für die Profilaufnahme aktiviert. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM-Gerätedaten | Gerätedaten mit ECIDs und entsprechenden Segmentrealisierungen, die in Audience Manager aggregiert werden. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM-Geräteprofildaten | Wird für die Audience Manager-Connector-Diagnose verwendet. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM-authentifizierte Profile | Dieser Datensatz enthält authentifizierte Audience Manager-Profile. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| AAM-Metadaten für authentifizierte Profile | Wird für die Diagnose des Audience Manager-Connectors verwendet. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| Aufstockung der Daten von AAM-Geräten | Datensatz aus dem Einbringen vergangener Gerätedaten. Diese enthält ECIDs und entsprechende Segmentrealisierungen, die in Audience Manager aggregiert wurden. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |
| Aufstockung der authentifizierten AAM-Profile | Datensatz aus dem Einbringen früherer authentifizierter Daten. Dieses enthält authentifizierte Audience Manager-Profile. Daten sind nicht als Batches im Datensatz sichtbar. Sie können den Umschalter **[!UICONTROL Profil]** aktivieren, um die Daten direkt in das Profil aufzunehmen. | Eintrag |

### Verbindungen

Adobe Audience Manager erstellt im Katalog eine Verbindung: Audience Manager-Verbindung. Catalog ist das System der Datensätze für den Speicherort und die Herkunft von Daten in Adobe Experience Platform. Eine Verbindung ist ein Katalogobjekt, das eine kundenspezifische Instanz von Connectoren ist. Weitere Informationen zu [, Verbindungen und Connectoren finden Sie &#x200B;](../../../catalog/home.md) „Übersicht zum Katalog-Service“.

### Auswirkungen der Segmentpopulation auf das Profil

Die Größe der Segmentpopulation wirkt sich direkt auf die Profilzahlen aus, wenn Sie zum ersten Mal ein Audience Manager-Segment an Experience Platform senden. Das bedeutet, dass die Auswahl aller Segmente möglicherweise zu Profilüberhängen führen kann, die Ihre Lizenznutzungsberechtigung überschreiten. Experience Platform unterscheidet bei der Profilaufnahme auch zwischen neuen Daten und historischen Daten. Ein Segment mit 100 First-Party-Identitäten erstellt 100 Profile. Wenn die Population desselben Segments jedoch auf 150 erhöht und in Experience Platform aufgenommen wurde, erhöht sich die Anzahl der Profile nur um 50, da es nur 50 neue Profile gibt.

Sie können auch die Profilnutzung Ihres Kontos im Dashboard [Lizenznutzung“ &#x200B;](../../../dashboards/guides/license-usage.md).

## Wie hoch ist die erwartete Latenz für Audience Manager-Daten in Experience Platform?

| Audience Manager-Daten | Typ | Latenz | Anmerkungen |
| --- | --- | --- | --- |
| Echtzeitdaten | Ereignisse | &lt;25 Minuten | Zeit von der Erfassung im Audience Manager Edge-Knoten bis zur Anzeige im Data Lake. |
| Echtzeitdaten | Profilaktualisierungen | &lt;10 Minuten | Zeit für die Landung im Echtzeit-Kundenprofil. |
| Echtzeit- und Onboarding-Daten | Profilaktualisierungen | 24 bis 36 Stunden | Zeit von der Erfassung über DCS/PCS Edge-Daten und integrierte Daten, die zu einem Benutzerprofil verarbeitet werden, bis hin zur Anzeige im Echtzeit-Kundenprofil. Derzeit landen diese Daten nicht direkt im Data Lake. Der Profilumschalter kann für Audience Manager-Profildatensätze aktiviert werden, um diese Daten direkt in das Echtzeit-Kundenprofil aufzunehmen. |

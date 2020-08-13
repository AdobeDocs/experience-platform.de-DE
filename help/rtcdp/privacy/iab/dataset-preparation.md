---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: IAB TCF 2.0 support in Real-time Customer Data Platform
topic: privacy events
translation-type: tm+mt
source-git-commit: e7cbbd2e376ab109367d1d16cb9e033202866a6f
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 3%

---


# Create datasets for capturing IAB TCF 2.0 consent data

In order for [!DNL Real-time Customer Data Platform] to process customer consent data in accordance with the IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, that data must be sent to datasets whose schemas contain TCF 2.0 consent fields.

Specifically, two datasets are required for capturing TCF 2.0 consent data:

* A dataset based on the [!DNL XDM Individual Profile] class, enabled for use in [!DNL Real-time Customer Profile].
* A dataset based on the [!DNL XDM ExperienceEvent] class.

This document provides steps for setting up these two datasets to collect IAB TCF 2.0 consent data. For an overview of the full workflow to configure [!DNL Real-time CDP] for TCF 2.0, refer to the [IAB TCF 2.0 compliance overview](./overview.md).

## Voraussetzungen 

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)](../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemata.
   * [Create a schema in the UI](../../../xdm/tutorials/create-schema-ui.md): A tutorial covering the basics of working with the Schema Editor.
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Allows you to bridge customer identities from your disparate data sources across devices and systems.
* [Real-time Customer Profile](../../../profile/home.md): Leverages [!DNL Identity Service] to let you create detailed customer profiles from your datasets in real-time. [!DNL Real-time Customer Profile] pulls data from the Data Lake and persists customer profiles in its own separate data store.

## Consent schema structure {#structure}

There are two XDM mixins that provide customer consent fields that are required for TCF 2.0 support: one for record-based data ([!DNL XDM Individual Profile]), and another for time-series-based data ([!DNL XDM ExperienceEvent]):

| Schema | Beschreibung |
| --- | --- |
| Profile privacy mixin | Dieses Mixin erfasst die aktuellen Voreinstellungen für die Zustimmung eines Kunden. Bei Verwendung in einem [!DNL Profile]aktivierten Schema werden die in diesem Mixin angegebenen Werte als Wahrheitsquelle für die Art und Weise betrachtet, wie die Durchsetzung der Zustimmung auf die Daten eines Kunden angewendet werden sollte. |
| [!DNL Experience Event] Datenschutzmischung | Dieses Mixin erfasst die Präferenzen eines Kunden zur Einwilligung zu einem bestimmten Zeitpunkt. Die in diesen Feldern erfassten Daten können verwendet werden, um Änderungen in den Voreinstellungen für die Zustimmung des Kunden im Laufe der Zeit zu verfolgen. |

Während der Anwendungsfall der einzelnen Mixins unterschiedlich ist, sind die angegebenen Felder ungefähr gleich. Diese Felder werden im folgenden Abschnitt näher erläutert.

### Felder für Zustimmungsmixes {#privacy-mixin}

Während jede Kombination aus Datenschutz und Struktur der darin enthaltenen Felder unterschiedlich ist, stellen beide das `xdm:consentString` Attribut bereit, dessen Unterfelder für die TCF 2.0-Durchsetzung erforderlich sind. Die Struktur dieser Felder und die erwarteten Werte sind nachfolgend dargestellt:

```json
{
  "xdm:consentString": {
    "xdm:consentStandard": "IAB TCF",
    "xdm:consentStandardVersion": "2.0",
    "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
    "xdm:gdprApplies": true,
    "xdm:containsPersonalData": false
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:consentString` | Enthält die aktualisierten Zustimmungsdaten des Kunden und andere Kontextinformationen. |
| `xdm:consentStandard` | Der Rahmen für die Zustimmung, für den die Daten gelten. Für die TCF-Konformität sollte der Wert &quot;IAB TCF&quot;lauten. |
| `xdm:consentStandardVersion` | Die Versionsnummer des Genehmigungsrahmens, angegeben durch `xdm:consentStandard`. Bei TCF 2.0-Kompatibilität sollte der Wert &quot;2.0&quot;lauten. |
| `xdm:consentStringValue` | Die auf der Grundlage der vom Kunden ausgewählten Einstellungen für die Zustimmung generierte Zeichenfolge. |
| `xdm:gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für diesen Kunden gilt. Der Wert muss auf &quot;true&quot;gesetzt werden, damit eine TCF 2.0-Durchsetzung erfolgt. Die Standardeinstellung lautet &quot;false&quot;(falsch), wenn sie nicht enthalten ist. |
| `xdm:containsPersonalData` | Ein boolescher Wert, der angibt, ob die Aktualisierung der Zustimmung personenbezogene Daten enthält. Die Standardeinstellung lautet &quot;false&quot;(falsch), wenn sie nicht enthalten ist. |

## Schemas zur Kundengenehmigung erstellen {#create-schemas}

In the Platform UI, click **[!UICONTROL Schemas]** in the left navigation to open the *[!UICONTROL Schemas]workspace *. Gehen Sie von hier aus wie folgt vor, um jedes erforderliche Schema zu erstellen.

>[!NOTE]
>
>Wenn Sie vorhandene XDM-Schema haben, die Sie stattdessen zur Erfassung von Genehmigungsdaten verwenden möchten, können Sie diese Schema bearbeiten, anstatt neue zu erstellen. Bei der Bearbeitung vorhandener Schema ist es jedoch wichtig, die [Grundsätze der Schema-Evolution](../../../xdm/schema/composition.md#evolution) zu beachten, um Veränderungen zu vermeiden.

### Erstellen eines Schemas für die Einwilligung in einen Datensatz {#profile-schema}

Erstellen Sie auf der Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;im Arbeitsbereich &quot; *[!UICONTROL Schemas]&quot;ein neues Schema, das auf der *Klasse**[!DNL XDM Individual Profile]**basiert. Nachdem Sie das Schema im Schema-Editor geöffnet haben, klicken Sie auf der linken Seite der Arbeitsfläche unter dem Abschnitt &quot;**[!UICONTROL Mixins]**&quot;auf *[!UICONTROL Hinzufügen]*.

![](../assets/iab/add-mixin-profile.png)

The *[!UICONTROL Add mixin]* dialog appears. Wählen Sie hier in der Liste die Option **[!UICONTROL Profil Privacy]** . Sie können optional die Suchleiste verwenden, um die Ergebnisse einzuschränken, um das Mixin einfacher zu finden. Nachdem das Mixin ausgewählt ist, klicken Sie auf **[!UICONTROL Hinzufügen Mixin]**.

![](../assets/iab/add-profile-privacy.png)

Die Arbeitsfläche des Schema-Editors wird wieder angezeigt, sodass Sie die Struktur der hinzugefügten Felder für die Zustimmungszeichenfolge überprüfen können.

![](../assets/iab/profile-privacy-structure.png)

Wiederholen Sie von hier aus die oben genannten Schritte, um dem Schema die folgenden zusätzlichen Mixins hinzuzufügen:

* [!UICONTROL IdentityMap]
* [!UICONTROL Datenerfassungsregion für Profil]
* [!UICONTROL Angaben zur Person des Profils]
* [!UICONTROL Persönliche Angaben zum Profil]

![](../assets/iab/profile-all-mixins.png)

Wenn Sie ein vorhandenes Schema bearbeiten, das bereits für die Verwendung in aktiviert wurde, klicken Sie auf [!DNL Real-time Customer Profile]&quot; **[!UICONTROL Speichern]** &quot;, um die Änderungen zu bestätigen, bevor Sie mit dem Abschnitt zum [Erstellen eines Datensatzes auf der Grundlage Ihres Schemas](#dataset)für die Zustimmung fortfahren. Wenn Sie ein neues Schema erstellen, führen Sie die im Unterabschnitt unten beschriebenen Schritte aus.

#### Schema zur Verwendung in [!DNL Real-time Customer Profile]

Damit die [!DNL Real-time CDP] von ihr erhaltenen Daten mit bestimmten Profilen verknüpft werden können, muss das Schema für die Zustimmung zur Verwendung in diesem Bereich aktiviert werden [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Das in diesem Schema gezeigte Beispiel verwendet sein `identityMap` Feld als primäre Identität. Wenn Sie ein anderes Feld als primäre Identität festlegen möchten, stellen Sie sicher, dass Sie einen indirekten Bezeichner wie eine Cookie-ID verwenden und nicht ein direkt identifizierbares Feld, das nicht für interessensbasierte Werbung wie eine E-Mail-Adresse verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie nicht sicher sind, welche Felder eingeschränkt sind.
>
>Schritte zum Festlegen eines primären Identitätsfelds für ein Schema finden Sie im Lernprogramm zur Erstellung von [Schemas](../../../xdm/tutorials/create-schema-ui.md#identity-field).

To enable the schema for [!DNL Profile], click the schema&#39;s name in the left-hand rail to open the *[!UICONTROL Schema properties]* dialog in the right-hand rail. From here, click the **[!UICONTROL Profile]** toggle button.

![](../assets/iab/profile-enable-profile.png)

A popover appears, indicating a missing primary identity. Select the checkbox for using an alternate primary identity, as the primary identity will be contained in the identityMap field.

<img src="../assets/iab/missing-primary-identity.png" width="600" /><br>

Finally, click **[!UICONTROL Save]** to confirm your changes.

![](../assets/iab/profile-save.png)

### Create a time-series-based consent schema {#event-schema}

From the **[!UICONTROL Browse]** tab in the *[!UICONTROL Schemas]workspace *, create a new schema based on the**[!DNL XDM ExperienceEvent]class **. Once you have the schema open within the Schema Editor, click **[!UICONTROL Add]**under the *[!UICONTROL Mixins]*section on the left side of the canvas.

![](../assets/iab/add-mixin-event.png)

The *[!UICONTROL Add mixin]* dialog appears. From here, select **[!UICONTROL Experience event privacy mixin]** from the list. You can optionally use the search bar to narrow down results to locate the mixin easier. Once the mixin is selected, click **[!UICONTROL Add mixin]**.

![](../assets/iab/add-event-privacy.png)

The Schema Editor canvas reappears, showing the added consent string fields.

![](../assets/iab/event-privacy-structure.png)

From here, repeat the above steps to add the following additional mixins to the schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Details zur ExperienceEvent-Umgebung]
* [!UICONTROL ExperienceEvent-Webdetails]
* [!UICONTROL Details zur ExperienceEvent-Implementierung]

Once the mixins have been added, finish by clicking **[!UICONTROL Save]**.

![](../assets/iab/event-all-mixins.png)

## Erstellen Sie Datensätze basierend auf Ihren Schemas zur Einwilligung {#datasets}

For each of the required schemas described above, you must create a dataset that will ultimately ingest your customers&#39; consent data. Der auf dem [!DNL XDM Individual Profile] Schema basierende Datensatz muss aktiviert werden, [!DNL Real-time Customer Profile]während der auf dem [!DNL XDM ExperienceEvent] Schema basierende Datensatz nicht [!DNL Profile]aktiviert werden sollte.

Wählen Sie zunächst **[!UICONTROL Datasets]** in der linken Navigation und klicken Sie dann in der oberen rechten Ecke auf Dataset **[!UICONTROL erstellen]** .

![](../assets/iab/dataset-create.png)

On the next page, select **[!UICONTROL Create dataset from schema]**.

![](../assets/iab/dataset-create-from-schema.png)

Der _[!UICONTROL Arbeitsablauf zum Erstellen eines Datensatzes aus Schema]_wird angezeigt, beginnend mit dem Schritt zum_[!UICONTROL  Auswählen des Schemas]_ . Suchen Sie in der bereitgestellten Liste nach einem der Schema für die Zustimmung, die Sie zuvor erstellt haben. Sie können die Suche optional verwenden, um die Ergebnisse einzugrenzen und Ihr Schema einfacher zu finden. Klicken Sie auf das Optionsfeld neben dem Schema, um es auszuwählen, und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![](../assets/iab/dataset-select-schema.png)

Der Schritt _[!UICONTROL Datensatz konfigurieren]_wird angezeigt. Geben Sie einen eindeutigen, leicht identifizierbaren Namen und eine Beschreibung für den Datensatz ein, bevor Sie auf**[!UICONTROL  Fertig stellen ]**klicken.

![](../assets/iab/dataset-configure.png)

Die Detailseite für den neu erstellten Datensatz wird angezeigt. Wenn der Datensatz auf Ihrem [!DNL XDM ExperienceEvent] Schema basiert, ist der Vorgang abgeschlossen. Wenn der Datensatz auf Ihrem [!DNL XDM Individual Profile] Schema basiert, besteht der letzte Schritt darin, den Datensatz zur Verwendung in zu aktivieren [!DNL Real-time Customer Profile]. Klicken Sie in der rechten Leiste auf die Schaltfläche zum Umschalten des **[!UICONTROL Profils]** , um den Datensatz zu aktivieren.

![](../assets/iab/dataset-enable-profile.png)

Führen Sie die oben genannten Schritte erneut aus, um den anderen erforderlichen Datensatz für die TCF 2.0-Kompatibilität zu erstellen.

## Nächste Schritte

In diesem Lernprogramm haben Sie zwei Datensätze erstellt, die jetzt zur Erfassung von Daten zur Kundeneinwilligung verwendet werden können:

* Ein [!DNL Profile]aktivierter Datensatz, der auf Ihrem [!DNL XDM Individual Profile] Schema basiert.
* Ein auf Ihrem [!DNL XDM ExperienceEvent] Schema basierender Datensatz, für den nicht aktiviert ist [!DNL Profile].

Sie können nun zum [IAB TCF 2.0-Überblick](./overview.md#merge-policies) zurückkehren, um den Prozess der Konfiguration [!DNL Real-time CDP] für TCF 2.0-Compliance fortzusetzen.
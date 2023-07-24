---
title: Umgang mit Identitäten im Aktivierungs-Workflow für Ziele
description: Erfahren Sie, wie der Identitätsexport im Aktivierungs-Workflow je nach Zieltyp verarbeitet wird.
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 100%

---

# Umgang mit Identitäten im Aktivierungs-Workflow für Ziele

Auf dieser Seite wird beschrieben, wie Identitäten in verschiedene Zieltypen exportiert werden. Außerdem erfahren Sie, wie Sie ermitteln, welche Identitäten je nach Ziel für den Export verfügbar sind.

>[!TIP]
>
> Ausführliche Informationen zu Identitäten, Identity-Namespaces und Definitionen identitätsbezogener Begriffe finden Sie unter [Identity Service – Übersicht](/help/identity-service/home.md).

Jedes Ziel im [Katalog](/help/destinations/catalog/overview.md) ist ein wenig anders, sodass es keine universelle Einrichtung für alle Ziele gibt. Es gibt jedoch einige Muster, die die Einrichtung von Zielen und deren Identitätsanforderungen lenken, wie in den folgenden Abschnitten beschrieben.

## Dateibasierte Ziele {#file-based}

Für [dateibasierte Ziele](/help/destinations/destination-types.md#file-based) (z. B. [!DNL Amazon S3], SFTP oder die meisten E-Mail-Marketing-Ziele wie [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]) ist die Identitätseinrichtung bei den meisten dieser Ziele offen, d. h., Sie müssen keine Identität im Schritt [Attribute auswählen](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) des Batch-Aktivierungs-Workflows auswählen.

Wenn Sie Ihren Dateiexporten Identitäten hinzufügen möchten, beachten Sie, dass nur eine einzige Identität aus dem [Identity-Namespace](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) in einem Export ausgewählt werden kann. Wenn Sie eine Identität für den Export auswählen, wird sie automatisch als [obligatorisches Attribut](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) und [Deduplizierungsschlüssel](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys) ausgewählt.

![Eine als obligatorisches Attribut und Deduplizierungsschlüssel ausgewählte Identität](/help/destinations/assets/how-destinations-work/selected-identity.png)

Als Problemumgehung können Sie dem Export weitere Identitäten hinzufügen, wenn diese als Attribute in Experience Platform aufgenommen wurden. Im Folgenden finden Sie ein Beispiel, bei dem zusätzlich zum Identity-Namespace `Phone_E.164` die E-Mail-Adresse des XDM-Attributs für den Export ausgewählt wurde.

![Beispiel eines für den Export ausgewählten E-Mail-Adressen-Attributs](/help/destinations/assets/how-destinations-work/email-selected.png)

## Unterschiede zwischen dem Export einer Identität aus einer Identitätszuordnung und dem Export einer Identität als XDM-Attribut {#identity-map-or-attribute}

Die Anzahl der exportierten Datensätze kann unterschiedlich sein, je nachdem, ob Sie Identitäten aus der Identitätszuordnung für den Export auswählen oder Identitäten, die als Attribute in Experience Platform aufgenommen wurden. [Zusammenführungsrichtlinien](/help/profile/merge-policies/overview.md) spielen ebenfalls eine wichtige Rolle bei der Anzahl der Datensätze, die exportiert werden, wenn Sie Identitäten aus der Identitätszuordnung auswählen.

Angenommen, Ihnen liegen beispielsweise aus zwei verschiedenen Datensätzen die folgenden Profilfragmente vor, die zu einem Kundenprofil zusammengeführt werden:

**Profilfragment 1**

| Identitätszuordnung | Vorname | Nachname | E-Mail-Attribut |
|---------|----------|---------|--------|
| email1, Loyalty ID1 | John | Doe | email 1 |


**Profilfragment 2**

| Identitätszuordnung | Vorname | Nachname | E-Mail-Attribut |
|---------|----------|---------|--------|
| email2, Loyalty ID1 | John | Doe | email 2 |

Das zusammengeführte Profil würde wie folgt aussehen:

| Identitätszuordnung | Vorname | Nachname | E-Mail-Attribut |
|---------|----------|---------|--------|
| email1, email2, Loyalty ID1 | John | Doe | email 2 |

Das Exportverhalten variiert je nachdem, ob Sie `IdentityMap: Email` oder `xdm: personalEmail.address` für den Export auswählen.

Wenn kundenseitig `IdentityMap: Email` aktiviert wird, enthält die exportierte Datei zwei Datensätze, einen für email1 und einen weiteren für email2.

Wenn jedoch eine Kundin oder ein Kunde `xdm: personalEmail.address` aktiviert, ist nur email2 im Datensatz vorhanden, da das E-Mail-Attributfeld nur email2 umfasst. Hier sind verschiedene Anwendungsfälle möglich, je nachdem, ob Sie alle bei Ihnen hinterlegten Kunden-E-Mail-Adressen oder nur die neueste hinterlegte Kunden-E-Mail-Adresse aktivieren möchten.

Es bleibt festzuhalten, dass die Anzahl der zu exportierenden Datensätze von den ausgewählten Zusammenführungsrichtlinien sowie davon abhängt, ob Sie im Export Identitäten oder Attribute auswählen.

## API-basierte Streaming-Ziele {#streaming-destinations}

[API-basierte Streaming-Ziele](/help/destinations/destination-types.md#streaming-destination) mit [Destination SDK](/help/destinations/destination-sdk/overview.md) (z. B. [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze] und andere) unterstützen nur bestimmte IDs für den Export. Detaillierte Informationen zu den spezifischen Identitäten, die an die einzelnen Ziele exportiert werden können, finden Sie im Abschnitt zu *unterstützten Identitäten* auf jeder Zieldokumentationsseite (siehe zum Beispiel den Abschnitt zu [unterstützten Identitäten](/help/destinations/catalog/advertising/pinterest.md) auf der [!DNL Pinterest]-Zielseite).

Beachten Sie jedoch, dass Sie flexibel sind, Daten entweder aus [privaten Diagrammen](/help/profile/merge-policies/overview.md#id-stitching) oder aus Attributen als Identitäten zu nutzen. Dies bedeutet, dass Sie XDM-Attribute dem für das Ziel erforderlichen Identitätsfeld zuordnen können. Unten finden Sie ein Beispiel für das Ziel [!DNL Pinterest], wobei das XDM-Attribut `personalEmail.address` der erforderlichen [!DNL Pinterest]-Identität `pinterest_audience` zugeordnet ist.

>[!TIP]
>
>Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit Experience Platform die Daten bei Aktivierung automatisch hasht. Mehr über die Option **[!UICONTROL Umwandlung anwenden]** erfahren Sie im [Tutorial zur Aktivierung von Streaming-Zielen](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Beispiel eines E-Mail-Adressenattributs, das dem Identitätsfeld für ein Pinterest-Ziel zugeordnet ist.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Werbeziele, die auf Drittanbieterfirmen-Cookie-Integrationen angewiesen sind {#third-party-cookie-destinations}

Werbeziele, die auf Drittanbieterfirmen-Cookies angewiesen sind (z. B.: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) erfordern nicht, dass Kundinnen oder Kunden IDs im Aktivierungs-Workflow auswählen. Bei diesen Zielen überprüft Experience Platform bei der Einrichtung eines Aktivierungs-Workflows automatisch die vom [[!UICONTROL Experience Cloud-ID-Service]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) aufgebaute Tabelle für Identitätsübereinstimmung und exportiert alle Identitäten, die für ein Profil verfügbar sind und vom Ziel unterstützt werden.

Für diese Ziele ist eine ID-Synchronisierung entweder über den [!UICONTROL Experience Cloud-ID-Service] oder das [!UICONTROL Experience Platform Web SDK] erforderlich.

Wenn Sie das [!UICONTROL Experience Platform Web SDK] verwenden und der ältere [!UICONTROL Experience Cloud-ID-Service] nicht auf der Seite implementiert ist, müssen Sie sicherstellen, dass der Datenstrom für die betroffene Website aktiviert ist, um die Synchronisierung von Drittanbieterfirmen-IDs zu ermöglichen, wie in der [Dokumentation zum Konfigurieren eines Datenstroms](/help/datastreams/configure.md#create) beschrieben.

Beim Konfigurieren eines Datenstroms, wie in der oben verlinkten Dokumentation beschrieben, müssen Sie sicherstellen, dass der Regler **[!UICONTROL Synchronisierung der Drittanbieter-ID]** aktiviert ist. Die meisten Kundinnen und Kunden lassen das `container_id`-Feld leer (es enthält standardmäßig 0). Sie müssen diesen Wert nur ändern, wenn Ihre ältere Audience Manager-Implementierung eine bestimmte Container-ID verwendete (beachten Sie jedoch, dass dies nur die wenigsten Kundinnen und Kunden betrifft).

>[!NOTE]
>
>Die meisten dieser Werbeziele werden in Audience Manager unterstützt (diese Zieltypen werden in Audience Manager als gerätebasierte Ziele bezeichnet. Hier finden Sie eine [Liste aller unterstützten gerätebasierten Ziele in Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=de)). Nur wenige sind in Experience Platform aufgeführt. Informationen zur Datenfreigabe zwischen Experience Platform und Audience Manager finden Sie im Abschnitt zum [Aktivieren der Datenfreigabe von Experience Platform an Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#enable-aep-to-aam-data). Derzeit ist keine Unterstützung für weitere Drittanbieter-Cookie-Ziele geplant.

## Unternehmensziele {#enterprise-destinations}

[Unternehmensziele](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP-API) erfordern keine spezifischen IDs im Datenexport, da diese für Anwendungsfälle der Unternehmensintegration entwickelt wurden. Sie können jedoch bei Bedarf Identitäten als XDM-Attribute oder aus der Identitätszuordnung exportieren. Sehen Sie sich ein [Beispiel für an das HTTP-Ziel exportierte Daten](/help/destinations/catalog/streaming/http-destination.md#exported-data) an, das sowohl das `personalEmail.address`-XDM-Attribut als auch die Identitäten `ECID` und `email_lc_sha256` (gehashte E-Mail-Adresse) aus der Identitätszuordnung beinhaltet.

## Personalisierungsziele {#personalization-destinations}

[Personalisierungs- (oder Edge-)Ziele](/help/destinations/destination-types.md#edge-personalization-destinations) (z. B. Adobe Target, [!DNL Custom Personalization]) erfordern keine Identitätsauswahl im Aktivierungs-Workflow, da die Integration eine Profilsuche ist. Der Client ([!DNL Target], [!DNL Web SDK] oder andere) fragt [[!UICONTROL Edge]](/help/collection/home.md#edge) ab und ruft die Profilinformationen ab, die für die Personalisierung vor Ort erforderlich sind.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie herausfinden können, welche Identitäten für einzelne Ziele unterstützt oder erforderlich sind. Sie wissen außerdem, wie die Identitätsauswahl für jeden Zieltyp funktioniert.

Als Nächstes können Sie lesen, welche [Exporteinstellungen](/help/destinations/how-destinations-work/destinations-configurations.md) für Ziele in allen Zieltypen üblich sind, die von Entwicklerinnen und Entwicklern auf individueller Zielebene konfiguriert werden können, und welche Einstellungen Benutzende im Aktivierungs-Workflow bearbeiten können.

Sie können auch alle verfügbaren Ziele im [Katalog](/help/destinations/catalog/overview.md) finden.

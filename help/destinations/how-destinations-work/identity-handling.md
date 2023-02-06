---
title: Identitätsverarbeitung im Workflow für die Zielaktivierung
description: Erfahren Sie, wie der Identitätsexport im Aktivierungs-Workflow je nach Zieltyp verarbeitet wird.
source-git-commit: 6ccf26cbdbbe675d0d731f59cee589d63ca6f8ad
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 3%

---

# Identitätsverarbeitung im Workflow für die Zielaktivierung

Auf dieser Seite wird beschrieben, wie Identitäten in verschiedene Zieltypen exportiert werden. Außerdem erfahren Sie, wie Sie ermitteln, welche Identitäten je nach Ziel für den Export verfügbar sind.

>[!TIP]
>
> Ausführliche Informationen zu Identitäten, Identitäts-Namespaces und Definitionen identitätsbezogener Begriffe finden Sie in der [Übersicht über den Identitätsdienst](/help/identity-service/home.md).

Jedes Ziel im [Katalog](/help/destinations/catalog/overview.md) etwas anders ist, sodass es keine universelle Einrichtung für alle Ziele gibt. Es gibt jedoch einige Muster, die die Einrichtung von Zielen und deren Identitätsanforderungen leiten, wie in den folgenden Abschnitten beschrieben.

## Dateibasierte Ziele {#file-based}

Für [dateibasierte Ziele](/help/destinations/destination-types.md#file-based) (z. B. [!DNL Amazon S3], SFTP, die meisten E-Mail-Marketing-Ziele wie [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), ist die Identitätseinrichtung in den meisten dieser Ziele geöffnet, d. h., Sie müssen keine Identität in der [Attribute auswählen](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) Schritt des Batch-Aktivierungs-Workflows.

Wenn Sie Ihren Dateiexporten Identitäten hinzufügen möchten, beachten Sie, dass nur eine Identität aus der [Identitäts-Namespace](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) kann in einem Export ausgewählt werden. Wenn Sie eine Identität für den Export auswählen, wird sie automatisch als [mandatory attribute](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) und [Deduplizierungsschlüssel](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Eine Identität, die als obligatorisches Attribut und Deduplizierungsschlüssel ausgewählt wird.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Als Workaround können Sie dem Export weitere Identitäten hinzufügen, wenn diese als Attribute in Experience Platform aufgenommen wurden. Unten finden Sie ein Beispiel, bei dem zusätzlich zum Identitäts-Namespace die E-Mail-Adresse des XDM-Attributs für den Export ausgewählt wurde. `Phone_E.164`.

![Beispiel eines für den Export ausgewählten E-Mail-Adressen-Attributs.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exportieren einer Identität aus einer Identitätszuordnung im Vergleich zum Exportieren einer Identität als XDM-Attribut - die Unterschiede {#identity-map-or-attribute}

Die Anzahl der exportierten Datensätze kann unterschiedlich sein, je nachdem, ob Sie Identitäten aus der Identitätszuordnung für den Export auswählen oder Identitäten, die als Attribute in Experience Platform aufgenommen wurden. [Zusammenführungsrichtlinien](/help/profile/merge-policies/overview.md) spielen auch eine wichtige Rolle bei der Anzahl der Datensätze, die exportiert werden, wenn Sie Identitäten aus der Identitätszuordnung auswählen.

Angenommen, aus zwei verschiedenen Datensätzen bestehen die folgenden Profilfragmente, die zu einem Kundenprofil zusammengeführt werden:

**Profilfragment eins**

| Identitätszuordnung | Vorname | Nachname | Email-Attribut |
|---------|----------|---------|--------|
| email1, Loyalitäts-ID1 | John | Doe | email 1 |


**Profilfragment zwei**

| Identitätszuordnung | Vorname | Nachname | Email-Attribut |
|---------|----------|---------|--------|
| email2, Loyalitäts-ID1 | John | Doe | email 2 |

Das zusammengeführte Profil würde wie folgt aussehen:

| Identitätszuordnung | Vorname | Nachname | Email-Attribut |
|---------|----------|---------|--------|
| E-Mail 1, E-Mail2, Treueprogramm-ID1 | John | Doe | email 2 |

Das Exportverhalten variiert je nachdem, ob Sie `IdentityMap: Email` oder `xdm: personalEmail.address` für den Export.

Wenn ein Kunde aktiviert `IdentityMap: Email`, enthält die exportierte Datei zwei Datensätze, einen für email1 und einen weiteren für email2.

Wenn jedoch ein Kunde `xdm: personalEmail.address`, ist nur email2 im Datensatz enthalten, da das E-Mail-Attributfeld nur email2 enthält. In diesen Situationen können verschiedene Anwendungsfälle behandelt werden, bei denen Sie möglicherweise eine Aktivierung für alle E-Mail-Adressen vornehmen möchten, die für einen Kunden in einer Datei enthalten sind, oder nur für die neueste E-Mail-Adresse, über die Sie für den Kunden eine Datei erstellt haben.

Der Vorteil besteht darin, dass die Anzahl der zu exportierenden Datensätze von den ausgewählten Zusammenführungsrichtlinien und davon abhängt, ob Sie im Export Identitäten oder Attribute auswählen.

## API-basierte Streaming-Ziele {#streaming-destinations}

[API-basierte Streaming-Ziele](/help/destinations/destination-types.md#streaming-destination) mit [Destination SDK](/help/destinations/destination-sdk/overview.md) (z. B. [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]und andere) unterstützen nur bestimmte IDs für den Export. Detaillierte Informationen zu den spezifischen Identitäten, die an die einzelnen Ziele exportiert werden können, finden Sie im Abschnitt *unterstützte Identitäten* auf jeder Zieldokumentationsseite (siehe zum Beispiel [unterstützter Identitätsabschnitt](/help/destinations/catalog/advertising/pinterest.md) im [!DNL Pinterest] Zielseite).

Beachten Sie jedoch, dass Sie die Flexibilität haben, Daten aus [private Diagramme](/help/profile/merge-policies/overview.md#id-stitching) oder aus Attributen als Identitäten. Dies bedeutet, dass Sie XDM-Attribute dem für das Ziel erforderlichen Identitätsfeld zuordnen können. Unten finden Sie ein Beispiel für die [!DNL Pinterest] Ziel, wobei das XDM-Attribut `personalEmail.address` wird dem erforderlichen [!DNL Pinterest] identity `pinterest_audience`.

>[!TIP]
>
>Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, damit Experience Platform die Daten bei Aktivierung automatisch hasst. Mehr über **[!UICONTROL Umwandlung anwenden]** in der [Tutorial zur Aktivierung von Streaming-Zielen](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Beispiel eines E-Mail-Adressen-Attributs, das dem Identitätsfeld für das Pinterest-Ziel zugeordnet ist.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Werbeziele, die auf Drittanbieter-Cookie-Integrationen angewiesen sind {#third-party-cookie-destinations}

Werbeziele, die auf Drittanbieter-Cookies angewiesen sind (z. B.: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) erfordern nicht, dass Kunden IDs im Aktivierungs-Workflow auswählen. Bei diesen Zielen sucht Experience Platform bei der Einrichtung eines Aktivierungs-Workflows automatisch die von der [[!UICONTROL Experience Cloud-ID-Dienst]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) und exportiert alle Identitäten, die für ein Profil verfügbar und vom Ziel unterstützt werden.

Für diese Ziele ist eine ID-Synchronisierung erforderlich, die entweder über die [!UICONTROL Experience Cloud-ID-Dienst] oder [!UICONTROL Experience Platform Web SDK].

Wenn Sie [!UICONTROL Experience Platform Web SDK] und das Vermächtnis [!UICONTROL Experience Cloud-ID-Dienst] nicht auf der Seite implementiert ist, müssen Sie sicherstellen, dass der Datastrom für die betroffene Website aktiviert ist, um die Synchronisierung der Drittanbieter-IDs zu ermöglichen, wie in der [Dokumentation zum Datenspeicher konfigurieren](/help/edge/datastreams/configure.md#create).

Beim Konfigurieren eines Datastreams, wie in der oben stehenden Dokumentation beschrieben, müssen Sie sicherstellen, dass die Variable **[!UICONTROL Synchronisierung der Drittanbieter-ID]** aktiviert ist. Die meisten Kunden verlassen die `container_id` leer ist (standardmäßig 0). Sie müssen diesen Wert nur ändern, wenn Ihre ältere Audience Manager-Implementierung eine bestimmte Container-ID verwendet (beachten Sie jedoch, dass dies die große Minderheit von Kunden wäre).

>[!NOTE]
>
>Die meisten dieser Werbeziele werden in Audience Manager unterstützt (diese Zieltypen werden in Audience Manager als gerätebasierte Ziele bezeichnet). Siehe [Liste aller unterstützten gerätebasierten Ziele in Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Nur wenige sind in Experience Platform aufgeführt. Informationen zum Datenaustausch zwischen Experience Platform und Audience Manager finden Sie im Abschnitt unter [Datenfreigabe von Experience Platform an Audience Manager aktivieren](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). Derzeit ist keine Unterstützung für weitere Drittanbieter-Cookie-Ziele geplant.

## Enterprise-Ziele {#enterprise-destinations}

[Enterprise-Ziele](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP-API) erfordern keine spezifischen IDs im Datenexport, da diese für Anwendungsfälle der Unternehmensintegration entwickelt wurden. Sie können jedoch Identitäten als XDM-Attribute oder bei Bedarf aus der Identitätszuordnung exportieren. Anzeigen von [Beispiel für exportierte Daten an das HTTP-Ziel](/help/destinations/catalog/streaming/http-destination.md#exported-data), der sowohl die `personalEmail.address` XDM-Attribut und die Identitäten `ECID` und `email_lc_sha256` (gehashte E-Mail-Adresse) aus der Identitätszuordnung.

## Personalisierungsziele {#personalization-destinations}

[Personalisierungs- (oder Edge-)Ziele](/help/destinations/destination-types.md#edge-personalization-destinations) (z. B.: Adobe Target, [!DNL Custom Personalization]) erfordert keine Identitätsauswahl im Aktivierungs-Workflow, da die Integration eine Profilsuche ist. Der Client ([!DNL Target], [!DNL Web SDK], oder andere) die [[!UICONTROL Edge]](/help/collection/home.md#edge) und ruft die Profilinformationen ab, die für die Personalisierung vor Ort erforderlich sind.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie herausfinden können, welche Identitäten für einzelne Ziele unterstützt oder erforderlich sind. Jetzt wissen Sie auch, wie die Identitätsauswahl für jeden Zieltyp funktioniert.

Als Nächstes können Sie lesen, welche [Exporteinstellungen](/help/destinations/how-destinations-work/destinations-configurations.md) für Ziele sind in allen Zieltypen üblich, die von Entwicklern auf individueller Zielebene konfiguriert werden können und welche Einstellungen von Benutzern im Aktivierungs-Workflow bearbeitet werden können.
---
title: Merkury Enterprise Identity-Ziel
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Zielverbindung für Merkury Enterprise Identity erstellen.
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: a5452183-289c-49c3-9574-e09b0153dc00
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 15%

---

# Merkury Enterprise Identity-Ziel

>[!NOTE]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Merkury]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihren [!DNL Merkury].

## Überblick

Verwenden Sie das [!DNL Merkury Enterprise Identity] Ziel, um genauere, umfassendere und aufschlussreichere Verbraucherprofile zu erstellen. Mit verbesserten Profildaten können Marketing-Fachleute bessere Einblicke, Segmente und Modelle ermöglichen, was zu einer genaueren Zielgruppenbestimmung und prädiktiven Modellierung führt.

![Ein Diagramm, das die Verbindung zwischen Merkury und Experience Platform zeigt, einschließlich Aufnahme und Aktivierung](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Führen Sie die Schritte auf dieser Dokumentationsseite aus, um eine [!DNL Merkury Identity] Zielverbindung zu erstellen und Zielgruppen zur Identifizierung und Anreicherung über die Benutzeroberfläche von Adobe Experience Platform zu aktivieren.

>[!NOTE]
>
>Wenn Sie Zielgruppen für Medienziele mit Ihrem [!DNL Merkury Connect]-Konto aktivieren möchten, verwenden Sie stattdessen das [!DNL Merkury Connections] .

![Die Merkury Enterprise Identity-Zielkarte, die im Experience Platform-Zielkatalog hervorgehoben ist.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Anwendungsfälle

Das [!DNL Merkury Enterprise Identity]-Ziel bietet die Möglichkeit, Verbraucher-PII für die folgenden [!DNL Merkury] sicher zu übertragen:

* **Datenqualität**: Verbessern der Qualität von Verbraucherprofildaten durch Datenhygiene und -standardisierung. [!DNL Merkury] umfasst die US-Posthygiene und die Umzugskennzeichnung, um die fortschrittlichsten Anwendungsfälle für Direkt-Mail-Marketing zu unterstützen.
* **Identitätsauflösung**: Erstellen Sie eine genaue und umfassende Sicht auf den Kunden, die durch [!DNL Merkury] Personen- und Haushalts-IDs informiert wird. Merkury IDs bieten ein tiefes Maß an Profilverknüpfung, das von [!DNL Merkury] umfassenden US-amerikanischen Identitätsdiagramm für Erwachsene von über 268 Millionen Menschen unterstützt wird.
* **Anreicherung**: Bessere Einblicke und Personalisierung mit [!DNL Merkury Data]. [!DNL Merkury Data] enthält mehr als 10.000 verfügbare Datenattribute, von demografischen, Lifestyle-, Finanz-, Lebensereignis- und Kaufdaten aus der [!DNL Merkury Data Suite].

>[!NOTE]
>
>Diese Anwendungsfälle werden durch eine Kombination aus Ziel- und Quell-Connectoren ausgeführt. Der Kunde würde beginnen, indem er seine vorhandenen Kundendatensätze zur Anreicherung mit diesem Ziel-Connector exportiert. [!DNL Merkury]s Service würde nach der Datei suchen, sie abrufen, sie mit den Daten von [!DNL Merkury] anreichern und eine Datei generieren. Der Kunde würde dann die entsprechende [!DNL Merkury] Source Connector-Quellkarte verwenden, um die hydrierten Kundenprofile wieder in Adobe Real-Time CDP aufzunehmen.

## Voraussetzungen

>[!IMPORTANT]
>
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **Ziele anzeigen** und **Ziele verwalten**, **Ziele aktivieren**, **Profile anzeigen** und **Segmente anzeigen** [[Zugriffssteuerungsberechtigungen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lesen Sie die [[Übersicht über die Zugriffskontrolle]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie das **Identitätsdiagramm anzeigen** [[Zugriffssteuerungsberechtigung]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Unterstützte Identitäten {#supported-identities}

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| **Zielgruppe** | **Unterstützt** | **Beschreibung** |
|---|---|---|
| Segmentierungs-Service | ✓ | Zielgruppen, die über den Experience Platform [[Segmentierungs-Service]](https://experienceleague.adobe.com/de/docs/experience-platform/segmentation/home) generiert wurden. |
| Benutzerdefinierte Uploads | x | Audiences [[importiert]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) aus CSV-Dateien in Experience Platform. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| **Zielgruppe** | **Unterstützt** | **Herkunft Beschreibung** |
|---|---|---|      
| Segmentierungs-Service | ✓ | Zielgruppen, die über den Experience Platform [[Segmentierungs-Service]](https://experienceleague.adobe.com/de/docs/experience-platform/segmentation/home) generiert wurden. |
| Benutzerdefinierte Uploads | X | Audiences [[importiert]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) aus CSV-Dateien in Experience Platform. |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **Ziele anzeigen** und **Datensatzziele verwalten und aktivieren** [[Zugriffssteuerungsberechtigungen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lesen Sie die [[Übersicht über die Zugriffskontrolle]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, führen Sie die Schritte aus, die im [[Tutorial zur Zielkonfiguration]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination) beschrieben sind. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **Mit Ziel verbinden**.

Um auf Ihren Bucket in Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldeinformationen angeben:

| **Anmeldedaten** | **Beschreibung** |
|---|---|
| Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Bucket. Sie können diesen Wert vom Merkury-Team abrufen. |
| Geheimer Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom Merkury-Team abrufen. |
| Behältername | Dies ist der Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom Merkury-Team abrufen. |

{style="table-layout:auto"}

![Bildschirm zur Erstellung eines neuen Ziels](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Ausfüllen der Zieldetails

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Ein Screenshot mit Zieldetails](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Name (erforderlich)** - Der Name, unter dem das Ziel gespeichert wird
* **Beschreibung** - Kurze Erläuterung des Ziels
* **Behältername (erforderlich)** - Name des Amazon S3-Buckets, der auf S3 eingerichtet wurde
* **Ordnerpfad (erforderlich)** - Wenn Unterordner in einem Bucket verwendet werden, muss ein Pfad definiert werden, oder &#39;/&#39;, um auf den Stammpfad zu verweisen.
* **Dateityp** - Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Fragen Sie Ihr Merkury-Team nach dem erwarteten Dateityp für Ihr Konto.

>[!NOTE]
>
>Wenn Sie die CSV-Option auswählen, werden die Optionen Trennzeichen, Anführungszeichen, Escape-Zeichen, Leerer Wert, Null-Wert, Komprimierungsformat und Manifestdatei einschließen angezeigt. Wenden Sie sich an Ihr Merkury-Team, um die entsprechenden Einstellungen für Ihr Konto zu erhalten.

![Bild der CSV-Option](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Vorhandenes Konto

Konten, die bereits mit dem Merkury Enterprise Identity-Ziel definiert wurden, werden in einem Popup-Fenster mit einer Liste angezeigt. Wenn diese Option aktiviert ist, werden Details zum Konto in der rechten Leiste angezeigt. Sehen Sie sich das Beispiel über die Benutzeroberfläche an, wenn Sie zu **Ziele** > **Konten** navigieren.

![Screenshot des Zielkontos auf der Seite „Zielkonten“](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Aktivieren von Warnhinweisen

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](https://experienceleague.adobe.com/de/docs/experience-platform/destinations/ui/alerts).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **Weiter**.

## Aktivieren von Zielgruppen für dieses Ziel

>[!IMPORTANT]
>
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **Ziele anzeigen**, **Ziele aktivieren**, **Profile anzeigen** und **Segmente anzeigen**. Lesen Sie die Übersicht zur Zugriffskontrolle oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren von Identitäten benötigen Sie die Zugriffssteuerungsberechtigung **Identitätsdiagramm anzeigen** .

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele“.

## Zuordnungsvorschläge

Die korrekte Verarbeitung von Dateien auf der [!DNL Merkury] erfordert Namen- und Adresselemente. Es sind zwar nicht alle Elemente erforderlich, doch die Bereitstellung von so viel wie möglich hilft bei der erfolgreichen Zuordnung.

Mapping-Vorschläge sind in der folgenden Tabelle aufgeführt. In dieser Liste sind die Attribute auf der Zielseite aufgeführt, die von der [!DNL Merkury]-Verarbeitung verwendet werden, der Kundinnen und Kunden Profilattribute zuordnen können. Behandeln Sie diese Elemente als Vorschläge, da nicht alle Elemente erforderlich sind. Die Quellwerte hängen von den Anforderungen des Kontos ab.

| Zielfeld | Source-Beschreibung |
|---|---|
| id | Identitätsfeld, das zum Zuordnen [!DNL Merkury] Daten zu Experience Platform über den [!DNL Merkury Enterprise Identity] Source-Connector verwendet werden soll |
| input_first_name | Der `person.name.firstName` Wert in Experience Platform. |
| input_last_name | Der `person.name.lastName` Wert in Experience Platform. |
| input_address_line_1 | Der `mailingAddress.street` Wert in Experience Platform. |
| input_city | Der `mailingAddress.city` Wert in Experience Platform. |
| input_state_Province_code | Der `mailingAddress.state` Wert in Experience Platform. Verwenden Sie , wenn der Status im Code-Formular mit zwei Zeichen vorliegt. |
| input_state_Province_name | Der `mailingAddress.state` Wert in Experience Platform. Verwenden Sie , wenn der Status der vollständige Statusname ist. |
| input_postal_code | Der `mailingAddress.postalCode` Wert in Experience Platform. |
| input_email_address | Der Wert, den Sie als E-Mail-Adresse der Profile zuordnen möchten. |
| input_phone | Der Wert, den Sie als Telefonnummer der Profile zuordnen möchten. |

{style="table-layout:auto"}

## Überprüfen des Datenexports

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren Amazon S3-Speicher-Bucket und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Datennutzung und -Governance

Alle Adobe Experience Platform-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie Adobe Experience Platform Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Profildaten aus Experience Platform an Ihren [!DNL Merkury] verwalteten S3-Speicherort zu exportieren. Als Nächstes müssen Sie sich mit dem Namen des Kontos, den Dateinamen und dem Pfad des Buckets an Ihren [!DNL Merkury] wenden, damit die Verarbeitung eingerichtet werden kann.

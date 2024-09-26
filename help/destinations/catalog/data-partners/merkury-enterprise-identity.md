---
title: Merkury Enterprise Identity Destination
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Verbindung zum Enterprise Identity-Ziel von Merkury erstellen.
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: a5452183-289c-49c3-9574-e09b0153dc00
source-git-commit: 2b84b5106105339ab243a9f4412b47692caedf3c
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 18%

---

# Merkury Enterprise Identity Destination

>[!NOTE]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Merkury]-Team erstellt und gepflegt. Wenden Sie sich bei Fragen oder Aktualisierungsanfragen an Ihren [!DNL Merkury] Kundenbetreuer.

## Übersicht

Verwenden Sie das Ziel &quot;[!DNL Merkury Enterprise Identity]&quot;, um genauere, umfassendere und aufschlussreichere Verbraucherprofile zu erstellen. Dank verbesserter Profildaten können Marketingexperten bessere Einblicke, Segmente und Modelle gewinnen, was zu genauerer Zielgruppenbestimmung und prädiktiver Modellierung führt.

![Ein Diagramm, das die Verbindung zwischen Merkury und Experience Platform zeigt, einschließlich Aufnahme und Aktivierung](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Führen Sie die Schritte auf dieser Dokumentationsseite aus, um eine 0-Ziel-Verbindung zu erstellen und Zielgruppen zur Identifizierung und Anreicherung mithilfe der Adobe Experience Platform-Benutzeroberfläche zu aktivieren.[!DNL Merkury Identity]

>[!NOTE]
>
>Wenn Sie Zielgruppen mit Ihrem [!DNL Merkury Connect] -Konto für Medienziele aktivieren möchten, verwenden Sie stattdessen das Ziel [!DNL Merkury Connections] .

![Die im Experience Platform-Zielkatalog hervorgehobene Merkury Enterprise Identity-Zielkarte.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Anwendungsfälle

Das Ziel [!DNL Merkury Enterprise Identity] bietet die Möglichkeit, personenbezogene Daten von Verbrauchern sicher für die folgenden [!DNL Merkury]-Funktionen zu übertragen:

* **Datenqualität**: Verbessern Sie die Qualität der Kundenprofil-Daten durch Datenhygiene und -standardisierung. [!DNL Merkury] beinhaltet US-Posthygiene und die Bewegungserkennung zur Unterstützung der fortschrittlichsten Anwendungsfälle für das Briefpost-Marketing.
* **Identitätsauflösung**: Erstellen Sie eine genaue und umfassende Einzelansicht des Kunden, die von [!DNL Merkury] individuellen und Haushalts-IDs informiert wird. Merkurkunden-IDs bieten ein tiefes Maß an Profilverknüpfung basierend auf dem umfassenden US-Identitätsdiagramm für erwachsene Verbraucher von [!DNL Merkury] von über 268 Millionen Menschen.
* **Anreicherung**: Erhöhen Sie Ihre Einblicke und Personalisierung mit [!DNL Merkury Data]. [!DNL Merkury Data] enthält mehr als 10.000 verfügbare Datenattribute, von demografischen Daten, Lebensstil-, Finanz-, Lebensereignissen und Kaufdaten aus dem [!DNL Merkury Data Suite].

>[!NOTE]
>
>Diese Anwendungsfälle werden über eine Kombination aus Ziel- und Quell-Connectoren ausgeführt. Der Kunde exportiert zunächst seine vorhandenen Kundendatensätze zur Anreicherung mithilfe dieses Ziel-Connectors. Der Dienst von [!DNL Merkury] würde nach der Datei suchen, sie abrufen, sie mit den Daten von [!DNL Merkury] anreichern und eine Datei generieren. Der Kunde verwendet dann die entsprechende Source-Connector-Quellkarte, um die hydrierten Kundenprofile wieder in Adobe Real-Time CDP aufzunehmen.[!DNL Merkury]

## Voraussetzungen

>[!IMPORTANT]
>
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **Ziele anzeigen** und **Ziele verwalten**, **Ziele aktivieren**, **Profile anzeigen** und **Segmente anzeigen** [[Zugriffssteuerungsberechtigungen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lesen Sie den Abschnitt &quot;[[Zugriffskontrolle - Übersicht]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)&quot;oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Um *Identitäten* zu exportieren, benötigen Sie die **Identitätsdiagramm anzeigen** [[Zugriffssteuerungsberechtigung]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Unterstützte Identitäten {#supported-identities}

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| **Zielgruppe** | **Unterstützt** | **Beschreibung** | **origin** |
|---|---|---|---|
| Segmentierungs-Service | ✓ | Zielgruppen, die durch die Experience Platform [[Segmentierungsdienst]](https://experienceleague.adobe.com/de/docs/experience-platform/segmentation/home) generiert wurden. |
| Benutzerdefinierte Uploads | x | Zielgruppen [[importiert]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) aus CSV-Dateien in Experience Platform. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| **Zielgruppe** | **Unterstützt** | **Beschreibung origin** |
|---|---|---|      
| Segmentierungs-Service | ✓ | Zielgruppen, die durch die Experience Platform [[Segmentierungsdienst]](https://experienceleague.adobe.com/de/docs/experience-platform/segmentation/home) generiert wurden. |
| Benutzerdefinierte Uploads | X | Zielgruppen [[importiert]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) aus CSV-Dateien in Experience Platform. |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **Ziele anzeigen** und **Datensatzziele verwalten und aktivieren** [[Zugriffssteuerungsberechtigungen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lesen Sie den Abschnitt &quot;[[Zugriffskontrolle - Übersicht]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)&quot;oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [[Zielkonfiguration]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination) beschrieben sind. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **Mit Ziel verbinden** aus.

Um auf Ihren Bucket auf dem Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldedaten angeben:

| **Credential** | **Beschreibung** |
|---|---|
| Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Behälter. Sie können diesen Wert vom Merkury-Team abrufen. |
| Geheimer Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom Merkury-Team abrufen. |
| Behältername | Dies ist Ihr Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom Merkury-Team abrufen. |

{style="table-layout:auto"}

![Bildschirm zur Erstellung eines neuen Ziels](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Ausfüllen der Zieldetails

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Zieldetails](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Name (erforderlich)** - Der Name, unter dem das Ziel gespeichert wird
* **Beschreibung** - Kurze Erläuterung des Zwecks des Ziels
* **Behältername (erforderlich)** - Name des auf S3 eingerichteten Amazon S3-Behälters
* **Ordnerpfad (erforderlich)** - Wenn Unterverzeichnisse in einem Behälter verwendet werden, muss ein Pfad definiert sein oder &quot;/&quot;, um auf den Stammpfad zu verweisen.
* **Dateityp** - Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Fragen Sie Ihr Merkury-Team nach dem erwarteten Dateityp für Ihr Konto.

>[!NOTE]
>
>Bei der Auswahl der CSV-Option werden die Optionen Trennzeichen, Anführungszeichen, Escape-Zeichen, Leerwert, Null-Wert, Komprimierungsformat und Manifestdatei einschließen angezeigt. Wenden Sie sich an Ihr Merkury-Team, um die entsprechenden Einstellungen für Ihr Konto zu erhalten.

![Bild der CSV-Option](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Vorhandenes Konto

Konten, die bereits mit dem Merkury Enterprise Identity-Ziel definiert wurden, werden in einem Listen-Popup angezeigt. Wenn diese Option aktiviert ist, werden Details zum Konto in der rechten Leiste angezeigt. Zeigen Sie das Beispiel in der Benutzeroberfläche an, wenn Sie zu **Ziele** > **Konten** navigieren.

![Screenshot des Zielkontos auf der Seite der Zielkonten](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Aktivieren von Warnhinweisen

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](https://experienceleague.adobe.com/de/docs/experience-platform/destinations/ui/alerts).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **Weiter** aus.

## Aktivieren von Zielgruppen für dieses Ziel

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die Zugriffssteuerungsberechtigungen **Ziele anzeigen**, **Ziele aktivieren**, **Profile anzeigen** und **Segmente anzeigen** . Lesen Sie die Übersicht zur Zugriffskontrolle oder kontaktieren Sie Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Um Identitäten zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **Identitätsdiagramm anzeigen** .

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) .

## Vorschläge zuordnen

Für die korrekte Verarbeitung von Dateien auf der Seite [!DNL Merkury] sind Name und Adresselemente erforderlich. Auch wenn nicht alle Elemente erforderlich sind, hilft eine möglichst umfassende Bereitstellung bei der erfolgreichen Zuordnung.

Zuordnungsvorschläge werden in der folgenden Tabelle bereitgestellt, in der Attribute auf Ihrer Zielseite aufgelistet werden, die von der [!DNL Merkury] -Verarbeitung verwendet werden, der Kunden Profilattribute zuordnen können. Behandeln Sie diese Elemente als Vorschläge, da nicht alle Elemente erforderlich sind und die Quellwerte von den Anforderungen des Kontos abhängen.

| Zielfeld | Source-Beschreibung |
|---|---|
| id | Identitätsfeld für die Zuordnung von [!DNL Merkury] -Daten zum Experience Platform über den [!DNL Merkury Enterprise Identity] Source-Connector |
| input_first_name | Der `person.name.firstName` -Wert in Experience Platform. |
| input_last_name | Der `person.name.lastName` -Wert in Experience Platform. |
| Input_Address_Line_1 | Der `mailingAddress.street` -Wert in Experience Platform. |
| Input_City | Der `mailingAddress.city` -Wert in Experience Platform. |
| Input_State_Province_code | Der `mailingAddress.state` -Wert in Experience Platform. Verwenden Sie diese Option, wenn der Status im Formular mit dem Code für zwei Zeichen vorliegt. |
| Input_State_Province_Name | Der `mailingAddress.state` -Wert in Experience Platform. Verwenden Sie , wenn der Status der vollständige Statusname ist. |
| input_postal_code | Der `mailingAddress.postalCode` -Wert in Experience Platform. |
| input_email_address | Der Wert, den Sie als Profil-E-Mail-Adresse zuordnen möchten. |
| Input_Phone | Der Wert, den Sie als Telefonnummer für Profile zuordnen möchten. |

{style="table-layout:auto"}

## Überprüfen des Datenexports

Um zu überprüfen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren Amazon S3-Speicher-Bucket und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Datennutzung und -Governance

Alle Adobe Experience Platform-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie Adobe Experience Platform Data Governance durchsetzt, finden Sie in der [Übersicht zu Data Governance](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Profildaten von Experience Platform an Ihren von [!DNL Merkury] verwalteten S3-Speicherort zu exportieren. Als Nächstes müssen Sie sich an Ihren [!DNL Merkury]-Support-Mitarbeiter mit dem Namen des Kontos, den Dateinamen und dem Behälterpfad wenden, damit die Verarbeitung eingerichtet werden kann.

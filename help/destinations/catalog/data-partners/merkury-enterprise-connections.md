---
title: Merkury Enterprise Connections Destination
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Enterprise Connections-Zielverbindung für Merkury erstellen.
hide: true
hidefromtoc: true
source-git-commit: 66a0a085e696dbe13d0368da395f655c7ca01a97
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 20%

---

# Merkury Enterprise Connections Destination

>[!NOTE]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom Merkury-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihren Merkury-Kundenbetreuer.

## Übersicht

Verwenden Sie das Ziel Enterprise Connections von Merkury, um Merkury sichere Zielgruppen bereitzustellen. Merkury bietet Marketing-Experten eine einfache Abstimmung und Bereitstellung personalbasierter Zielgruppen zu Merkurys über 80 adressierbaren TV-/CTV-, Herausgeber- und Ad-Tech-Verbindungen. Merkury basiert auf einem umfassenden US-Diagramm zur Identität erwachsener Verbraucher mit über 268 Millionen Menschen.

![Ein Diagramm, das die Verbindung zwischen Merkury und Experience Platform zeigt, einschließlich Aufnahme und Aktivierung](../../assets/catalog/data-partners/merkury-connections/media/image1.png)

Führen Sie die Schritte auf dieser Dokumentationsseite aus, um eine Zielverbindung für Merkury-Verbindungen zu erstellen und Zielgruppen über die Adobe Experience Platform-Benutzeroberfläche zu aktivieren.

>[!NOTE]
>
>Wenn Sie mit Ihrem Merkury Connect-Konto Zielgruppen für Medienziele aktivieren möchten, verwenden Sie stattdessen unser Ziel für Merkury-Verbindungen .

![Die Zielkarte Merkury Enterprise Conections , die im Experience Platform-Zielkatalog hervorgehoben ist.](../../assets/catalog/data-partners/merkury-connections/media/image2.png)

## Anwendungsfälle

* **Aktivierung für digitale Medien**: Einfache Zuordnung und Bereitstellung Ihrer Zielgruppenprofile zu den mehr als 50 adressierbaren Herausgebern von Merkury und Ad-Tech-Verbindungen.
* **Effizienzsteigerung**: Erhöhen Sie Ihre Cookie-lose, adressierbare Medienreichweite, verbessern Sie die Targeting-Effizienz und die ROAS-Kosten (Return on Advertising Spend).

## Voraussetzungen

>[!IMPORTANT]
>
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **Ziele anzeigen** und **Ziele verwalten**, **Ziele aktivieren**, **Anzeigen von Profilen**, und **Segmente anzeigen** [[Zugriffssteuerungsberechtigungen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lesen Sie die [[Zugriffskontrolle - Übersicht]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **Identitätsdiagramm anzeigen** [[Zugriffssteuerungsberechtigung]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](../../assets/catalog/data-partners/merkury-connections/media/image3.png)

## Unterstützte Identitäten {#supported-identities}

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Siehe folgendes Dokument unter [ECID](/help/identity-service/features/ecid.md) für weitere Informationen. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| **Zielgruppe** | **Unterstützt** | **Ursprung der Beschreibung** |
|---|---|---|      
| Segmentierungs-Service | ✓ | Über die Experience Platform generierte Zielgruppen [[Segmentation Service]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Benutzerdefinierte Uploads | X | Zielgruppen [[importiert]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform aus CSV-Dateien. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| **Posten** | **Typ** | **Hinweise** |
|---|---|---|  
| Exporttyp | **Profilbasiert** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute auswählen der [[Zielaktivierungs-Workflow]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations#select-attributes). |
| Häufigkeit | **Batch** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [[Batch-dateibasierte Häufigkeitsziele]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-types#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **Ziele anzeigen** und **Verwalten und Aktivieren von Datensatzzielen** [[Zugriffssteuerungsberechtigungen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lesen Sie die [[Zugriffskontrolle - Übersicht]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Gehen Sie wie im Abschnitt [[Tutorial zur Zielkonfiguration]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren

Füllen Sie die erforderlichen Felder aus und wählen Sie **Mit Ziel verbinden**.

Um auf Ihren Bucket auf dem Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldedaten angeben:


| **Berechtigung** | **Beschreibung** |
|---|---|
| Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Behälter. Sie können diesen Wert vom Merkury-Team abrufen. |
| Geheimer Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom Merkury-Team abrufen. |
| Behältername | Dies ist Ihr Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom Merkury-Team abrufen. |

{style="table-layout:auto"}

![Bildschirm zur Zielerstellung](../../assets/catalog/data-partners/merkury-connections/media/image4.png)

### Ausfüllen der Zieldetails

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Zieldetails](../../assets/catalog/data-partners/merkury-connections/media/image6.png)

* **Name (erforderlich)** - Der Name, unter dem das Ziel gespeichert wird
* **Beschreibung** - Kurze Erläuterung des Ziels des Bestimmungsorts
* **Behältername (erforderlich)** - Name des auf S3 eingerichteten Amazon S3-Buckets
* **Ordnerpfad (erforderlich)** - Wenn Unterverzeichnisse in einem Behälter verwendet werden, muss ein Pfad definiert werden, oder &quot;/&quot;, um auf den Stammpfad zu verweisen.
* **Dateityp** - Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Fragen Sie Ihr Merkury-Team nach dem erwarteten Dateityp für Ihr Konto.

>[!NOTE]
>
>Bei Auswahl der CSV-Option werden die Optionen Trennzeichen, Anführungszeichen, Escape-Zeichen, Leerwert, Null-Wert, Komprimierungsformat und Manifestdatei einschließen angezeigt. Wenden Sie sich an Ihr Merkury-Team, um die entsprechenden Einstellungen für Ihr Konto zu erhalten.

![Bild der CSV-Optionen](../../assets/catalog/data-partners/merkury-connections/media/image8.png)

### Vorhandenes Konto

Konten, die bereits mit dem Ziel &quot;Enterprise Connections&quot;von Merkury definiert wurden, werden in einem Listen-Popup angezeigt. Wenn diese Option aktiviert ist, werden Details zum Konto in der rechten Leiste angezeigt. Zeigen Sie das Beispiel in der Benutzeroberfläche an, wenn Sie zu **Ziele** > **Konten**;

![Screenshot des Zielkontos auf der Seite der Zielkonten](../../assets/catalog/data-partners/merkury-connections/media/image5.png)

## Aktivieren von Warnhinweisen

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **Nächste**.

## Aktivieren von Zielgruppen für dieses Ziel

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die Zugriffssteuerungsberechtigungen Ziele anzeigen, Ziele aktivieren, Profile anzeigen und Segmente anzeigen . Lesen Sie die Übersicht zur Zugriffskontrolle oder kontaktieren Sie Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Um Identitäten zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung für Identitätsdiagramme anzeigen .


Lesen [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## Vorschläge zuordnen

Die korrekte Verarbeitung von Dateien auf der Merkurseite erfordert Name- und Adresselemente. Auch wenn nicht alle Elemente erforderlich sind, hilft eine möglichst umfassende Bereitstellung bei der erfolgreichen Zuordnung.

Zuordnungsvorschläge finden Sie in der folgenden Tabelle, in der Attribute auf Ihrer Zielseite aufgelistet werden, die von der Merkury-Verarbeitung verwendet werden und denen Kunden Profilattribute zuordnen können. Behandeln Sie diese Elemente als Vorschläge, da nicht alle Elemente erforderlich sind und die Quellwerte von den Anforderungen des Kontos abhängen.

| Zielfeld | Quellbeschreibung |
|---|---|
| id | Identitätsfeld, das verwendet wird, um Daten aus der Metrik über den Quell-Connector für die Enterprise Identity-Lösung von Merkury an die Experience Platform zuzuordnen |
| input_first_name | Die `person.name.firstName` -Wert in Experience Platform. |
| input_last_name | Die `person.name.lastName` -Wert in Experience Platform. |
| Input_Address_Line_1 | Die `mailingAddress.street` -Wert in Experience Platform. |
| Input_City | Die `mailingAddress.city` -Wert in Experience Platform. |
| Input_State_Province_code | Die `mailingAddress.state` -Wert in Experience Platform. Verwenden Sie diese Option, wenn der Status im Formular mit dem Code für zwei Zeichen vorliegt. |
| Input_State_Province_Name | Die `mailingAddress.state` -Wert in Experience Platform. Verwenden Sie , wenn der Status der vollständige Statusname ist. |
| input_postal_code | Die `mailingAddress.postalCode` -Wert in Experience Platform. |
| input_email_address | Der Wert, den Sie als Profil-E-Mail-Adresse zuordnen möchten. |
| Input_Phone | Der Wert, den Sie als Telefonnummer für Profile zuordnen möchten. |

{style="table-layout:auto"}

## Überprüfen des Datenexports

Um zu überprüfen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren Amazon S3-Speicher-Bucket und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Datennutzung und -Governance

Alle Adobe Experience Platform-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie Adobe Experience Platform Data Governance durchsetzt, finden Sie im Abschnitt [Data Governance - Übersicht](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Profildaten von Experience Platform an Ihren von Merkury verwalteten S3-Speicherort zu exportieren. Als Nächstes müssen Sie sich an Ihren Merkury-Kundenbetreuer mit dem Namen des Kontos, den Dateinamen und dem Behälterpfad wenden, damit die Verarbeitung eingerichtet werden kann.
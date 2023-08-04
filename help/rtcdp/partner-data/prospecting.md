---
title: (Beta) Engage und Akquisition neuer Kunden durch Nutzungsszenarien für die Prospektion
description: Erfahren Sie, wie Sie durch die Unterstützung von Partnerdaten in Real-Time CDP neue Kunden durch Nutzungsszenarios gewinnen und gewinnen können.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 2e2a473efd247cb235ee7e8f94058baa48fd1b1a
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 16%

---

# Engagieren und Akquirieren neuer Kunden durch Nutzungsszenarien für die Prospektion

>[!AVAILABILITY]
>
>* Diese Betafunktion steht Kundinnen und Kunden zur Verfügung, die Real-Time CDP (App-Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime und Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie in den [Produktbeschreibungen](https://helpx.adobe.com/de/legal/product-descriptions.html) und erhalten Sie von Ihrem Adobe-Support-Team.

Nutzen Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, um Ihre Profilbasis mit potenziellen Profilen von Datenpartnern zu erweitern und mit ihnen Kontakt aufzunehmen, um neue Kunden zu gewinnen oder zu erreichen.

![Kundenprospektion Anwendungsfall - Überblick über die allgemeine visuelle Darstellung.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie erwägen, mithilfe der Unterstützung von Partnerdaten in Real-Time CDP neue Kunden anzusprechen und zu gewinnen, sollten Sie die folgenden Voraussetzungen in Ihrem Planungsprozess berücksichtigen:

* Wie häufig erwarten Sie, dass von Partnern bereitgestellte Profile in Real-Time CDP aufgenommen und aktualisiert werden?
* Welche Identitäten benötigen Ihre nachgelagerten Ziele?
* Stellen Sie sicher, dass die erfassten Kennungen nachgelagert verarbeitet werden können.
* Sind die Partnerdaten, die Sie erfassen, an eine allgemein akzeptierte dauerhafte Kennung wie personenbezogene Daten (PII), Hash-personenbezogene Daten oder eine Partner-ID gebunden?
* Welche Datennutzungsrichtlinien müssen Sie aus der Partnerperspektive und aus Ihrem eigenen Rechts-, Datenschutz- oder Compliance-Team kennen?

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

Bevor Sie Real-Time CDP erweitern, um neue Kunden zu gewinnen, stellen Sie sicher, dass Sie Real-Time CDP verwenden, um eine robuste Grundlage für Ihre Erstanbieter-Daten zu schaffen. Die Workflows zur Erreichung dieses Anwendungsfalls ähneln Workflows, mit denen Sie mit Ihren bekannten Kunden interagieren.

![Kundenprospektion Anwendungsfall - Überblick über die allgemeine visuelle Darstellung.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Als **customer**, können Sie Interessenten-Profile aus einem oder mehreren **Datenpartner** , um die Trichterkundenakquise zu optimieren.
2. Als **customer**, erweitern Sie Ihre Profildaten und Ihr Governance-Modell, um die **Partner**- eine Liste mit Interessenten-Profilen.
3. Als **customer**, laden Sie potenzielle Profile in Real-Time CDP und erstellen Sie Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Als **customer**, erstellen Sie zielgerichtete Zielgruppen aus der Liste der potenziellen Profile.
5. Als **customer** aktivieren Sie potenzielle Zielgruppen für Ziele, die die in Ihrer Interessentenliste verfügbaren Identitäten akzeptieren.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** für die Aktivierung von Zielgruppen über die letzte Meile an die gewünschten Paid-Media-Ziele.

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte, die Links zu weiterführender Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Benutzeroberflächenfunktionen und -elemente, die Sie verwenden {#ui-functionality-and-elements}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, nutzen Sie die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente (aufgelistet in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

* [Identitäten](/help/identity-service/namespaces.md)
* [Schemata](/help/xdm/home.md)
* [Datennutzungskennzeichnungen](/help/data-governance/labels/overview.md)
* [Datensätze](/help/catalog/datasets/overview.md)
* [Quellen](/help/sources/home.md)
* Profile (Link zu potenziellen Profilen)
* Zielgruppen (Link zum Anzeigen von Zielgruppen)
* [Ziele](/help/destinations/home.md)

### Lizenzieren von Profildetails von Drittanbietern vom Partner {#license-profiles-from-partner}

Dieser Schritt wird im Abschnitt [Voraussetzungen](#prerequisites-and-planning) und Adobe setzt voraus, dass Sie über die richtigen vertraglichen Vereinbarungen mit vertrauenswürdigen Datenanbietern verfügen, um vom Datenpartner bereitgestellte Prospektprofile zu erfassen.

### Erweitern Sie Ihre Profildaten und Ihr Governance-Modell, um von Partnern bereitgestellte Profile aufzunehmen. {#extend-governance-model}

Zur Vorbereitung auf den Empfang von potenziellen Profilen von Ihrem Datenpartner müssen Sie Ihr Data-Management-Framework in Real-Time CDP erweitern, um diesen neuen Profiltyp aufzunehmen.

Die Identitäts-, Daten- und Governance-Komponenten, die Sie verwenden werden, sind:

* Eine neue **[!UICONTROL Partner-ID]** Identitätstyp für die vom Partner bereitgestellten Profile
* Eine neue **[!UICONTROL XDM Individual Prospect Profile]** XDM-Klasse
* **(Dokumentation in Kürze verfügbar)** Auf die Partnerdatenunterstützung zugeschnittene Feldergruppen
* **(Dokumentation in Kürze verfügbar)** Drittanbieterbeschriftungen, die Sie zu den Attributen hinzufügen, die von Partnern eingehen

#### Erstellen eines Identitäts-Namespace der Partner-ID {#create-partner-id-namespace}

Erstellen Sie zunächst einen neuen Identitätstyp für die Profile, die Sie vom Partner erhalten. Dazu müssen Sie im Abschnitt Identität einen neuen Identitäts-Namespace des Typs **[!UICONTROL Partner-ID]**.

![Erstellen Sie einen neuen Identitäts-Namespace für die Partner-ID.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Weitere Informationen zu Partner-ID-Namespaces finden Sie im Abschnitt [Identitätstypen-Abschnitt](/help/identity-service/namespaces.md).
* Lesen Sie die Anweisungen zum [Definieren von Identitätsfeldern](/help/xdm/ui/fields/identity.md) in der Experience Platform-Benutzeroberfläche.

#### Erstellen Sie ein neues Schema mit der **[!UICONTROL XDM Individual Prospect Profile]** class

Als Nächstes in **[!UICONTROL Data Management]** > **[!UICONTROL Schemas]**, erstellen Sie ein neues Schema und weisen Sie ihm das **[!UICONTROL XDM Individual Prospect Profile]** -Klasse.

![Suchen Sie im XDM-Schema-Builder nach der Klasse &quot;XDM Individual Prospect Profile&quot;.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Lesen der Anleitung [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](/help/xdm/ui/resources/schemas.md) und erhalten Sie vollständige Informationen zur Klasse &quot;XDM Individual Prospect Profile&quot;(Link bevorsteht).

Die **[!UICONTROL XDM Individual Prospect Profile]** -Klasse ist mit den unten aufgeführten Feldern vorkonfiguriert. Um Ihr Schema mit von Partnern bereitgestellten Attributen für die potenziellen Profile anzureichern, können Sie entweder eine neue Feldergruppe mit den erwarteten Attributen erstellen und zum Schema hinzufügen oder eine der von Adobe bereitgestellten vorkonfigurierten Feldergruppen verwenden.

![Vorkonfigurierte Felder für die Klasse XDM Individual Prospect Profile .](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Als Nächstes müssen Sie die zuvor erstellte partnerID-Identität als primäre Identität für das Schema auswählen. Profildatensätze müssen eine primäre Kennung aufweisen. Dieser Schritt ist erforderlich, um sicherzustellen, dass Interessensdaten in den Profilspeicher geladen und für die Segmentierung und Aktivierung verfügbar gemacht werden können.

>[!AVAILABILITY]
>
>Interessenten-Profile sind automatisch darauf beschränkt, nur ID-Namespaces des Partner-ID-Typs zu verwenden. Dies erfolgt in der Konzeption und gewährleistet eine saubere Trennung zwischen Erstanbieter- und Interessenten-Profilen.

![Wählen Sie die zuvor konfigurierte Partner-ID als primäre Identität im Schema aus.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Beachten Sie, dass das Schema noch nicht für das Profil aktiviert ist. Schalten Sie die Schaltfläche Profil um, um dieses Schema für die Aufnahme in den Profildienst zu aktivieren. Weitere Informationen zum Aktivieren des Schemas für die Verwendung im Echtzeit-Kundenprofil finden Sie in der [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Aktivieren eines Schemas für ein Profil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Fügen Sie allen Feldern im Schema die Beschriftung Data Governance von Drittanbietern hinzu.

Erwägen Sie das Hinzufügen von Data Governance-Beschriftungen von Drittanbietern zu allen Feldern, aus denen das Schema besteht. Dies ist wichtig, um eine verantwortungsvolle Nutzung von Drittanbieterdaten zu gewährleisten und das Risiko der Datenlecks zu minimieren. Weitere Informationen zu Data Governance-Beschriftungen von Drittanbietern finden (Link zu Dokumenten von Jordanien hinzufügen)

Gehen Sie dazu wie folgt vor:

1. Navigieren Sie zum erstellten Schema und wählen Sie die **[!UICONTROL Bezeichnungen]** Registerkarte.
2. Wählen Sie alle Felder in diesem Schema mithilfe des Kontrollkästchens oben aus und klicken Sie dann auf das Stiftsymbol rechts, um Data Governance-Beschriftungen auf dieses Schema anzuwenden.
3. Wählen Sie die **[!UICONTROL Partnerökosystem]** Titel aus den Kategorien links.
4. Wählen Sie die Bezeichnung **[!UICONTROL Dritte]** und wählen **[!UICONTROL Speichern]**.
5. Beachten Sie, dass jetzt alle Felder im Schema die im vorherigen Schritt ausgewählte Bezeichnung tragen.

>[!SUCCESS]
>
>Ihr Schema kann jetzt verwendet werden und Sie können mit dem nächsten Schritt fortfahren, um potenzielle Daten von Ihrem Datenpartner zu erfassen.

Überlegen Sie in diesem Schritt außerdem, wie sich Ihr Data-Governance-Modell ändert, wenn Sie Ihre Daten-Management-Strategie erweitern und vom Partner bereitgestellte Drittanbieterdaten einschließen. Machen Sie sich mit den Hinweisen in den folgenden Links zur Dokumentation vertraut:

* (**In Kürze verfügbar**) Halten Sie Drittanbieterdaten in einem separaten Datensatz, damit Integrationen auf einfache Weise gelöscht und rückgängig gemacht werden können.
* (**In Kürze verfügbar**) Verwenden Sie die Funktion [Datensatzgültigkeit](/help/hygiene/ui/dataset-expiration.md) für den Datensatz bei Kundinnen und Kunden, die das Datenhygiene-Add-on erworben haben.
* (**In Kürze verfügbar**) Gehen Sie beim Erstellen abgeleiteter Datensätze, die Daten von Drittanbietern abrufen, vorsichtig vor. Denn einmal vermischt, besteht die einzige Lösung zum Entfernen der Daten von Drittanbietern darin, den gesamten abgeleiteten Datensatz zu löschen.

### Liste der potenziellen Profile laden und die Profilansicht des Interessenten überprüfen

Nachdem Sie Ihr Datenmodell für die Verwaltung von Interessenten-Profilen vorbereitet haben, ist es Zeit, Daten zu erfassen.

#### Erstellen eines Datensatzes und Laden von Beispielprojektdaten

Um einige Beispieldaten zu laden und Interessenten-Profile zu füllen, erstellen Sie einen Datensatz und laden Sie eine Datei hoch, die Sie vom Datenpartner erhalten haben. Führen Sie die folgenden Schritte aus:

1. Navigieren Sie zu **[!UICONTROL Data Management]** > **[!UICONTROL Datensätze]** und wählen **[!UICONTROL Datensatz erstellen]**.
2. Wählen Sie Datensatz aus Schema erstellen aus
3. Wählen Sie das Schema aus, das Sie im vorherigen Schritt erstellt haben
4. Geben Sie Ihrem Datensatz einen Namen und optional eine Beschreibung.
5. Wählen Sie **[!UICONTROL Beenden]** aus.

![Eine Aufzeichnung der Schritte zum Erstellen eines Datensatzes für Interessenten-Profile.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Beachten Sie, dass Sie ähnlich wie beim Schritt zum Erstellen eines Schemas die Aufnahme des Datensatzes in das Echtzeit-Kundenprofil aktivieren müssen. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie in der [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Datensatz für Profil aktivieren.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Um eine vom Partner erhaltene Datei in den Datensatz zu laden, wählen Sie den Datensatz aus, scrollen Sie in der rechten Leiste nach unten und wählen Sie **[!UICONTROL Daten hinzufügen]**. Sie können die Datei per Drag-and-Drop verschieben oder **[!UICONTROL Dateien auswählen]** , um zum Dateispeicherort zu navigieren und ihn auszuwählen.

![Datei zum Datensatz hinzufügen.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Nachdem Sie die Profilliste vom Datenpartner in Real-Time CDP geladen haben, fahren Sie mit dem [Inspect des Bereichs der geladenen Profile](#inspect-profiles) , um zu überprüfen, ob die potenziellen Profile in der Benutzeroberfläche ausgefüllt werden.

#### Interessensdaten über Quell-Connectoren erfassen

Sie können wiederkehrende Dateiimporte einrichten, um Daten vom Partner über einen Quell-Connector zu erfassen und die Liste der potenziellen Profile in Real-Time CDP zu importieren.

Nachfolgend finden Sie einige empfohlene Quell-Connectoren zu diesem Zweck. Beachten Sie jedoch, dass jede dateibasierte Erfassungsmethode in Real-Time CDP zu Ihrem Zweck funktioniert.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Nachdem Sie die Profilliste vom Datenpartner in Real-Time CDP geladen haben, fahren Sie mit dem nächsten Abschnitt fort, um zu überprüfen, ob die potenziellen Profile in der Benutzeroberfläche ausgefüllt werden.

#### Inspect der geladenen Profile {#inspect-profiles}

Um die Liste der potenziellen Profile anzuzeigen, navigieren Sie zu **[!UICONTROL Perspektiven]** > **[!UICONTROL Profile]** in der linken Leiste.

Beachten Sie, dass es bis zu zwei Stunden dauern kann, bis die Profile, die Sie gerade in Real-Time CDP geladen haben, im **[!UICONTROL Durchsuchen]** Ansicht des Profilbildschirms. Wenn auf der Seite die Meldung &quot;Es gibt derzeit keine potenziellen Profile zum Durchsuchen&quot; angezeigt wird, versuchen Sie es nach einiger Zeit erneut. Nach einiger Wartezeit sollten Interessenten-Profile in der **[!UICONTROL Durchsuchen]** anzeigen.

>[!TIP]
>
>Beachten Sie, dass die **[!UICONTROL Identity Namespace]** Spalte. Wenn Sie mit mehreren Datenanbietern arbeiten, verwenden Sie diese Spalte, um die Herkunft von potenziellen Profilen zu ermitteln.

![Anzeigen der potenziellen Profile, die in Real-Time CDP geladen wurden](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Sie können auch ein beliebiges Profil für eine weitere Überprüfung auswählen, wie unten dargestellt.

![Überprüfen von potenziellen Profilen](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**In Kürze verfügbar**) Weitere Informationen zu potenziellen Profilen.

### Erstellen potenzieller Zielgruppen {#create-prospect-audiences}

Verwenden Sie die Segmentierungsfunktion in Real-Time CDP, um Zielgruppen aus Ihren potenziellen Profilen zu erstellen. Verwenden Sie die gewünschten Segmentierungsregeln, um maßgeschneiderte Zielgruppen zu erstellen.

Um zu beginnen und Audiences aus Interessenten-Profilen zu erstellen, navigieren Sie zu **[!UICONTROL Perspektiven]** > **[!UICONTROL Zielgruppen]**.

![Ansicht potenzieller Zielgruppen](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Beachten Sie, dass sich das Erlebnis beim Erstellen von Zielgruppen für potenzielle Profile vom Erlebnis zum Erstellen von Zielgruppen unterscheidet, das von Ihren bekannten Erstanbieterkunden genutzt wird. Diese Ansicht beschränkt sich auf:

* Attribute aus der Prospektklasse, die Sie zuvor erstellt haben
* Nur Batch-Profilauswertung.
* Das Erstellen von Zielgruppen basierend auf Zeitreihenereignissen wird nicht unterstützt.

(**In Kürze verfügbar**) Erfahren Sie mehr über potenzielle Zielgruppen.

### Profile für Interessenten für Ziele aktivieren {#activate-to-destinations}

Nutzen Sie die potenziellen Zielgruppen, indem Sie sie an Ziele exportieren. Derzeit werden nur bestimmte Ziele, wie [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) oder [!BADGE Alpha]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp-onboarding.md) Zielunterstützung Aktivierung von Interessenten-Profilen.

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [!BADGE Beta]{type=Informative}[Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* (**In Kürze verfügbar**) [!BADGE Beta]{type=Informative}**Partnergestützte Erkennung** für die Personalisierung von Onsite-Erlebnissen während des Besuchs und für das Offsite-Retargeting nach dem Besuch, ohne dass sich die Benutzerin oder der Benutzer authentifiziert oder bereits Erfahrung mit Ihrer Marke hat.
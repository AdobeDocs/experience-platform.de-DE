---
title: Engagieren und Akquirieren neuer Kundinnen und Kunden durch Anwendungsfälle für die Kundengewinnung
description: Erfahren Sie, wie Sie neue Kundinnen und Kunden durch Anwendungsfälle für die Prospektion, ermöglicht durch die Unterstützung von Partnerdaten in Real-Time CDP, ansprechen und gewinnen können.
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: da7a53c1e4accdacfa55e4022c1b499f70aab8fa
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 93%

---

# Engagieren und Akquirieren neuer Kundinnen und Kunden durch Anwendungsfälle für die Kundengewinnung

>[!AVAILABILITY]
>
>* Diese Funktion steht Kunden zur Verfügung, die Real-Time CDP (App Service), Adobe Experience Platform Activation, Echtzeit-Kundendatenplattform, Real-Time CDP Prime und Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie in den [Produktbeschreibungen](https://helpx.adobe.com/de/legal/product-descriptions.html) und erhalten Sie von Ihrem Adobe-Support-Team.

Nutzen Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, um Ihre Profilbasis mit potenziellen Profilen von Datenpartnern zu erweitern und mit ihnen zu interagieren, um neue Kundinnen und Kunden anzusprechen und zu gewinnen.

![Anwendungsfall „Kundenprospektion“ – visuelle allgemeine Übersicht.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie erwägen, mithilfe der Unterstützung von Partnerdaten in Real-Time CDP neue Kundinnen und Kunden anzusprechen und zu gewinnen, sollten Sie die folgenden Voraussetzungen in Ihrem Planungsprozess berücksichtigen:

* Wie häufig werden von Partnern bereitgestellte Profile voraussichtlich wieder in Real-Time CDP aufgenommen und aktualisiert?
* Welche Identitäten benötigen Ihre nachgelagerten Ziele?
* Stellen Sie sicher, dass die aufgenommenen Kennungen nachgelagert verarbeitet werden können
* Sind die Partnerdaten, die Sie erfassen, an eine allgemein akzeptierte dauerhafte Kennung wie personenbezogene Informationen (PII), gehashte PII oder eine Partnerkennung gebunden?
* Welche Datennutzungsrichtlinien müssen Sie aus der Partnerperspektive und aus Ihrem eigenen Rechts-, Datenschutz- oder Compliance-Team kennen?

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

Bevor Sie Real-Time CDP erweitern, um neue Kundinnen und Kunden anzusprechen und zu gewinnen, stellen Sie sicher, dass Sie Real-Time CDP verwenden, um eine robuste Grundlage für Ihre Erstanbieterdaten zu schaffen. Die Workflows zur Erreichung dieses Anwendungsfalls ähneln Workflows, mit denen Sie mit Ihren bekannten Kundinnen und Kunden interagieren.

![Anwendungsfall „Kundenprospektion“ – visuelle allgemeine Übersicht.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Als **Kundin bzw. Kunde** können Sie Interessentenprofile von einem oder mehreren **Datenpartnern** lizenzieren, um die Trichter-Kundenakquise zu optimieren.
2. Als **Kundin bzw. Kunde** erweitern Sie Ihre Profildaten und Ihr Governance-Modell, um die von **Partnern** bereitgestellte Liste von Interessentenprofilen aufzunehmen.
3. Als **Kundin bzw. Kunde** laden Sie Interessentenprofile in Real-Time CDP und erstellen Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Als **Kundin bzw. Kunde** erstellen Sie fokussierte Zielgruppen aus der Liste der Interessentenprofile.
5. Als **Kundin bzw. Kunde** aktivieren Sie potenzielle Zielgruppen für Ziele, die die in Ihrer Interessentenliste verfügbaren Identitäten akzeptieren.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** bei der Last-Mile-Aktivierung von Zielgruppen bei gewünschten zahlungspflichtigen Medienzielen zusammen.

## Videoeinführung {#video-walkthrough}

Sehen Sie sich das Video-Tutorial unten an, um eine exemplarische Vorgehensweise zum Erreichen und Ansprechen potenzieller Zielgruppen zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte, die Links zu weiterführender Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Funktionen und Elemente der Benutzeroberfläche, die Sie verwenden werden {#ui-functionality-and-elements}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, werden Sie die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente nutzen (aufgelistet in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihre Systemadmins, Ihnen die erforderlichen Berechtigungen zu erteilen.

* [Identitäten](/help/identity-service/namespaces.md)
* [Schemata](/help/xdm/home.md)
* [Datennutzungskennzeichnungen](/help/data-governance/labels/overview.md)
* [Datensätze](/help/catalog/datasets/overview.md)
* [Quellen](/help/sources/home.md)
* [Interessentenprofile](/help/profile/ui/prospect-profile.md)
* [Potenzielle Zielgruppen](/help/segmentation/ui/prospect-audience.md)
* [Ziele](/help/destinations/home.md)

### Lizenzieren der Details von Drittanbieterprofilen vom Partner {#license-profiles-from-partner}

Dieser Schritt wird im Abschnitt [Voraussetzungen](#prerequisites-and-planning) beschrieben. Adobe geht dabei davon aus, dass Sie über die richtigen vertraglichen Vereinbarungen mit vertrauenswürdigen Datenanbietern verfügen, um vom Datenpartner bereitgestellte Interessentenprofile aufzunehmen.

### Erweitern der Profildaten und des Governance-Modells für von Partnern bereitgestellte Interessentenprofile {#extend-governance-model}

Zur Vorbereitung darauf, Interessentenprofile von Ihrem Datenpartner zu erhalten, müssen Sie Ihr Daten-Management-Framework in Real-Time CDP erweitern, um diesen neuen Profiltyp zu berücksichtigen.

Die Identitäts-, Daten- und Governance-Komponenten, die Sie verwenden werden, sind:

* der neue Identitätstyp **[!UICONTROL Partner-ID]** für die von Partnern bereitgestellten Profile
* die neue XDM-Klasse **[!UICONTROL XDM Individual Prospect Profile]**
* **(Dokumentation in Kürze verfügbar)** Feldergruppen, die auf die Partnerdatenunterstützung zugeschnitten sind
* **(Dokumentation in Kürze verfügbar)** Drittanbieterkennzeichnungen, die Sie zu den Attributen hinzufügen, die von Partnern eingehen

#### Erstellen eines Identity-Namespace für die Partner-ID {#create-partner-id-namespace}

Erstellen Sie zunächst einen neuen Identitätstyp für die Profile, die Sie vom Partner erhalten. Dazu müssen Sie im Abschnitt „Identität“ einen neuen Identity-Namespace des Typs **[!UICONTROL Partner-ID]** erstellen.

![Erstellen Sie einen neuen Identity-Namespace für die Partner-ID.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Weitere Informationen zur Partner-ID finden Sie im Abschnitt [Identitätstypen](/help/identity-service/namespaces.md).
* Lesen Sie die Anweisungen zum [Definieren von Identitätsfeldern](/help/xdm/ui/fields/identity.md) in der Experience Platform-Benutzeroberfläche.

#### Erstellen eines neues Schemas mit der Klasse **[!UICONTROL XDM Individual Prospect Profile]**

Erstellen Sie als Nächstes in **[!UICONTROL Daten-Management]** > **[!UICONTROL Schemata]** ein neues Schema und weisen Sie ihm die Klasse **[!UICONTROL XDM Individual Prospect Profile]** zu.

![Suchen Sie im XDM-Schema-Builder nach der Klasse „XDM Individual Prospect Profile“.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Lesen Sie, wie Sie [Schemata in der Benutzeroberfläche erstellen und bearbeiten](/help/xdm/ui/resources/schemas.md), und erhalten Sie vollständige Informationen zur Klasse „XDM Individual Prospect Profile“ (Link folgt in Kürze).

Die Klasse **[!UICONTROL XDM Individual Prospect Profile]** ist mit den unten aufgeführten Feldern vorkonfiguriert. Um Ihr Schema mit von Partnern bereitgestellten Attributen für die Interessentenprofile anzureichern, können Sie entweder eine neue Feldergruppe mit den erwarteten Attributen erstellen und zum Schema hinzufügen oder eine der von Adobe bereitgestellten vorkonfigurierten Feldergruppen verwenden.

![Vorkonfigurierte Felder für die Klasse „XDM Individual Prospect Profile“.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Als Nächstes müssen Sie die zuvor erstellte Partner-ID-Identität als primäre Identität für das Schema auswählen. Profildatensätze müssen eine primäre Kennung aufweisen. Dieser Schritt ist erforderlich, um sicherzustellen, dass Interessentendaten in den Profilspeicher geladen und für die Segmentierung und Aktivierung verfügbar gemacht werden können.

>[!AVAILABILITY]
>
>Interessentenprofile sind automatisch darauf beschränkt, nur ID-Namespaces des Typs „Partner-ID“ zu verwenden. Dies ist beabsichtigt und gewährleistet eine saubere Trennung zwischen Erstanbieter- und Interessentenprofilen.

![Wählen Sie die zuvor konfigurierte Partner-ID als primäre Identität im Schema aus.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Beachten Sie, dass das Schema noch nicht für das Profil aktiviert ist. Schalten Sie die Schaltfläche „Profil“ um, um dieses Schema für das Einschließen in den Profildienst zu aktivieren. Weitere Informationen zum Aktivieren des Schemas für die Verwendung im Echtzeit-Kundenprofil finden Sie im [Tutorial zum Erstellen von Schemata](/help/xdm/tutorials/create-schema-ui.md#profile).

![Aktivieren eines Schemas für ein Profil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Hinzufügen der Data Governance-Beschriftung „Drittanbieter“ zu allen Feldern im Schema

Erwägen Sie das Hinzufügen der Data Governance-Beschriftung „Drittanbieter“ zu allen Feldern, aus denen das Schema besteht. Dies ist wichtig, um eine verantwortungsvolle Nutzung von Drittanbieterdaten zu gewährleisten und das Risiko von Datenlecks zu minimieren. Weitere Informationen finden Sie [Data Governance-Beschriftungen von Drittanbietern](../../data-governance/labels/reference.md#partner-ecosystem-labels).

Gehen Sie dazu wie folgt vor:

1. Navigieren Sie zum erstellten Schema und wählen Sie die Registerkarte **[!UICONTROL Kennzeichnungen]** aus.
2. Wählen Sie alle Felder in diesem Schema mithilfe des Kontrollkästchens oben aus und klicken Sie dann auf das Stiftsymbol rechts, um Data Governance-Kennzeichnungen auf dieses Schema anzuwenden.
3. Wählen Sie die Kennzeichnung **[!UICONTROL Partner-Ökosystem]** aus den Kategorien auf der linken Seite aus.
4. Wählen Sie die Kennzeichnung **[!UICONTROL Drittanbieter]** aus und klicken Sie auf **[!UICONTROL Speichern]**.
5. Beachten Sie, dass jetzt alle Felder im Schema die im vorherigen Schritt ausgewählte Kennzeichnung tragen.

>[!SUCCESS]
>
>Ihr Schema kann jetzt verwendet werden, und Sie können mit dem nächsten Schritt fortfahren, um Interessentendaten von Ihrem Datenpartner aufzunehmen.

Überlegen Sie in diesem Schritt außerdem, wie sich Ihr Data-Governance-Modell ändert, wenn Sie Ihre Daten-Management-Strategie erweitern und vom Partner bereitgestellte Drittanbieterdaten einschließen. Machen Sie sich mit den Hinweisen in den folgenden Links zur Dokumentation vertraut:

* (**In Kürze verfügbar**) Halten Sie Drittanbieterdaten in einem separaten Datensatz, damit Integrationen auf einfache Weise gelöscht und rückgängig gemacht werden können.
* (**In Kürze verfügbar**) Verwenden Sie die Funktion [Datensatzgültigkeit](/help/hygiene/ui/dataset-expiration.md) für den Datensatz bei Kundinnen und Kunden, die das Datenhygiene-Add-on erworben haben.
* (**In Kürze verfügbar**) Gehen Sie beim Erstellen abgeleiteter Datensätze, die Daten von Drittanbietern abrufen, vorsichtig vor. Denn einmal vermischt, besteht die einzige Lösung zum Entfernen der Daten von Drittanbietern darin, den gesamten abgeleiteten Datensatz zu löschen.

### Laden der Liste der Interessentenprofile und Anzeigen der Ansicht der Interessentenprofile

Nachdem Sie Ihr Datenmodell für die Verwaltung von Interessentenprofilen vorbereitet haben, ist es Zeit, Daten zu aufzunehmen.

#### Erstellen eines Datensatzes und Laden von Beispiel-Interessentendaten

Um einige Beispieldaten zu laden und Interessentenprofile zu füllen, erstellen Sie einen Datensatz und laden Sie eine Datei hoch, die Sie vom Datenpartner erhalten haben. Führen Sie folgende Schritte durch:

1. Navigieren Sie zu **[!UICONTROL Daten-Management]** > **[!UICONTROL Datensätze]** und wählen Sie **[!UICONTROL Datensatz erstellen]** aus.
2. Wählen Sie „Datensatz aus Schema erstellen“ aus
3. Wählen Sie das Schema aus, das Sie im vorherigen Schritt erstellt haben
4. Geben Sie Ihrem Datensatz einen Namen und optional eine Beschreibung.
5. Wählen Sie **[!UICONTROL Beenden]** aus.

![Eine Aufzeichnung der Schritte zum Erstellen eines Datensatzes für Interessentenprofile.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Beachten Sie, dass Sie ähnlich wie beim Schritt zum Erstellen eines Schemas den Datensatz aktivieren müssen, der in das Echtzeit-Kundenprofil einbezogen werden soll. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie im [Tutorial zum Erstellen von Schemata](/help/xdm/tutorials/create-schema-ui.md#profile).

![Datensatz für Profil aktivieren.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Um eine vom Partner erhaltene Datei in den Datensatz zu laden, wählen Sie den Datensatz aus, scrollen Sie in der rechten Leiste nach unten und wählen Sie **[!UICONTROL Daten hinzufügen]** aus. Sie können die Datei per Drag-and-Drop verschieben oder **[!UICONTROL Dateien auswählen]** verwenden, um zum Dateispeicherort zu navigieren und ihn auszuwählen.

![Datei zum Datensatz hinzufügen.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Nachdem Sie die Liste der Profile vom Datenpartner in die Real-Time-CDP geladen haben, fahren Sie mit dem Abschnitt [Inspizieren der geladenen Interessentenprofile](#inspect-profiles) fort, um zu überprüfen, ob die Interessentenprofile in der Benutzeroberfläche ausgefüllt werden.

#### Aufnehmen von Interessentendaten über Quell-Connectoren

Sie können wiederkehrende Dateiimporte einrichten, um Daten vom Partner über einen Quell-Connector zu erfassen und die Liste der Interessentenprofile in die Real-Time CDP zu importieren.

Nachfolgend finden Sie einige empfohlene Quell-Connectoren für diesen Zweck. Beachten Sie jedoch, dass jede dateibasierte Aufnahmemethode in die Real-Time CDP für Ihre Zwecke funktioniert.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Nachdem Sie die Liste von Profilen vom Datenpartner in die Real-Time CDP geladen haben, fahren Sie mit dem nächsten Abschnitt fort, um zu überprüfen, ob die Interessentenprofile in der Benutzeroberfläche ausgefüllt werden.

#### Inspizieren der geladenen Interessentenprofile {#inspect-profiles}

Um die Liste der Interessentenprofile anzuzeigen, navigieren Sie in der linken Leiste zu **[!UICONTROL Interessenten]** > **[!UICONTROL Profile]**.

Beachten Sie, dass es bis zu zwei Stunden dauern kann, bis die Interessentenprofile, die Sie gerade in die Real-Time CDP geladen haben, in der Ansicht **[!UICONTROL Durchsuchen]** des Interessentenprofil-Bildschirms erscheinen. Wenn auf der Seite die Meldung „Es sind derzeit keine Interessentenprofile zum Durchsuchen vorhanden“ angezeigt wird, versuchen Sie es nach einiger Zeit erneut. Nach einiger Wartezeit sollten Interessentenprofile in der Ansicht **[!UICONTROL Durchsuchen]** erscheinen.

>[!TIP]
>
>Beachten Sie, dass die Spalte **[!UICONTROL Identity-Namespace]** vorhanden ist. Wenn Sie mit mehreren Datenanbietern arbeiten, verwenden Sie diese Spalte, um die Herkunft von Interessentenprofilen zu ermitteln.

![Anzeigen der Interessentenprofile, die in die Real-Time CDP geladen wurden.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Sie können auch ein Interessentenprofil für eine weitere Inspektion auswählen, wie unten dargestellt.

![Ansicht, wie Interessentenprofile inspiziert werden können.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Mehr dazu [Interessenten-Profile](/help/profile/ui/prospect-profile.md).

### Erstellen von Interessentenzielgruppen {#create-prospect-audiences}

Verwenden Sie die Segmentierungsfunktion in der Real-Time CDP, um Zielgruppen aus Ihren Interessentenprofilen zu erstellen. Verwenden Sie die gewünschten Segmentierungsregeln, um maßgeschneiderte Zielgruppen zu erstellen.

Um zu beginnen und Zielgruppen aus Interessentenprofilen zu erstellen, navigieren Sie zu **[!UICONTROL Interessierte]** > **[!UICONTROL Zielgruppen]**.

![Ansicht von Interessentenzielgruppen.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Beachten Sie, dass sich das Erlebnis des Erstellens von Zielgruppen für Interessentenzielgruppen vom Erlebnis des Erstellens von Zielgruppen aus Ihren bekannten Erstanbieterkundinnen und -kunden unterscheidet. Diese Ansicht beschränkt sich auf:

* Attribute aus der Klasse „Interessierte“, die Sie zuvor erstellt haben.
* Nur Batch-Profilauswertung.
* Das Erstellen von Zielgruppen basierend auf Zeitreihenereignissen wird nicht unterstützt.

Mehr dazu [Interessenten-Zielgruppen](/help/segmentation/ui/prospect-audience.md).

### Aktivieren von Interessentenprofilen für Ziele {#activate-to-destinations}

Nutzen Sie die Interessentenzielgruppen, indem Sie sie zu Zielen exportieren. Derzeit unterstützen nur bestimmte Cloud-Speicher-Ziele die Aktivierung von potenziellen Profilen.

![Ziele, die potenzielle Zielgruppen unterstützen.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[Mehr dazu](/help/destinations/ui/activate-prospect-audiences.md) über die Aktivierung von Perspektiven für Cloud-Speicher-Ziele.

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [Nutzen Sie die von Partnern unterstützte Erkennung für die Personalisierung von On-site-Erlebnissen](/help/rtcdp/partner-data/onsite-personalization.md) während des Besuchs, ohne dass sich der Benutzer authentifiziert oder über einen früheren Verlauf mit Ihrer Marke verfügt.
* [Erweiterte Aktivierung von Interessenten- und Interessenten-Zielgruppen](/help/destinations/ui/activate-prospect-audiences.md) , um Ziele auszuwählen.

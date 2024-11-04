---
title: Kontozielgruppen
description: Erfahren Sie, wie Sie Zielgruppen für Konten erstellen und verwenden, um Kontoprofile in nachgelagerten Zielen auszuwählen.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: fd0a495d68d6a09ccca66c400993d2e72673321c
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 22%

---

# Konto-Zielgruppen

>[!AVAILABILITY]
>
>Kontozielgruppen sind nur in der [B2B edition von Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) und der [B2P Edition von Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p) verfügbar.

Mit der Kontosegmentierung können Sie mit Adobe Experience Platform die gesamte Einfachheit und Komplexität der Marketing-Segmentierungserfahrung von benutzerbezogenen Zielgruppen zu kontobasierten Zielgruppen bringen.

Kontozielgruppen können als Eingabe für kontobasierte Ziele verwendet werden, sodass Sie die Personen innerhalb dieser Konten in nachgelagerten Diensten ansprechen können. Sie können beispielsweise kontobasierte Zielgruppen verwenden, um Datensätze aller Konten abzurufen, die **nicht** über Kontaktinformationen für Personen mit dem Titel Chief Operating Officer (COO) oder Chief Marketing Officer (CMO) verfügen.

## Terminologie {#terminology}

Bevor Sie mit Kontozielgruppen beginnen, sollten Sie sich die Unterschiede zwischen den verschiedenen Zielgruppentypen ansehen:

- **Konto-Zielgruppen**: Eine Konto-Zielgruppe ist eine Zielgruppe, die mit den Profildaten **Konto** erstellt wird. Kontoprofildaten können verwendet werden, um Zielgruppen zu erstellen, die Personen in nachgelagerten Konten ansprechen. Weiterführende Informationen zu Kontoprofilen finden Sie in der [Kontoprofilübersicht](../../rtcdp/accounts/account-profile-overview.md).
- **Zielgruppen für Personen**: Eine Zielgruppe für Personen ist eine Zielgruppe, die mithilfe von Profildaten vom Typ **Kunde** erstellt wird. Kundenprofildaten können verwendet werden, um Zielgruppen zu erstellen, die auf die Kundengruppe Ihres Unternehmens ausgerichtet sind. Weiterführende Informationen zu Kundenprofilen finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md) .
- **Interessante Zielgruppen**: Eine potenzielle Zielgruppe ist eine Zielgruppe, die mithilfe von Profildaten vom Typ **Interessent** erstellt wird. Mit potenziellen Profildaten können Sie Zielgruppen von nicht authentifizierten Benutzern erstellen. Weiterführende Informationen zu potenziellen Profilen finden Sie in der [Profilübersicht für Interessenten](../../profile/ui/prospect-profile.md).

## Zugriff {#access}

Um auf Kontozielgruppen zuzugreifen, wählen Sie **[!UICONTROL Zielgruppen]** im Abschnitt **[!UICONTROL Konten]** aus.

![Die Schaltfläche &quot;Zielgruppen&quot;wird im Abschnitt &quot;Konten&quot;hervorgehoben.](../images/ui/account-audiences/select.png)

Die Seite [!UICONTROL Durchsuchen] wird angezeigt und enthält eine Liste aller Zielgruppen des Kontos für die Organisation.

![Die Zielgruppen des Kontos, die zur Organisation gehören, werden angezeigt.](../images/ui/account-audiences/browse.png)

Diese Ansicht listet Informationen zur Zielgruppe auf, einschließlich Name, Profilanzahl, Ursprung, Lebenszyklusstatus, Erstellungsdatum und Datum der letzten Aktualisierung.

Sie können auch die Such- und Filterfunktion verwenden, um schnell nach bestimmten Kontozielgruppen zu suchen und diese zu sortieren. Weitere Informationen zu dieser Funktion finden Sie in der [Audience Portal-Übersicht](./audience-portal.md#manage-audiences) .

## Zielgruppe erstellen {#create}

>[!NOTE]
>
>Kontozielgruppen werden mit der **Batch**-Segmentierung ausgewertet und alle 24 Stunden ausgewertet.

Um eine Konto-Audience zu erstellen, wählen Sie auf der Seite [!UICONTROL Durchsuchen] die Option **[!UICONTROL Audience erstellen]** aus.

![Die Schaltfläche [!UICONTROL Audience erstellen] wird auf der Seite zum Durchsuchen der Zielgruppe des Kontos hervorgehoben.](../images/ui/account-audiences/select-create-audience.png)

Der Segment Builder wird angezeigt. Die Kontoattribute und Zielgruppen werden in der linken Navigationsleiste angezeigt. Auf der Registerkarte [!UICONTROL Attribute] können Sie sowohl von Platform erstellte als auch benutzerdefinierte Attribute hinzufügen.

![Der Segment Builder wird angezeigt. Beachten Sie, dass nur die Attribute und Zielgruppen angezeigt werden.](../images/ui/account-audiences/segment-builder.png)

Beachten Sie bei der Erstellung von Kontozielgruppen, dass Ereignisse unter **[!UICONTROL Personen]** aufgelistet werden, anstatt ihre eigene Registerkarte zu sein, da diese Attribute mit Personen verknüpft sind.

![Der Speicherort für Ereignisse, der sich im Ordner [!UICONTROL Personen] befindet, wird hervorgehoben.](../images/ui/account-audiences/attributes.png)

Auf der Registerkarte [!UICONTROL Zielgruppen] können Sie zuvor erstellte personenbasierte Zielgruppen hinzufügen, die bei der Erstellung Ihrer eigenen Kontozielgruppe erstellt werden sollen.

![Die Registerkarte &quot;Zielgruppen&quot;im Segment Builder wird hervorgehoben.](../images/ui/account-audiences/audiences.png)

Weitere Informationen zur Verwendung von Segment Builder finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](./segment-builder.md).

### Beziehungen herstellen {#relationships}

Standardmäßig zeigt die Benutzeroberfläche von Segment Builder für Kontozielgruppen die direkte Beziehung zwischen einem Konto und einer Person an. Für Kontozielgruppen stehen jedoch andere Beziehungstypen zur Verfügung.

Um die alternativen Beziehungstypen zu verwenden, wählen Sie ![das Einstellungssymbol](../../images/icons/settings.png) aus.

![Das Einstellungssymbol wird im Abschnitt &quot;Felder&quot;hervorgehoben.](../images/ui/account-audiences/select-settings.png)

Wählen Sie auf der Registerkarte [!UICONTROL Einstellungen] die Option **[!UICONTROL Beziehungsselektoren anzeigen]** im Abschnitt **[!UICONTROL Beziehung der Felder]** aus.

![Der Umschalter Verknüpfungsauswahl anzeigen ist im Bereich Beziehung der Felder auf der Registerkarte Einstellungen ausgewählt.](../images/ui/account-audiences/show-relation-selectors.png)

Wählen Sie erneut ![das Einstellungssymbol](../../images/icons/settings.png) aus, um zur Registerkarte [!UICONTROL Felder] zurückzukehren. Sie können jetzt den Abschnitt **[!UICONTROL Beziehungen herstellen]** sehen, in dem Sie feststellen können, wie das Konto mit der Person verbunden ist und wie die Person mit der Gelegenheit verbunden ist.

![Der Abschnitt Beziehungen herstellen wird hervorgehoben und zeigt die Optionen zum Herstellen einer Verbindung zwischen einem Konto und einer Person und zum Herstellen einer Verbindung zu einer Gelegenheit an.](../images/ui/account-audiences/establish-relationships.png)

Beim Verbinden des Kontos mit der Person können Sie aus den folgenden Optionen wählen:

| Option | Beschreibung |
| ------ | ----------- |
| Direkte Beziehung | Die direkte Verbindung zwischen dem Konto und der Person Dies gibt an, mit welchen Konten jede Person über das Array von `accountID` -Werten im Array `personComponents` des Personenschemas verknüpft ist. Dieser Pfad wird am häufigsten verwendet. |
| Kundenbeziehung | Die Beziehung zwischen dem Konto und der Person, die durch das Objekt `accountPersonRelation` definiert wird. Dieser Pfad ermöglicht es auch, jede Person mit mehreren Konten zu verbinden. Sie wird verwendet, wenn Ihr Unternehmen aus Ihren Quelldaten eine explizite Beziehungstabelle definiert hat. |
| Chancen-/Personenbeziehung | Die Beziehung zwischen der Gelegenheit und der Person, die durch das `opportunityPersonRelation` -Objekt definiert wird. Dadurch wird die Person mit einem Konto verbunden, indem sie von der Opportunity zur Opportunity zum Konto wechselt. Auf diese Weise können Sie beschreiben, bei welchen Unternehmen die Person mit Chancen verbunden ist. |

Wenn Sie die Gelegenheit mit der Person verbinden, können Sie aus den folgenden Optionen wählen:

| Option | Beschreibung |
| ------ | ----------- |
| Konto | Die direkte Verbindung zwischen dem Konto und der Gelegenheit. Wenn Sie dies in einer Konto-Zielgruppe verwenden, verbindet dieser Pfad alle Personen im Unternehmen mit der Möglichkeit. |
| Chancen-/Personenbeziehung | Die Beziehung zwischen der Chance und der Person, die auf dem Opportunity-Person-Objekt basiert. Dieser Weg verbindet nur Personen, die als an einer Gelegenheit beteiligt identifiziert wurden. |

Nachdem Sie die gewünschte Beziehung hergestellt haben, können Sie die erforderlichen Personen-Zielgruppen zu Ihrer Segmentdefinition hinzufügen.

## Zielgruppe aktivieren {#activate}

>[!NOTE]
>
>Nur eine begrenzte Anzahl von Zielen unterstützt Kontozielgruppen. Stellen Sie sicher, dass das Ziel, das Sie aktivieren möchten, um Kontozielgruppen zu unterstützen, bevor Sie diesen Prozess fortsetzen.

Nachdem Sie Ihre Zielgruppe erstellt haben, können Sie die Zielgruppe für andere nachgelagerte Dienste aktivieren.

Wählen Sie die Zielgruppe aus, die Sie aktivieren möchten, gefolgt von **[!UICONTROL Für Ziel aktivieren]**.

![Die Schaltfläche [!UICONTROL In Ziel aktivieren] ist im Schnellaktionsmenü für die ausgewählte Zielgruppe hervorgehoben.](../images/ui/account-audiences/activate.png)

Die Seite [!UICONTROL Ziel aktivieren] wird angezeigt. Weitere Informationen zum Aktivierungsprozess, einschließlich unterstützter Ziele und Details zu Feldzuordnungen, finden Sie im Tutorial [Kontozielgruppen aktivieren](/help/destinations/ui/activate-account-audiences.md) .

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Handbuchs erhalten Sie jetzt ein besseres Verständnis dafür, wie Sie Ihre Kontozielgruppen in Adobe Experience Platform erstellen und verwenden. Informationen zur Verwendung anderer Zielgruppentypen in Platform finden Sie im [UI-Handbuch für den Segmentation Service](./overview.md).

## Anhang {#appendix}

Im folgenden Abschnitt finden Sie weitere Informationen zu Kontozielgruppen.

### Validierung der Kontosegmentierung {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Fehler beim maximalen Lookback-Fenster"
>abstract="Das maximale Lookback-Fenster für Erlebnisereignisse beträgt 30 Tage."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Fehler bei der Tiefe des maximalen verschachtelten Containers"
>abstract="Die maximale Tiefe verschachtelter Container beträgt **5**. Das bedeutet, dass Sie beim Erstellen Ihrer Zielgruppe **nicht** mehr als fünf verschachtelte Container haben dürfen."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Fehler bei der maximalen Anzahl von Regeln"
>abstract="Die maximale Anzahl von Regeln in einem einzelnen Container beträgt **5**. Das bedeutet, dass ein Container beim Erstellen Ihrer Zielgruppe **nicht** mehr als fünf Regeln enthalten darf."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Fehler bei der maximalen Anzahl von übergreifenden Entitäten"
>abstract="Die maximale Anzahl von Entitäten, die in einer Zielgruppe verwendet werden können, beträgt **5**. Eine übergreifende Entität ist der Fall, wenn Sie zwischen verschiedenen Entitäten in Ihrer Zielgruppe wechseln. So können Sie beispielsweise von einem Konto zu einer Person zu einer Marketingliste wechseln."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Fehler bei der benutzerdefinierten Entität"
>abstract="Benutzerdefinierte Entitäten sind **nicht** zulässig."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Fehler einer ungültigen B2B-Entität"
>abstract="Es dürfen nur die folgenden B2B-Entitäten verwendet werden: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member` und `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Maximaler Wertefehler"
>abstract="Die maximale Anzahl von Werten, die für ein einzelnes Feld überprüft werden können, beträgt **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="inSegment-Ereignisfehler"
>abstract="inSegment-Ereignisse sind **nicht** zulässig."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="inSegment-Ereignisfehler"
>abstract="inSegment-Ereignisse sind **nicht** zulässig."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Fehler bei aufeinanderfolgenden Ereignissen"
>abstract="Aufeinanderfolgende Ereignisse sind **nicht** erlaubt."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Eigenschaftsfehler vom Typ „Map“"
>abstract="Eigenschaften vom Typ „Map“ sind **nicht** zulässig."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Fehler bei der maximalen Tiefe von verschachtelten Entitäten"
>abstract="Die maximale Tiefe von verschachtelten Arrays beträgt **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Fehler bei der maximalen Anzahl verschachtelter Objekte"
>abstract="Die maximale Anzahl zulässiger verschachtelter Objekte beträgt **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Verstoß gegen eine Einschränkung"
>abstract="Die Zielgruppe verstößt gegen eine Einschränkung. Weitere Informationen hierzu finden Sie im verknüpften Dokument."

Bei der Verwendung von Kontozielgruppen muss die Zielgruppe **1} die folgenden Einschränkungen erfüllen:**

>[!NOTE]
>
>Die folgende Liste zeigt die **standardmäßigen** -Begrenzungen für Kontozielgruppen. Diese Werte **können** entsprechend den vom Administrator Ihres Unternehmens implementierten Einstellungen ändern.

- Das maximale Lookback-Fenster für Erlebnisereignisse beträgt **30 Tage**.
- Die maximale Tiefe verschachtelter Container beträgt **5**.
   - Das bedeutet, dass Sie beim Erstellen Ihrer Zielgruppe **nicht** mehr als fünf verschachtelte Container haben dürfen.
- Die maximale Anzahl von Regeln innerhalb eines einzelnen Containers beträgt **5**.
   - Das bedeutet, dass Ihre Audience **nicht mehr als fünf Regeln haben kann, aus denen Ihre Audience besteht.**
- Die maximale Anzahl von Querentitäten, die verwendet werden können, ist **5**.
   - Eine übergreifende Entität ist der Fall, wenn Sie zwischen verschiedenen Entitäten in Ihrer Zielgruppe wechseln. So können Sie beispielsweise von einem Konto zu einer Person zu einer Marketingliste wechseln.
- Benutzerdefinierte Entitäten **können nicht** verwendet werden.
- Die maximale Anzahl von Werten, die für ein einzelnes Feld überprüft werden können, beträgt **50**.
   - Wenn Sie beispielsweise das Feld &quot;Stadt&quot;haben, können Sie diesen Wert mit 50 Stadtnamen vergleichen.
- Kontozielgruppen **können** keine `inSegment` -Ereignisse verwenden.
- Kontozielgruppen **können keine sequenziellen Ereignisse verwenden.**
- Kontozielgruppen **können keine Karten verwenden**.
- Die maximale Tiefe von verschachtelten Arrays beträgt **5**.
- Die maximale Anzahl verschachtelter Objekte ist **10**.

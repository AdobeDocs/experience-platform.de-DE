---
title: Bestimmen einer Tendenzbewertung mithilfe eines vom maschinellen Lernen erzeugten Prognosemodells
description: Erfahren Sie, wie Sie mit Query Service Ihr prädiktives Modell auf Platform-Daten anwenden können. In diesem Dokument wird gezeigt, wie Platform-Daten verwendet werden, um die Kaufneigung eines Kunden bei jedem Besuch vorherzusagen.
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: 40c27a52fdae2c7d38c5e244a6d1d6ae3f80f496
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Bestimmen eines Tendenzwerts mithilfe eines vom maschinellen Lernen generierten Prognosemodells

Mithilfe von Query Service können Sie prädiktive Modelle wie Tendenzwerte nutzen, die auf Ihrer maschinellen Lernplattform zur Analyse von Daten zur Experience Platform aufbauen.

In diesem Handbuch wird erläutert, wie Sie mithilfe von Query Service Daten an Ihre Plattform für maschinelles Lernen senden können, um ein Modell in ein rechnergestütztes Notebook zu trainieren. Das trainierte Modell kann mithilfe von SQL auf Daten angewendet werden, um die Kaufneigung eines Kunden bei jedem Besuch vorherzusagen.

## Erste Schritte

Im Rahmen dieses Prozesses müssen Sie ein Modell für maschinelles Lernen trainieren. In diesem Dokument wird davon ausgegangen, dass Sie über Kenntnisse in einer oder mehreren Umgebungen für maschinelles Lernen verfügen.

Dieses Beispiel verwendet [!DNL Jupyter Notebook] als Entwicklungsumgebung. Es stehen zwar viele Optionen zur Verfügung, [!DNL Jupyter Notebook] wird empfohlen, da es sich um eine Open-Source-Webanwendung mit niedrigen Rechenanforderungen handelt. Es kann [von der offiziellen Website heruntergeladen](https://jupyter.org/).

Wenn Sie dies noch nicht getan haben, führen Sie die Schritte aus, um [connect [!DNL Jupyter Notebook] mit Adobe Experience Platform Query Service](../clients/jupyter-notebook.md) bevor Sie mit diesem Handbuch fortfahren.

Die in diesem Beispiel verwendeten Bibliotheken umfassen:

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Importieren von Analysetabellen aus Platform in [!DNL Jupyter Notebook] {#import-analytics-tables}

Um ein Tendenzwertmodell zu generieren, muss eine Projektion der in Platform gespeicherten Analysedaten in [!DNL Jupyter Notebook]. Von einem [!DNL Python] 3 [!DNL Jupyter Notebook] mit Query Service verbunden sind, importieren die folgenden Befehle einen Datensatz zum Kundenverhalten aus Luma, einem fiktiven Bekleidungsspeicher. Da Platform-Daten im XDM-Format (Experience-Datenmodell) gespeichert werden, muss ein JSON-Beispielobjekt generiert werden, das der Struktur des Schemas entspricht. Anweisungen dazu finden Sie in der Dokumentation . [JSON-Beispielobjekt generieren](../../xdm/ui/sample.md).

![Die [!DNL Jupyter Notebook] Dashboard mit mehreren hervorgehobenen Befehlen.](../images/use-cases/jupyter-commands.png)

Die Ausgabe zeigt eine tabellarische Ansicht aller Spalten aus dem Verhaltensdatensatz von Luma innerhalb der Variablen [!DNL Jupyter Notebook] Dashboard.

![Die tabularisierte Ausgabe des importierten Datasets zum Kundenverhalten von Luma in [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Daten für maschinelles Lernen vorbereiten {#prepare-data-for-machine-learning}

Eine Zielspalte muss identifiziert werden, um ein Modell für maschinelles Lernen zu trainieren. Da die Kaufneigung das Ziel für diesen Anwendungsfall ist, wird die `analytic_action` wird als Zielspalte aus den Luma-Ergebnissen ausgewählt. Der Wert `productPurchase` ist der Indikator für einen Kundenkauf. Die `purchase_value` und `purchase_num` -Spalten werden ebenfalls entfernt, da sie direkt mit der Aktion &quot;Produktkauf&quot;verbunden sind.

Die Befehle zum Ausführen dieser Aktionen lauten wie folgt:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Anschließend müssen die Daten aus dem Datensatz &quot;Luma&quot;in geeignete Darstellungen umgewandelt werden. Zwei Schritte sind erforderlich:

1. Wandeln Sie die Zahlenspalten in numerische Spalten um. Konvertieren Sie dazu explizit den Datentyp im `dataframe`.
1. Kategorische Spalten können auch in numerische Spalten umgewandelt werden.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Eine Technik namens *eine Hot-Kodierung* wird verwendet, um die kategorischen Datenvariablen für die Verwendung mit maschinellen und tiefen Lernalgorithmen zu konvertieren. Dies verbessert wiederum die Vorhersagen sowie die Klassifizierungsgenauigkeit eines Modells. Verwenden Sie die `Sklearn` -Bibliothek, um jeden kategorischen Wert in einer separaten Spalte darzustellen.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

Die als `X` ist tabellarisch und wird wie folgt angezeigt:

![Die tabularisierte Ausgabe von X innerhalb [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Nachdem die erforderlichen Daten für maschinelles Lernen verfügbar sind, können sie an die vorkonfigurierten Modelle für maschinelles Lernen in [!DNL Python]s `sklearn` -Bibliothek. [!DNL Logistics Regression] wird verwendet, um das Tendenzmodell zu trainieren, und ermöglicht Ihnen, die Genauigkeit von Testdaten zu sehen. In diesem Fall liegt er bei etwa 85 %.

Die [!DNL Logistic Regression] -Algorithmus und die Zugtest-Aufspaltungsmethode, mit der die Leistung von Algorithmen für maschinelles Lernen geschätzt wird, werden in den folgenden Codeblock importiert:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

Die Testdatengenauigkeit beträgt 0,8518518518518519.

Mithilfe der Logistik-Regression können Sie die Gründe für einen Kauf visualisieren und die Funktionen sortieren, die die Neigung nach ihrer Rangfolge in absteigenden Bestellungen bestimmen. Die ersten Spalten bezeichnen einen höheren Kausalzusammenhang, der zum Kaufverhalten führt. Die letztgenannten Spalten zeigen Faktoren an, die nicht zum Kaufverhalten führen.

Der Code zur Visualisierung der Ergebnisse in Form von zwei Balkendiagrammen lautet wie folgt:

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

Unten finden Sie eine Darstellung der Ergebnisse in einem vertikalen Balkendiagramm:

![Die Visualisierung der 10 wichtigsten Funktionen, die eine Kaufneigung definieren oder nicht kaufen.](../images/use-cases/visualized-results.png)

Im Balkendiagramm können mehrere Muster angezeigt werden. Die Themen Point of Sale (POS) und Call as Kostenerstattung sind die wichtigsten Faktoren für das Kaufverhalten des Kanals. Während die Themen Aufruf als Beschwerden und Rechnungen wichtige Rollen sind, um das nicht Kaufverhalten zu definieren. Hierbei handelt es sich um quantifizierbare, umsetzbare Einblicke, die Marketing-Experten nutzen können, um Marketingkampagnen durchzuführen, um die Kaufneigung dieser Kunden zu bekämpfen.

## Verwenden Sie Query Service , um das trainierte Modell anzuwenden {#use-query-service-to-apply-trained-model}

Nachdem das trainierte Modell erstellt wurde, muss es auf die in Experience Platform gespeicherten Daten angewendet werden. Dazu muss die Logik der Pipeline für maschinelles Lernen in SQL konvertiert werden. Die beiden wichtigsten Komponenten dieser Transition sind:

- Zunächst muss SQL die [!DNL Logistics Regression] -Modul, um die Wahrscheinlichkeit einer Prognosebeschriftung zu erhalten. Das von der Logistik-Regression erstellte Modell erzeugte Regressionsmodell `y = wX + c`  wobei Gewichte `w` und abfangen `c` sind die Ausgabe des Modells. SQL-Funktionen können verwendet werden, um die Gewichtungen zu multiplizieren, um eine Wahrscheinlichkeit zu erhalten.

- Zweitens: der in [!DNL Python] mit einer heißen Kodierung muss auch in SQL integriert werden. In der ursprünglichen Datenbank haben wir beispielsweise `geo_county` -Spalte, um den Kreis zu speichern, aber die Spalte in `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. Die folgende SQL-Anweisung führt dieselbe Transformation durch, wobei `w1`, `w2`und `w3` könnte durch die aus dem Modell in gelernten Gewichtungen ersetzt werden. [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Bei numerischen Funktionen können Sie die Spalten direkt mit den Gewichtungen multiplizieren, wie in der SQL-Anweisung unten dargestellt.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Nachdem die Zahlen erhalten wurden, können sie auf eine Sigmoid-Funktion portiert werden, bei der der Logistics Regression-Algorithmus die endgültigen Prognosen erzeugt. In der nachstehenden Erklärung: `intercept` ist die Nummer der Konstante in der Regression.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Ein Beispiel von Ende zu Ende

In einer Situation, in der Sie über zwei Spalten verfügen (`c1` und `c2`), wenn `c1` hat zwei Kategorien, die [!DNL Logistic Regression] Algorithmus wird mit der folgenden Funktion trainiert:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
Die Entsprechung in SQL lautet wie folgt:

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
Die [!DNL Python] Code zur Automatisierung des Übersetzungsprozesses lautet wie folgt:

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

Wenn SQL zum Ableiten der Datenbank verwendet wird, lautet die Ausgabe wie folgt:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

Die tabellarisierten Ergebnisse zeigen die Kaufneigung für jede Kundensitzung mit `0` bedeutet keine Kaufneigung und `1` bedeutet eine bestätigte Kaufneigung.

![Die tabularisierten Ergebnisse der Datenbankeinleitung mit SQL.](../images/use-cases/inference-results.png)

## Arbeiten mit Stichprobendaten: Bootstrapping {#working-on-sampled-data}

Falls die Datengrößen für Ihren lokalen Computer zu groß sind, um die Daten für die Modellschulung speichern zu können, können Sie anstelle der vollständigen Daten von Query Service Beispiele verwenden. Um zu erfahren, wie viele Daten zum Beispiel von Query Service benötigt werden, können Sie eine Methode namens Bootstrapping anwenden. In dieser Hinsicht bedeutet Bootstrapping, dass das Modell mehrmals mit verschiedenen Proben trainiert wird und die Varianz der Genauigkeit des Modells zwischen verschiedenen Proben untersucht wird. Um das oben angegebene Tendenzmodell anzupassen, schließen Sie zunächst den gesamten Workflow für maschinelles Lernen in eine Funktion ein. Der Code lautet wie folgt:

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

Diese Funktion kann dann mehrmals in einer Schleife ausgeführt werden, z. B. zehnmal. Der Unterschied zum vorherigen Code besteht darin, dass das Beispiel jetzt nicht aus der gesamten Tabelle, sondern nur aus einer Stichprobe von Zeilen genommen wird. Der folgende Beispielcode nimmt beispielsweise nur 1000 Zeilen in Anspruch. Die Genauigkeit für jede Iteration kann gespeichert werden.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

Die Genauigkeit des Bootstrapping-Modells wird dann sortiert. Danach werden die 10. und 90. Mengen der Genauigkeit des Modells zu einem 95%-Konfidenzintervall für die Genauigkeit des Modells mit der angegebenen Stichprobengröße.

![Der Druckbefehl zum Anzeigen des Konfidenzintervalls des Tendenzwerts.](../images/use-cases/confidence-interval.png)

In der obigen Abbildung wird angegeben, dass Sie bei nur 1.000 Zeilen für das Trainieren Ihrer Modelle mit einer Genauigkeit zwischen etwa 84 % und 88 % rechnen können. Sie können die `LIMIT` -Klausel in Query Service-Abfragen auf Grundlage Ihrer Anforderungen verwenden, um die Leistung der Modelle sicherzustellen.

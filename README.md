# Case Study #04: Global Electronics Store Chain

---

## **1. Executive Summary**: 
Diese Case Study analysiert eine globale Elektronikhandelskette (hauptsächlich in Europa) mit **144 Filialen in 37 Ländern**, basierend auf Sales-, Inventur- und Produktdaten vom **02.–05. Januar 2017**.  
Die Analyse zeigt, dass **Solar Blender Lux** das meistverkaufte Produkt war und ca. **85 Mio. €** Umsatz generiert hat, während **Expert MegaDom (13 Mio. €)** die umsatzstärkste Filiale und **Moskau (20 Mio. €)** die führende Stadt war.  
Das deutet darauf hin, dass KW 1 (02.–05. Jan) eine starke Periode für sowohl Expert MegaDom als auch Moskau war und dass die Marketing- bzw. Promotionsstrategie für Solar Blender Lux sehr attraktiv und effektiv war.  
Daraus ergeben sich folgende Empfehlungen:
1. Aufbauend auf diesen Marketingkampagnen und Angeboten in zukünftigen Perioden weiterarbeiten
2. Beste Merkmalen von Top Filialen auf schwächer performende Filialen übertragen

## **2. Aufgabe**:
#### *Analyse der Umsatzverteilung über **Produkte, Filialen und Städte** sowie Identifikation der wichtigsten Treiber*  

Dieses deskriptive Dashboard zeigt den Gesamtumsatz, die Anzahl der Filialen und Städte sowie die Top 10 Filialen & Städte und den täglichen Umsatz in der ersten Woche 2017.  

![image.png](attachment:image.png)  

## **3. Dataset Überblick**

**Datenquelle**: *IBM BI Analyst Course - Capstone Project*  
**Dataset/Datensatz**: *6 Tabllen (City_Names, Product_Hierarchy, Product_Names, Sales, Store_Cities, Store_Names)*  
**Zeitraum**: *Jan 02 - Jan 05 (2017)*

Datensatz Tabellen:  
![image-15.png](attachment:image-15.png)  

## **4. Datenbereinigung & Vorbereitung**

1. Hauptordner CS04_GlobalElectronicsStoreChain erstellt
2. Unterordner erstellt: 00_Dataset; 01_Data_Cleaning; 02_Data_Analysis; 03_Data_Visualization; 04_Reporting
3. Originaldateien heruntergeladen und unter 00_Dataset gespeichert
4. Dateien in 01_Data_Cleaning kopiert
5. Alle 6 Tabellen bereinigt und für die Analyse vorbereitet (Tabellen geprüft, Datentypen kontrolliert, Rechtschreibfehler, fehlende Werte und Duplikate bereinigt, Spalten formatiert, Texte standardisiert, leere Spalten entfernt)  
  5.1 Pivot Tabellen, Helper Columns, Flash Fill, XLOOKUP und weitere Funktionen verwendet um bereinigte Daten sicher zu stellen
6. BONUS: Teilweise synthetische Daten genutzt, um fehlende Werte (kleiner Anteil) mit Durchschnitts- oder häufigsten Werten zu füllen

## **5. Methodologie**

1. Datensatz heruntergeladen und strukturiert  

![image-15.png](attachment:image-15.png)  
*Datensatz Ordner*

---

2. Daten bereinigt, vorbereitet und für die Analyse zusammengeführt  
|  
v  
Beispiel (früher und später):  
![image-4.png](attachment:image-4.png) zum ![image-8.png](attachment:image-8.png)  

---

3. Analyse und Ableitung von Key Insights in Excel und SQL

Excel:  

![image-5.png](attachment:image-5.png)  


SQL:  

![image-7.png](attachment:image-7.png)  

---

4. Interaktive Power BI Dashboards erstellt (Descriptive, Products, Stores, Cities)  

![image-9.png](attachment:image-9.png)  

---

## **6. Fähigkeiten**

    SQL: Trendanalyse, CTEs, Joins, Window Funktionen
    Excel: Datenbereinigung, Transformation, Pivot Tabellen, Analyse
    Power BI: Datenmodellierung, interaktive Dashboards, Visualisierung, DAX
    Jupyter Notebook: Markdown Dokumentation

**Quick SQL Code**:
```
#Task 8: Ermittle tägliche Gesamtsumme und den gleitenden Durchschnitt pro Filiale
CREATE OR REPLACE VIEW GESC_DataAnalysis.08_Daily_Revenue_RunningTotal_and_RunningAVG_per_Store AS
  SELECT
    store_id,
    date,
    daily_revenue,
    SUM(daily_revenue) OVER(partition by store_id ORDER BY date) AS running_total,
    AVG(daily_revenue) OVER(partition by store_id ORDER BY date) AS running_average
  FROM(
    SELECT
      store_id,
      date,
      SUM(revenue) AS daily_revenue
    FROM
      `globalelectronicstorechain.GESC_DataAnalysis.Sales`
    GROUP BY
      store_id,
      date
  )
  ORDER BY
    store_id,
    date;
```
## **7. Ergebnisse**

Diese Analyse basiert auf einem Dataset-Snapshot mit **699 Produkten, 144 Filialen und 37 Städten**.  
**Moskau** war die umsatzstärkste Stadt (**20 Mio. €**), mit **Expert MegaDom** als Top-Filiale in Moskau und gleichzeitig #1 insgesamt (**13 Mio. €**).  
Das meistverkaufte Produkt war **Solar Blender Lux** mit über **420K Verkäufen**, **85 Mio. €** Umsatz und einem Anteil von **83%** am Gesamtumsatz.  
Zwei mögliche Erklärungen für diesen starken Ausreißer:  
1. **Realistischer**: Es handelt sich nur um einen kleinen Dataset-Snapshot – im vollständigen Datensatz würde sich die Verteilung normalisieren
2. **Alternativ**: Da könnte man für den Zweck dieser Case Study annehmen, dass eine Marketingkampagne außergewöhnlich erfolgreich war (auch wenn es eher unwahrscheinlich ist, dass allein dadurch ein so extremer Ausreißer entsteht) und darauf basierend eine entsprechende Story bzw. ein Narrativ aufbauen.  

**Store Type 4** machte den Großteil des Umsatzes aus (**83%**), stark beeinflusst durch den Solar Blender Lux Effekt.  
Die Korrelation zwischen Bestand und Umsatz liegt bei **0,33** – jedoch mit vielen Abweichungen, daher kein klarer Zusammenhang.  
Obwohl London die meisten Filialen hatte, war Moskau insgesamt die stärkste Stadt nach Umsatz.  

#### **Visuals**

Top 10 Städte nach Umsatz:

![image-6.png](attachment:image-6.png)  

---

Umsatztreiber und Bestseller:  

![image-10.png](attachment:image-10.png)

---

Die leistungsstärksten Geschäfte:

![image-11.png](attachment:image-11.png)  

---

Umsatzanteil nach Filialtyp:

![image-12.png](attachment:image-12.png)  

---

Korrelation zwischen Lagerbestand und Umsatz:

![image-13.png](attachment:image-13.png)  

---

Gesamtzahl der Filialen pro Stadt:

![image-14.png](attachment:image-14.png)  

## **8. Key Insights**

* Moskau ist die umsatzstärkste Stadt
* Expert MegaDom ist die beste Filiale
* Solar Blender Lux ist das meistverkaufte Produkt
* Overstocking zeigt keinen starken positiven Einfluss auf Sales

## **9. Empfehlungen**

* Auf der **Solar Blender Lux** Kampagne aufbauen
* Beste Merkmalen von Top-Filialen auf schwächere übertragen
* Überbestände bei Low-Priority-Produkten reduzieren

## **10. Limitationen**

* Nur ein kleiner Ausschnitt des vollständigen Datensatzes
* Sehr kurzer Zeitraum (02.–05. Jan) -> anfällig für Ausreißer
* Daten stammen aus 2017
* Der Solar Blender Lux Ausreißereffekt verzerrt die Umsatzverteilung stark (auch wenn man ihn aus der Analyse ausschließen könnte, war er für die Marketing-Story dennoch hilfreich)
* Mischung aus realen und fiktiven Filialen

## **11. Nächste Schritte**

* Zugriff auf vollständigen Datensatz
* Längerer Zeitraum (z.B. 2–3 Jahre) für bessere Insights
* Echtzeitsdaten integrieren
* Saisonalität, Kampagnen und Events berücksichtigen
* Ausreißer-Produkte wie Solar Blender Lux genauer validieren

## **12. Tools**

* SQL
* Excel
* Power BI
* Jupyter

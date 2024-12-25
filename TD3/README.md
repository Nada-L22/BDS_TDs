# TD-3: Spatial SQL Functions

In this exercise, we will use PostGIS to determine spatial relationships between parcels and fire points, such as identifying parcels within a 1 km radius of fire points, calculating total areas, and more.

---

## 1. Import the Shapefile into PostGIS

### Steps:
1. Download the Florida parcels shapefile from [this link](https://maps.leegov.com/datasets/80708a2f5f56426f94c8be97c182176b/about).
2. Open **PostGIS Shapefile Import/Export Manager**:
   - On Windows, search for "shapefile" in the Start Menu and select the tool.
3. Select the shapefile of the Florida parcels and import it into your PostgreSQL database.

### Verification:
Run the following queries in **pgAdmin**:
```sql
-- Count the total number of parcels
SELECT COUNT(*) FROM parcels;

-- Preview the first 5 rows of the table
SELECT * FROM parcels LIMIT 5;
```

---

## 2. Identify the Fire Point (Centroid of Parcel 462273)

### SQL Query:
To locate the fire point (centroid of the parcel with `gid = 462273`):
```sql
SELECT ST_Centroid(geom) AS fire_point
FROM parcels
WHERE gid = 462273;
```

---

## 3. Create a Fire-Risk Zone (1 km Radius Around the Fire Point)

### Steps in QGIS:
1. Duplicate the `parcels` layer and rename it as `fire-risk`.
2. Right-click on the `fire-risk` layer and select **Filter**.
3. Add the following filter expression to create a 1 km buffer around the fire point:
   ```sql
   ST_DWithin(geom, (SELECT ST_Centroid(geom) FROM "public"."parcels" WHERE gid = 462273), 1000)
   ```
4. Change the layer's symbology to highlight the fire-risk zones.

---

## 4. Include a Second Fire Point (Parcel 460957)

If another fire point is identified in the parcel with `gid = 460957`, update the QGIS filter to include both points:
```sql
ST_DWithin(geom, (SELECT ST_Union(ST_Centroid(geom)) FROM "public"."parcels" WHERE gid IN (462273, 460957)), 1000)
```

This filter detects parcels within 1 km of either fire point.

---

## 5. Perform Spatial Analysis Using SQL in pgAdmin

### a) Count the Number of Parcels Within 1 km of Both Fire Points:
```sql
SELECT COUNT(*)
FROM parcels
WHERE ST_DWithin(geom, (SELECT ST_Union(ST_Centroid(geom)) FROM parcels WHERE gid IN (462273, 460957)), 1000);
```

### b) Calculate the Total Area of Parcels Near the Fire Points:
```sql
SELECT SUM(ST_Area(geom))
FROM parcels
WHERE ST_DWithin(geom, (SELECT ST_Union(ST_Centroid(geom)) FROM parcels WHERE gid IN (462273, 460957)), 1000);
```

---

## Conclusion

This TD allowed us to:
1. Import spatial data into PostGIS.
2. Use spatial SQL functions to identify points and areas of interest.
3. Perform spatial analysis to determine the number and area of parcels within a fire-risk zone.
4. Integrate QGIS for visualization and advanced filtering of spatial data.

# TD-2: Creation of Tables with Spatial Columns

In this exercise, we will create spatial tables in PostgreSQL using PgAdmin and QGIS, and we will insert data into these tables. This includes creating tables with columns of type `Point`, `Polygon`, and `LineString`.

## 1. Create a Spatial Table (Points)

First, we create a spatial table `points_of_interests` with a column of type `Point`.

### SQL Query to Create Table:
```sql
CREATE TABLE points_of_interests (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(255),
    geom GEOMETRY(Point, 4326)
);
```

### Inserting Data Using QGIS:
1. Open **QGIS** and connect to your **PostgreSQL database**:
    - Right-click on **PostgreSQL** in the Browser panel.
    - Select **New Connection** and enter your connection details for the database.
    - Test the connection to ensure it is successful.
2. Once the connection is established, double-click on the `points_of_interests` table to add it as a layer in QGIS.
3. Switch to **Edit Mode** in QGIS and add new points to the layer.
4. After adding the points, click **Save** to persist the changes.
5. To verify the data, go to **PgAdmin** and execute the following SQL query:
    ```sql
    SELECT * FROM points_of_interests;
    ```

## 2. Create a Spatial Table (Polygons)

Now, we create a spatial table `zones_protegees` with a column of type `Polygon`.

### SQL Query to Create Table:
```sql
CREATE TABLE zones_protegees (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(255),
    geom GEOMETRY(Polygon, 4326)
);
```

### Inserting Data Using QGIS:
1. Open **QGIS** and connect to your **PostgreSQL database** if you haven't already.
2. Double-click on the `zones_protegees` table to add it as a new layer in QGIS.
3. Switch to **Edit Mode** in QGIS and draw polygons on the map.
4. Once you've drawn the polygons, click **Save** to store the changes in the database.
5. To verify the data, execute the following query in **PgAdmin**:
    ```sql
    SELECT * FROM zones_protegees;
    ```

## 3. Create a Spatial Table (LineStrings)

Lastly, we create a spatial table `routes` with a column of type `LineString`.

### SQL Query to Create Table:
```sql
CREATE TABLE routes (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(255),
    geom GEOMETRY(LineString, 4326)
);
```

### Inserting Data Using QGIS:
1. Open **QGIS** and connect to your **PostgreSQL database** if not already done.
2. Double-click on the `routes` table to add it as a new layer in QGIS.
3. Switch to **Edit Mode** and draw lines to represent the routes on the map.
4. After adding the lines, click **Save** to store the changes in the database.
5. To verify the data, run the following query in **PgAdmin**:
    ```sql
    SELECT * FROM routes;
    ```

## Conclusion

By following these steps, we have successfully created and populated spatial tables with different types of geometries (Point, Polygon, and LineString) in a PostgreSQL database using QGIS for data entry. Each table was verified by executing SQL queries in PgAdmin.

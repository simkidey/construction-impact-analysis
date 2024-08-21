## Construction Challenges for Autonomous Vehicles
The documents provides the solution posted for the challenges posted by construction for Autonomous Vehicles

### Data Setup
To carry out the exercise, **Postgres** was chosen the backend database to carry out all relevant operations.
- A local docker Postgres database was setup using the Postgres docker image.
- IDE used for the development purpose was **IntelliJ DataGrip**
- To load the data for the Construction, the csv file (`US_Constructions_Dec21.csv`) was downloaded from Kaggle and the data was imported into a table `Construction` in our local database. During the import the necessary data casting was done automatically. Hence the date fields are of date/timestamp format and not varchar.
- To load the `sf_paths.xlsx` into the table, we made some additional changes.
    - The postgres image was changed to `PostGis` image in `docker-compose.yaml` file
    - Enabled the extension Postgis in the database.
- Used SQL to load the data in the tables
```sql
create table if not exists path (
    path_name	varchar,
    path_wkt	geometry,
    distance_mi float
);

CREATE EXTENSION postgis;

insert into path values
    ('SF -> Berkley', 'LINESTRING (-122.41928 37.77492, ...)', 13.58),
    ('SF -> San Rafael', 'LINESTRING (-122.41928 37.77492,...)', 18.66),
    ('SF -> San Mateo', 'LINESTRING (-122.41928 37.77492, ...)', 19.3),
    ('SF -> San Leandro', 'LINESTRING (-122.41928 37.77492, ...)', 21.21),
    ('SF -> Pacifica', 'LINESTRING (-122.41928 37.77492, ...)', 15.37)
;
```

### How to setup the environment locally
- You should have docker configured and running locally as a pre-requisite
- Run the following command to start the Postgres instance locally:
```bash
docker compose up -d
```
- To test the postgres instance is up and running check the process
```
docker ps
```
- Connect to the postgres instance

```bash
pgcli postgres://postgres:pstgres@localhost:5432/simki
```

### Solution
The solution is provided in the [SOLUTION.MD](SOLUTION.MD)

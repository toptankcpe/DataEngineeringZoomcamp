## Module 1 Homework

### Question 1
#### Answer:
```bash
docker run -it m1:q1
pip --version
```

### Question 3
#### Answer:
```sql
SELECT count(*) 
FROM public.green_tripdata 
WHERE "lpep_pickup_datetime" >= '2019-10-01' 
  AND "lpep_pickup_datetime" < '2019-11-01' 
  AND "lpep_dropoff_datetime" < '2019-11-01' 
  AND trip_distance <= 1;

SELECT count(*) 
FROM public.green_tripdata 
WHERE "lpep_pickup_datetime" >= '2019-10-01' 
  AND "lpep_pickup_datetime" < '2019-11-01' 
  AND "lpep_dropoff_datetime" < '2019-11-01' 
  AND trip_distance > 1 AND trip_distance <= 3;

SELECT count(*) 
FROM public.green_tripdata 
WHERE "lpep_pickup_datetime" >= '2019-10-01' 
  AND "lpep_pickup_datetime" < '2019-11-01' 
  AND "lpep_dropoff_datetime" < '2019-11-01' 
  AND trip_distance > 3 AND trip_distance <= 7;

SELECT count(*) 
FROM public.green_tripdata 
WHERE "lpep_pickup_datetime" >= '2019-10-01' 
  AND "lpep_pickup_datetime" < '2019-11-01' 
  AND "lpep_dropoff_datetime" < '2019-11-01' 
  AND trip_distance > 7 AND trip_distance <= 10;

SELECT count(*) 
FROM public.green_tripdata 
WHERE "lpep_pickup_datetime" >= '2019-10-01' 
  AND "lpep_pickup_datetime" < '2019-11-01' 
  AND "lpep_dropoff_datetime" < '2019-11-01' 
  AND trip_distance > 10;
```

### Question 4
#### Answer:
```sql
SELECT "lpep_pickup_datetime", 
       MAX(trip_distance) AS trip_distance 
FROM public.green_tripdata 
GROUP BY "lpep_pickup_datetime" 
ORDER BY trip_distance DESC 
LIMIT 1;
```

### Question 5
#### Answer:
```sql
SELECT tz."LocationID" AS location_id, 
       tz."Zone" AS location_zone, 
       SUM(gt."total_amount") AS total_amount 
FROM public.green_tripdata gt
INNER JOIN public.taxi_zone tz 
        ON gt."PULocationID" = tz."LocationID"
WHERE gt."lpep_pickup_datetime" >= '2019-10-18 00:00:00' 
  AND gt."lpep_pickup_datetime" < '2019-10-19 00:00:00'
GROUP BY location_id, location_zone
HAVING SUM(gt."total_amount") > 13000 
ORDER BY total_amount DESC;
```

### Question 6
#### Answer:
```sql
SELECT tz_do."Zone" AS do_location_zone, 
       MAX(gt."tip_amount") AS max_tip 
FROM public.green_tripdata gt
INNER JOIN public.taxi_zone tz_pu 
        ON gt."PULocationID" = tz_pu."LocationID"
INNER JOIN public.taxi_zone tz_do 
        ON gt."DOLocationID" = tz_do."LocationID"
WHERE gt."lpep_pickup_datetime" >= '2019-10-01 00:00:00' 
  AND gt."lpep_pickup_datetime" < '2019-11-01 00:00:00' 
  AND tz_pu."Zone" = 'East Harlem North'
GROUP BY do_location_zone
ORDER BY max_tip DESC
LIMIT 1;
```

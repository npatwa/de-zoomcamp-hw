# Home Work 1

## Q1 

```sh
docker run -it --entrypoint=bash python:3.12.8
python
import pip
pip.__version__
```

## Q2
Answer is postgres:5432

## Q3
 ```sh
SELECT count(*) FROM public.green_taxi_data where trip_distance <= 1

SELECT count(*) FROM public.green_taxi_data where trip_distance > 1 and trip_distance <=3

SELECT count(*) FROM public.green_taxi_data where trip_distance > 3 and trip_distance <=7

SELECT count(*) FROM public.green_taxi_data where trip_distance > 7 and trip_distance <=10

SELECT count(*) FROM public.green_taxi_data where trip_distance > 10
```
Answer is 104,838; 199,013; 109,645; 27,688; 35,202

## Q4
```sh
select lpep_pickup_datetime from public.green_taxi_data where trip_distance = (select max(trip_distance) from public.green_taxi_data)
```

Answer is 2019-10-31

## Q5
```sh
select z."Zone", sum(t.total_amount) as tot
from green_taxi_data t join zones z on t."PULocationID"=z."LocationID"  
where date(t.lpep_pickup_datetime)= '2019-10-18'
group by z."Zone"
having sum(t.total_amount) > 13000
```

Answer is East Harlem North, East Harlem South, Morningside Heights

## Q6
```sh
select zdrop."Zone", sum(t.tip_amount)
from green_taxi_data t, zones zpick, zones zdrop
where t."DOLocationID" = zdrop."LocationID" and
	t."PULocationID" = zpick."LocationID" and
	zpick."Zone" = 'East Harlem North'
group by zdrop."Zone"
order by sum(t.tip_amount) DESC
```

Answer is East Harlem South
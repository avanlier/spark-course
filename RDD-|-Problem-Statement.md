## Transformations

In the context of Spark, transformations are operations that create a new dataset by applying a specific function to each element of an existing dataset. Let's explore two use cases where transformations, such as `filter` and `map`, are applied to analyze airport data.

### Use Case 1: Airports in the United States

We begin by creating a Java class named "AirportsInUsaProblem" within the package "com.sparkTutorial.rdd.airportspackage." Our goal is to analyze data from the "airports.text" file, which contains information about airports worldwide. Specifically, we want to identify airports located in the United States and extract their names and respective cities.

> #### Here's the problem statement:

> **Create a Spark program to read airport data from "in/airports.text," identify all airports in the United States, and output the airport names and their corresponding cities to "out/airports_in_usa.text."**

> Each row in the input file includes columns like Airport ID, Airport Name, Main City Served, Country, IATA/FAA Code, ICAO Code, Latitude, Longitude, Altitude, Timezone, DST, and Timezone in Olson format.

> Sample output:

> -   "Putnam County Airport", "Greencastle"
> -   "Dowagiac Municipal Airport", "Dowagiac"

### Use Case 2: Airports by Latitude

In the second scenario, we create a Java class called "AirportsByLatitudeProblem" in the "com.sparkTutorial.rdd.airports" package. This time, we aim to identify airports with latitudes greater than 40 degrees and output pairs of airport names and their respective latitudes.

> #### Here's the problem statement:

> **Create a Spark program to read airport data from "in/airports.text," identify all airports with latitudes greater than 40, and output the airport names along with their latitudes to "out/airports_by_latitude.text."**

> Again, each row in the input file consists of columns like Airport ID, Airport Name, Main City Served, Country, IATA/FAA Code, ICAO Code, Latitude, Longitude, Altitude, Timezone, DST, and Timezone in Olson format.

> Sample output:

> -   "St Anthony", 51.391944
> -   "Tofino", 49.082222

In both cases, we utilize Spark transformations to filter and map the data according to specific criteria, generating meaningful insights from the given dataset.
# mySQL-project-1
Railway System Database

This code creates a basic railway system database schema in MySQL. It includes tables for stations, trains, routes, and schedules.
Database Structure
The database consists of the following tables:
 * Stations: Stores information about stations, including station ID, name, city, and state.
 * Trains: Stores information about trains, including train ID, name, capacity, and type (e.g., express, passenger).
 * Routes: Stores information about train routes, including route ID, origin station ID, destination station ID, and distance.
 * Schedules: Stores the schedule for each train on a route, including schedule ID, route ID, train ID, departure time, and arrival time.
Dependencies
 * MySQL database server
Setup Instructions
 * Install MySQL server on your system.
 * Create a database for your railway system.
 * Run the provided SQL script to create the tables in your database.
Customization
This is a basic schema and can be extended to include additional features such as:
 * Passenger information
 * Booking details
 * Fare information
 * Train availability
Further Development
 * Implement functionalities like ticket booking and cancellation.
 * Create a user interface to interact with the database.
 * Generate reports on ridership, revenue, and train performance.




DROP SCHEMA IF EXISTS railway_system CASCADE;
CREATE SCHEMA IF NOT EXISTS railway_system;

DROP TABLE IF EXISTS railway_system.user_login;
CREATE TABLE IF NOT EXISTS railway_system.user_login (
	user_id TEXT PRIMARY KEY,
    user_password TEXT,
    first_name TEXT,
	last_name TEXT,
	sign_up_on DATE,
	email_id TEXT
);

DROP TABLE IF EXISTS railway_system.passenger;
CREATE TABLE IF NOT EXISTS railway_system.passenger (
	passenger_id TEXT PRIMARY KEY,
    user_password TEXT,
    first_name TEXT,
	last_name TEXT,
	sign_up_on DATE,
	email_id TEXT,
	contact TEXT
);

DROP TABLE IF EXISTS railway_system.train_type;
CREATE TABLE IF NOT EXISTS railway_system.train_type (
	train_type_id TEXT PRIMARY KEY,
    train_type TEXT,
    coaches_count TEXT,
	passenger_strength TEXT,
	train_count DATE
);

DROP TABLE IF EXISTS railway_system.stations;
CREATE TABLE IF NOT EXISTS railway_system.stations (
	station_id TEXT PRIMARY KEY,
    station_name TEXT,
	city TEXT,
	state TEXT
);

DROP TABLE IF EXISTS railway_system.train_details;
CREATE TABLE IF NOT EXISTS railway_system.train_details (
	train_id TEXT PRIMARY KEY,
    train_type_id TEXT REFERENCES railway_system.train_type (train_type_id),
    source_station_id TEXT REFERENCES railway_system.stations (station_id),
	destination_station_id TEXT REFERENCES railway_system.stations (station_id),
	duration_minutes INT,
	journey_start TIMESTAMP,
	journey_end TIMESTAMP,
	passenger_strength INT,
	is_available BOOLEAN
);

DROP TABLE IF EXISTS railway_system.journey;
CREATE TABLE IF NOT EXISTS railway_system.journey (
	journey_id TEXT PRIMARY KEY,
	passenger_id TEXT REFERENCES railway_system.passenger (passenger_id),
	train_id TEXT REFERENCES railway_system.train_details (train_id),
    booking_id TEXT,
	payment_id TEXT,
	payment_status TEXT,
	paid_on TIMESTAMP,
	booking_status TEXT,
	booked_on TIMESTAMP,
	seat_alloted TEXT,
	meal_booked BOOLEAN
);

DROP TABLE IF EXISTS railway_system.train_routes;
CREATE TABLE IF NOT EXISTS railway_system.train_routes (
	row_id SERIAL PRIMARY KEY,
	route_id TEXT,
	train_id TEXT REFERENCES railway_system.train_details (train_id),
    station_id TEXT REFERENCES railway_system.stations (station_id),
	order_number INT,
	halt_duration_minutes INT,
	estimated_arrival TIME,
	estimated_departure TIME
);


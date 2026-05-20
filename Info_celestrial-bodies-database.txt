Instructions

For this project, you need to log in to PostgreSQL with psql to create your database. Do that by entering psql --username=freecodecamp --dbname=postgres in the terminal. Make all the tests below pass to complete the project. Be sure to get creative, and have fun!

Don't forget to connect to your database after you create it 😄

Here's some ideas for other column and table names: description, has_life, is_spherical, age_in_millions_of_years, planet_types, galaxy_types, distance_from_earth.

Notes:
If you leave your virtual machine, your database may not be saved. You can make a dump of it by entering pg_dump -cC --inserts -U freecodecamp universe > universe.sql in a bash terminal (not the psql one). It will save the commands to rebuild your database in universe.sql. The file will be located where the command was entered. If it's anything inside the project folder, the file will be saved in the VM. You can rebuild the database by entering psql -U postgres < universe.sql in a terminal where the .sql file is.

If you are saving your progress on freeCodeCamp.org, after getting all the tests to pass, follow the instructions above to save a dump of your database. Save the universe.sql file in a public repository and submit the URL to it on freeCodeCamp.org.


Complete the tasks below

    You should create a database named universe

    Be sure to connect to your database with \c universe. Then, you should add tables named galaxy, star, planet, and moon

    Each table should have a primary key

    Each primary key should automatically increment

    Each table should have a name column

    You should use the INT data type for at least two columns that are not a primary or foreign key

    You should use the NUMERIC data type at least once

    You should use the TEXT data type at least once

    You should use the BOOLEAN data type on at least two columns

    Each "star" should have a foreign key that references one of the rows in galaxy

    Each "planet" should have a foreign key that references one of the rows in star

    Each "moon" should have a foreign key that references one of the rows in planet

    Your database should have at least five tables

    Each table should have at least three rows

    The galaxy and star tables should each have at least six rows

    The planet table should have at least 12 rows

    The moon table should have at least 20 rows

    Each table should have at least three columns

    The galaxy, star, planet, and moon tables should each have at least five columns

    At least two columns per table should not accept NULL values

    At least one column from each table should be required to be UNIQUE

    All columns named name should be of type VARCHAR

    Each primary key column should follow the naming convention table_name_id. For example, the moon table should have a primary key column named moon_id

    Each foreign key column should have the same name as the column it is referencing

    psql --username=freecodecamp --dbname=postgres

    CREATE DATABASE universe;

    \c universe

    CREATE TABLE galaxy (
    galaxy_id SERIAL PRIMARY KEY,
    name VARCHAR (50) UNIQUE NOT NULL,
    size NUMERIC NOT NULL,
    colonized BOOLEAN NOT NULL,
    info TEXT
    );

    CREATE TABLE star (
    star_id SERIAL PRIMARY KEY,
    galaxy_id INT NOT NULL REFERENCES galaxy(galaxy_id),
    name VARCHAR (50) UNIQUE NOT NULL,
    size NUMERIC NOT NULL,
    missions INT,
    colonized BOOLEAN NOT NULL
    );

    CREATE TABLE planet (
    planet_id SERIAL PRIMARY KEY,
    star_id INT NOT NULL REFERENCES star(star_id),
    name VARCHAR (50) UNIQUE NOT NULL,
    size NUMERIC NOT NULL,
    story TEXT,
    missions INT,
    colonized BOOLEAN NOT NULL
    );

    CREATE TABLE moon (
    moon_id SERIAL PRIMARY KEY,
    planet_id INT NOT NULL REFERENCES planet(planet_id),
    name VARCHAR (50) UNIQUE NOT NULL,
    size NUMERIC NOT NULL,
    story TEXT,
    missions INT,
    colonized BOOLEAN NOT NULL
    );

    CREATE TABLE species(
    species_id SERIAL PRIMARY KEY,
    name VARCHAR (100) UNIQUE NOT NULL,
    info TEXT,
    size NUMERIC
    );

INSERT INTO galaxy (name, size, colonized, info)
VALUES
('Milky Way', 100000, true, 'Home galaxy of humanity'),
('Andromeda', 220000, false, 'Nearest major galaxy to the Milky Way'),
('Triangulum', 60000, false, 'Small spiral galaxy in the Local Group'),
('Whirlpool', 76000, true, 'Known for intense star formation'),
('Sombrero', 50000, false, 'Galaxy with a bright central bulge'),
('Cartwheel', 150000, false, 'Ring galaxy formed by collision');

INSERT INTO star (name, size, missions, colonized, galaxy_id)
VALUES
('Sun', 1391000, 25, true, 1),
('Proxima Centauri', 200000, 5, false, 1),
('Sirius', 2400000, 8, false, 1),
('Betelgeuse', 1200000000, 2, false, 1),
('Rigel', 97000000, 1, false, 2),
('Vega', 3400000, 4, true, 3);

INSERT INTO planet (name, size, missions, colonized, star_id)
VALUES
('Mercury', 4879, 3, false, 1),
('Venus', 12104, 6, false, 1),
('Earth', 12742, 50, true, 1),
('Mars', 6779, 40, true, 1),
('Jupiter', 139820, 12, false, 1),
('Saturn', 116460, 8, false, 1),
('Neptune', 49244, 2, false, 1),
('Proxima b', 12000, 1, false, 2),
('Sirius Prime', 18000, 3, true, 3),
('Rigel IV', 22000, 0, false, 5),
('Vega Terra', 14000, 5, true, 6),
('Betel IX', 30000, 1, false, 4);

INSERT INTO moon (name, size, missions, colonized, planet_id)
VALUES
('Moon', 3474, 20, true, 3),
('Phobos', 22, 5, false, 4),
('Deimos', 12, 3, false, 4),
('Io', 3643, 4, false, 5),
('Europa', 3122, 10, true, 5),
('Ganymede', 5268, 6, false, 5),
('Callisto', 4821, 2, false, 5),
('Titan', 5150, 9, true, 6),
('Enceladus', 504, 4, false, 6),
('Mimas', 396, 1, false, 6),
('Triton', 2706, 2, false, 7),
('Nereid', 340, 0, false, 7),
('Luna-X', 4100, 2, true, 8),
('Sirius Moon I', 2000, 1, false, 9),
('Sirius Moon II', 1800, 1, false, 9),
('Rigel Rock', 900, 0, false, 10),
('Vega Moon Alpha', 3200, 3, true, 11),
('Vega Moon Beta', 2500, 2, false, 11),
('Betel Minor', 1500, 0, false, 12),
('Betel Major', 4500, 1, false, 12);

INSERT INTO species (name, info, size)
VALUES
('Humans', 'Advanced technological civilization from Earth', 8),
('Martians', 'Colonists adapted to Martian conditions', 7),
('Europans', 'Aquatic intelligent life beneath Europa ice', 6),
('Titanians', 'Methane-based lifeforms from Titan', 5),
('Vegans', 'Highly advanced species from Vega Terra', 9),
('Rigelians', 'Nomadic species from Rigel system', 7);

ALTER TABLE star
ADD CONSTRAINT fk_star_galaxy
FOREIGN KEY (galaxy_id)
REFERENCES galaxy(galaxy_id);

ALTER TABLE planet
ADD CONSTRAINT fk_planet_star
FOREIGN KEY (star_id)
REFERENCES star(star_id);

ALTER TABLE moon
ADD CONSTRAINT fk_moon_planet
FOREIGN KEY (planet_id)
REFERENCES planet(planet_id);





# transit-evaluator
Transit Evaluator (TE) is a simple project that utilizes the Google Maps API to calculate the time efficiency of a given city. The user inputs a city of their choosing, and TE returns time-based statistics about that city's bus system.

## Usage
TE requires a valid Google Maps API key. You can obtain one by checking [the official Google Maps API page.](https://developers.google.com/maps) The API key is saved to `key.txt` in the same folder that the program is located.

TE is run by entering:
```
python transit-evaluator
```

Once run, the user will be prompted to enter a city, as well as the number of instances. The number of instances determines the accuracy of TE's calculation; a higher number is more accurate. After the program finishes, it will record the city's transit efficiency score as well as relevant statistics to a local text file.

## How it works
TE works through a series of steps:
1. TE uses Google Maps' Geocoding API to obtain the boundaries of given city, represented as a square.
2. TE then creates a series of random paths within that boundaries. The number of paths is based off the number of instances given by the user.
3. After this, TE then uses the Distance Matrix API to calculate both the driving time and bus time of each generated path. TE then determines an **"efficiency score"** by dividing the driving time by the bus time.
4. TE finishes by averaging out the "efficiency scores" of each generated route. A higher efficiency score represents that the given city has a more time-efficient bus system (ex. a score of 0.2 would indicate that travelling by bus is 5 times slower than by car).
5. In addition, TE also returns a **"transit prevalence"** score, determined by how many bus routes could succesfully be calculated by the Distance Matrix API. This score gives some interesting insights into how prevalent and concentrated public transportation is within a given city.

## Results
To test the program, I input the 10 most populated cities in the US. In addition, I tested the five best and worst public transit systems rated in [a study by WalletHub,](https://wallethub.com/edu/cities-with-the-best-worst-public-transportation/65028) using their "Accessibility and Convenience" rank. (For fun, I also put in my hometown of Edwardsville, IL, whose less-than-stellar transit system inspired the creation of this project.)

![Transit Efficiency-1](https://user-images.githubusercontent.com/88009946/127079663-16c5483f-5581-41f2-b550-678403bc5f46.jpg)

(cities in blue are those ranked the five most accessible transit systems by WalletHub; cities in red are those ranked the worst)

The Transit Prevelance score in particular is rather interesting, as it gives insight into the structural development of the city itself. Many of the cities with a poor prevelance score have transit systems that are concentrated in population-dense areas, whereas high prevelance score cities have more spread-out systems.

## Weaknesses
TE's biggest weakness is its methodology. TE generates and tests paths on a purely random basis, agnostic to any demographic data. In other words, it's possible for a path generated to be between, for example, an abandoned waterpark and an old shack in the outskirts of town. TE's results, therefore, are somewhat pessimistic, as cities' transit systems are often strategically concentrated in high-volume areas rather than mindlessly spread out.

TE is also my first programming project, and as such, there are likely many instances of inefficient code in the program. I'd be happy to look back and revise some things when I get the chance.

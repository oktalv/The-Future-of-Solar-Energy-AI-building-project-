# The future of solar energy 
Final project for the Building AI course



## Summary

One of the biggest concerns of the 21st century is the source of energy. As fossil fuels are predicted to be completely used up in close future, more thoughts are being directed to reusable sources or energy, such as solar energy.
More and more solar panels are being implemented on roofs all around the world. But they are still quite unpopular. Is it because their efficiency isn't yet on high enough level, or because cost of their implementation is too high, or maybe it is just because it is not presented to customers in the right way. Most likely it is all of the 3 reasons combined together, but this idea tends to improve 3rd part - presentation of solar panels to wider public.
Wouldn't it be nice if anyone could just open a web site, or download a smart phone app, where a Google earths map appears. The person then just have to find their house in the Google earth, click on their house and following results appear: 
1) Cost of implementation of solar panels for your roof is: xxx.xx [$]. 
2) Years for this implementation to pay off is: xx.x [years].

If companies which sell solar panel had this system, much more people would have been interested in it. You wouldn't have to call their services to come to your house with their flying drones to record your roof and backyard and give you hours-long presentations how you should get those solar panels implemented on your roof. Instead, within just a few minutes you can do the most important part by yourself. Getting the cost of implementation and expected years for that implementation to pay off.

## Background

This idea solves the 'unpopularity of solar panels' problem. Problem is quite frequent as solar panels are going to be implemented on more and more rooftops in the future but they are still not available to wide enough public yet.
I was personally motivated for this idea because I would like to have solar panels implemented on my own roof. But they seem to be so unapproachable. This topic is important and interesting as it will not only help individuals with their budgets, but as well use the natural sources of energy which will help restore Earths healthy environment.



## How is it used?


Companies which sell and implement solar panels should partner up with Google to have the access to their high resolution satellite images. Once they have access to those images 90% of work is already done! Now it is only needed to calculate cost of implementation and years to pay off (the energy you're receiving through solar panels, converted to money, should be greater than the cost of implementation in some amount of years.)

Cost of implementation may depend on various number of factors. In this idea factors are following:
1) roof's surface - the bigger the surface the more solar panels can be installed, hence, cost is bigger.
2) angle of the roof - extremely steep roofs may result with different kind of problems during installation of solar panels.
3) production of solar panels (production_cost) - companies have their own costs when producing solar panels and this should be a constant.
Having the cost of implementation's factors listed, cost of the implementation can be calculated using linear regression with the following equation:

cost_of_implementaion = production_cost + k1 * roof's surface + k2 * roof_angle

In which k1, k2 are precaluclated coefficients.
For example, real life example could be the following:

cost_of_implementaion = 1 000 + 100 * 30 + 80 * 70
                      = 4 500 $

In the equation '1000' stands for cost of production of solar panels in dollars. '30' stands for roof's surface in square metres (notice that each square metre adds  100 dollars to the total cost of implementation. '70' is roof's angle in degrees (note that roof at 70 degrees adds up to 1500 dollars in total cost, while flat roofs don't add up any additional cost).
The total cost of implementation for a rooftop with 30 square metres and 70 degrees roof angle is 4 500 dollars

Second, probably most important variable is Years to pay off. It calculates how many years are needed to pass so that the customer is in plus. Meaning energy that he receives through panels on its roof over years, converted to money, should be greater than the cost of the implementation calculated above.

Years to pay off may depend on various number of factors. In this idea factors are following:
1) cost of implementation - the higher the cost of the implementation, more years are needed to pass.
2) noise - noise are all the negative factors combined together. Noise could be high mountain, tree, building next to the house which drop shadow on the solar panels and causes their efficiency to drop.
3) sunny days - efficiency of solar panels depends on sunny days for that city. Sunny days are usually calculated as average of sunny days through one year for that city.
4) roof's surface - this factor was also used in cost of implementation variable (as bigger the surface the more panels can fit on roof), but is also a vital factor for years to pay off, as bigger surfaces lead to larger energy income.
5) roof's angle - this factor was also used in cost of implementation, but again is a vital factor for years to pay off, as the angle of roof determines the amount of sun's rays which fall on the panels. I am not sure what is the most efficient angle as I do not work for solar panels companies, but we can take a guess and say ideal angle is 45 degrees.
6) roof's direction - this is meant as in which direction roof is pointing at. Roofs pointing to do South will probably be more efficient than those pointing to the North or West. In the equation below South will have the value of 1, East and West value of 0.8 and North the value of 0.6.
7) Earth's latitude - countries closer to the equator line have bigger efficiency from solar panels than northern countries (or southern countries on south hemisphere). 

Having the factors listed we can now make the equation using linear regression again:

years_to_pay_off = c1 * cost_of_implementation + c2 * noise - c3 * sunny_days - c4 * roofs_angle - c5 * roofs_direction - c6 * earths_latitude - c7 * roofs_surface.

In which c1-c7 are coefficients.
Notice that cost_of_implementation and noise have positive values as they increase number of years to pay off, while the rest have negative value and they are decreasing it. Our goal is to have years to pay off as close to zero, of course.
In a practical example equation could look like this:

years_to_pay_off = 0.006 * 4500 + 0.1 * 10 - 0.005 * 200 - 0.7 * (1 / abs(45.5 - 70)) - 2 * 0.6 - 50 * (1/ 45) - 0.05 * 30
                 = 27 + 1 - 1 - 0.029 - 1.2 - 1.111 - 1.5
                 = 23.16 years
                 
From the equation above we can see that cost of implementation adds up 27 years to pay off, noise adds up 1 year, 200 sunny days per year removes 1 year, roof at angle of 70 degrees removes 0.028 years (abs in the equation means that 35 degrees roof's angle is same as 55 degrees angle, while the best efficiency is at 45 and 46 degrees), roof pointing to the North (that's why value is 0.6) removes 1.2 years (if it was pointing to the South it would have been removing 2 years), countries located at 45 degrees Earth's latitude, such as central Europe, USA, China removes 1.11 years (while those at 60 degrees, such as Finland, Norway, remove only 0.76 years), and finally roofs surface of 30 square metres removes 1.5 years.

To sum up if a person who has a roof top of 30 square metres, roof angel at 70 degrees, roof's direction pointing to the North, house at longitude of 45 degrees and the average sunny days 200, clicks on his house on the website (or smartphone app) gets the following outcome:
Cost of implementation of solar panels for your house is 4500 $. It will take you 23.16 years to return the money just from these panels.
Smaller house in the mountains in Italy with steep roof could have similar parameters to those mentioned.



## Data sources and AI methods

Data is received from Google and its satellite images to have an access to roof's surface, roof's direction and latitude.
Angle of the roof may be hard to be seen just from satellite images, but it is possible to get it from Google cars (or whichever methods Google is using for 3d mapping).
Number of sunny days could be received from meteorological institutions.
AI methods used for this would be linear regression as mentioned in above examples. For calculations of cost of implementation and years to pay off maybe even more suitable method would be 'Nearest neighbour' method, in which training data would be already built solar panels in previous years, with known cost of implementation and years to pay off. New roofs would get the same results as the roof with the most similar angle/surface/direction/latitude/noise..
There would be many other AI methods needed to register rooftops from the satellite images and take them to the calculations. As well as for roof's angle and direction.


## Challenges

Challenges this idea is facing is Google's openness for cooperation with solar panel companies and possible law suits by customers because years to pay off in real were greater than what was estimated by website. (Although those results should be estimated numbers with +/- 20 % error).
In this description of this idea not everything was explained. For instance, roof's surface has been considered as in whole, while there are sometimes windows on the rooftops, as well as chimneys, which result in some part of roof being unavailable for implementation of solar panels. Noise factor, such as trees, should also be discussed deeper, as trees are ought to be cut down within longer period of years.
The coefficients and numbers in this work are made up numbers which haven't been tested on many examples yet. They were used just for the understanding of how this idea would work and have a long way to go to make bigger sense.
Another thing is that we discussed rooftops being covered with solar panels to the absolute limit. In real, customers most often do not want their whole roof covered with solar panels, but only want to implement 1 or some other smaller number of panels. Final version of this project should definitely have this option.


## What next?

This project needs few years of further researching and testing with experts to make it a real thing.
But what it needs the most is reviews and critics from anyone at the beginning to even stand a chance of becoming real one day.



## Creator of the idea

Vlatko Dvojkovic



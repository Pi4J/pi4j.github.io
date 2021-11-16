---
title: 'Cocktail Maker'
weight: 65
---

### Project description 

The CocktailMaker is a cocktail mixing machine by [Alexander Liggesmeyer](https://alexander.liggesmeyer.net/). It can 
control as many pumps as the RaspberryPi provides GPIO pins. For every pump that gets added to the system, the user has 
to provide the amount of time that that pump needs to pump one centiliter in milliseconds. The machine uses peristaltic 
pumps. So that number is perfectly accurate. The flow rate won't vary over time. It uses a relay board for closing the 
electronic circuit for all pumps. This allows to power the pumps with more than 5V. The relay board is connected to the 
Pi which controls the board with Pi4J V1. The backend-application is written in Java (Spring boot). The frontend is 
written with VueJS.

{{< gallery >}}
{{< figure link="/assets/featured-projects/cocktail/cocktailmaker_circuit.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/screen-login.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/screen-cocktail.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100823.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100734.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100717.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100645.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100534.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100457.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/cocktail/20211116_100414.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

[A video is available on Reddit](https://www.reddit.com/r/homeautomation/comments/qsjj04/built_an_automatic_cocktail_machine/)

### Application features

* Pumping ingredients in sequential order.
* Pumping ingredients concurrently and mixing them by spreading the active pump timings within the productionstep.
* Ingredients that cannot be added automatically (maybe because they didn't get assigned to one pump or are simply not liquid) can be handled. If a recipe with a non-pumpable ingredient got ordered the application will prompt the user to add that ingredient at the corresponding point.
* Recipes can be resized for every order. The user decides the size of the cocktail he wants to order. All ingredients amount will get recalculated automatically.
* A drag & drop recipe editor.
* Recipes can be categorized.
* Collections: Users can create collections and add recipes to them.
* Bar: Users can add owned ingredients to their bar. The application can search for recipes that he can order with the owned recipes. If the user tries to order a recipe where he doesn't own all ingredients he will get a warning.
* The cocktail maker can search for recipes that can be produced fully automatic. (Won't require the user to add ingredients manually)
* Recipes can be searched by ingredients.
* Multiple users & permission system: The admin can create new users and assign them to predefined groups, that have different permissions.

### Ideas for the future

The next update will also allow the application to track the remaining amount of liquid of the connected bottles and 
prevent an order if the remaining liquid doesn't reach. It is also able to switch between pumps on the fly. If one order 
empties one bottle, but another bottle with the same ingredient is connected, the application will empty the first 
container and will switch to the second one mid-production. 

### Docker deployment

The whole application can be deployed as a docker container that has to be started in privileged mode. This allows even
beginners that don't have much experience to build their own machine.

### Sources

[The full sources are available on GitHub](https://github.com/alex9849/pi-cocktail-maker)
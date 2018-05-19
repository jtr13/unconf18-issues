# [R in Minecraft, the next generation](https://github.com/ropensci/unconf18/issues/56)

> state: **open** opened by: **revodavid** on: **5/14/2018**

At ROpenSci 2017, a team created the [miner package](https://github.com/ropenscilabs/miner) with R functions to control the Minecraft world. The goal was to provide a framework for young people to learn R, motivated by their desire to automate the construction of objects in Minecraft or to control the world in other way. An accompanying package, [craft](https://github.com/ropenscilabs/craft), was also created with functions to implement some larger-scale projects (for example, an &#x60;elsify&#x60; function to give the player the power Elsa to freeze water behind their feet). A [bookdown book](https://ropenscilabs.github.io/miner_book/) collected these projects into book form.

With a small team and another couple of days, we could get the &#x60;miner&#x60; package ready for CRAN, and add additional examples to &#x60;craft&#x60; and the book. Things we could work on include:

- Cleaning up the API, in particular making location functions more consistent, and using R vectors instead of separate x, z, y arguments
- Making the server connection more robust (right now it tends to disconnect every few minutes)
- Providing a cleaner interface to Minecraft block types
- Creating an up-to-date Docker image for the Spigot server, and simplifying the installation process

The Spigot/RaspberryJuice server is a bit limited too; there&#x27;s no way to change the orientation of the player, for example. We might be able to explore other Minecraft APIs and see if they&#x27;re more suitable for this project.



### Comments

---
> from: [**seaaan**](https://github.com/ropensci/unconf18/issues/56#issuecomment-389322800) on: **5/15/2018**

This sounds fun! If the project I proposed doesn&#x27;t work out I&#x27;d like to work on this. 

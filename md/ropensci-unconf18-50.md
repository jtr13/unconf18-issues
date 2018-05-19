# [color palette aggregator/modifier tool](https://github.com/ropensci/unconf18/issues/50)

> state: **open** opened by: **cstawitz** on: **5/7/2018**

There are loads of packages/ways to choose color palettes for R graphics, but I still end up doing a lot of iterations through many packages until I find a suitable color palette. 

**Existing packages (please add):**
&#x60;colorspace&#x60; has a GUI that makes choosing colors easy with a preview function for different types of plots and a slider for Hue, Chroma, Luminance, and Power, but doesn&#x27;t integrate seamlessly with other color packages. &#x27;RColorBrewer&#x27; [(here)](http://colorbrewer2.org/#type&#x3D;sequential&amp;scheme&#x3D;YlGn&amp;n&#x3D;9) has many palettes but you have to use the &#x60;colorRampPalette()&#x60; function to get more than 9 or 11 colors. &#x60;hues&#x60; allows you to pick palettes with many colors, but requires numeric HCL inputs for colors. There are many great palettes out there (i.e. [Beyonce](http://beyoncepalettes.tumblr.com/) or &#x60;wesanderson&#x60; ) in addition, but checking how your graph looks across palettes from different packages requires loading and knowing the different syntax of each.

**Idea:**
A one-stop-shop for colors in R that combines the best of existing tools.  The goal would be to change the workflow from iterating across multiple packages to find a suitable palette to using one tool that:
1. Aggregates and displays color palettes across packages
2. Allows users to increase/decrease the number of colors in these palettes
3. Pick and choose colors from predefined palettes to create your own custom palette
4. Adds transparency or ensure colorblind-friendly schemes
5. Get immediate previews of what a/your graph would look like when you change any of these options

my colleague Margaret Siple inspired this idea  

 


### Comments

---
> from: [**mpadge**](https://github.com/ropensci/unconf18/issues/50#issuecomment-387212135) on: **5/7/2018**

Great idea! My go-to comprehensive list is [&#x60;r-color-palettes&#x60;](https://github.com/EmilHvitfeldt/r-color-palettes), but it&#x27;s neither interactive, nor does it quantify how many colours are available. A more interactive tool would be fantastic.
---
> from: [**jtr13**](https://github.com/ropensci/unconf18/issues/50#issuecomment-387213439) on: **5/7/2018**

Love the focus on color vision deficiency (CVD) friendliness
---
> from: [**OmaymaS**](https://github.com/ropensci/unconf18/issues/50#issuecomment-387316739) on: **5/8/2018**

The options and interactivity reminds me of [colorbrewer2.org](http://colorbrewer2.org/#type&#x3D;sequential&amp;scheme&#x3D;BuGn&amp;n&#x3D;3). It helps picking a palette taking in consideration the given criteria.
---
> from: [**cstawitz**](https://github.com/ropensci/unconf18/issues/50#issuecomment-389700987) on: **5/16/2018**

**Summary:** an interactive application that aggregates color palettes, allows users to choose and combine palette colors, preview and iterate easily, and makes transparency and CVD friendliness a one-click step. Doesn&#x27;t require manually loading or learning syntax of existing palette solutions.

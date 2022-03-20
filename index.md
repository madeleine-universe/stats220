# **Introducing my very first meme created with the all mighty R**

![](my_first_meme.png)


I have never created a meme before and wanted to my very first meme to have the following attributes:
<!--- unordered lists --->
* embodied my infant meme maker status
* showed my appreciation for learning these new image transformation skills in R
* original in essence

I wanted to just put text over an image but it didn't look great while meeting the requirements. *I did make something pretty basic in the beginning*. But as my ideas evolved and I become more comfortable with the way the *magick* package worked, I came up with this three layer baby meme with a small captioned box. To be fair, the image does look more impressive without the whiten removal but I was **SO** impressed with this skill I had to leave it and really show how these functions have shined a light on the power of *R*

The first layer can be found on [stockphoto.com](https://stockphoto.com) [here](https://stockphoto.com/assets/landingpage/images/Depositphotos_62550077_original.jpg).   The transparent sun can be found [here](https://cdn.pixabay.com/photo/2017/02/19/22/14/sun-2081062_960_720.png) from ![pixbay.com](https://pixabay.com) and many thanks to ![R](https://www.r-project.org) for providing their logo which can be found [here](https://www.r-project.org/Rlogo.png) here

## Original Images
![baby](https://stockphoto.com/assets/landingpage/images/Depositphotos_62550077_original.jpg) 
![sun](https://cdn.pixabay.com/photo/2017/02/19/22/14/sun-2081062_960_720.png)
![rlogo](https://www.r-project.org/Rlogo.png)

### R Code
```r
## create text box

babyblank <- image_blank(width = 250, height = 50, color="#0099ff") %>%
  image_annotate(text = "Bathing in the Power of R",
                 color = "#FFFFFF",
                 size = 18,
                 font = "Comic Sans",
                 gravity = "center")
                 
## create 1st layer and whiten sun background
babymeme <- image_read("https://stockphoto.com/assets/landingpage/images/Depositphotos_62550077_original.jpg") %>% image_scale(250)
babyfill <-image_fill(babymeme, "white", point = "+10+5", fuzz = 10)

##create 2nd layer and crop bottom right corner of sun
sun <- image_read("https://cdn.pixabay.com/photo/2017/02/19/22/14/sun-2081062_960_720.png")
sunflop <-image_flop(sun) %>% image_scale(240)
suncrop <- image_crop(sunflop, "200x200+100+100")

##create 3rd layer and change hue to become yellow
logo <- image_read("https://www.r-project.org/Rlogo.png") %>% image_scale(50) %>% image_modulate(hue = 10)

##get layers ready for append and finish!
sunvector <- c(babyfill,suncrop,logo)
flatsun <- image_flatten(sunvector)
flatblank <- image_flatten(babyblank)
flatx <- c(flatsun,flatblank)
babymemefinal <- image_append(flatx, stack = TRUE)
image_write(babymemefinal,"my_first_meme.png")


```

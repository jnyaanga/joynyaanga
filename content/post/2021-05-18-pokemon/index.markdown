---
title: ggPlot 'Em All!
author: Joy Nyaanga
date: '2021-05-18'
slug: pokemon
categories:
  - R
  - fun programming
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-05-18T18:33:48-05:00'
featured: no
image:
  caption: '[Photo by Thimo Pedersen on Unsplash](https://unsplash.com/photos/dip9IIwUK6w)'
  focal_point: ''
  preview_only: no
projects: []
---
<link href="{{< blogdown/postref >}}index_files/pagedtable/css/pagedtable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/pagedtable/js/pagedtable.js"></script>


I've been looking for ways to apply the R tools I use to **fun** data outside my research, so when I happened to stumble across the [Pokémon dataset](https://www.kaggle.com/rounakbanik/pokemon) I thought... what better way to dig into some Pokémon stats than with tidyverse!  

This dataset contains a treasure trove of information on 801 Pokémon from all seven generations. Let's see what we're working with:


```r
rmarkdown::paged_table(pokemon[1:6,])
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["name"],"name":[1],"type":["chr"],"align":["left"]},{"label":["generation"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["type1"],"name":[3],"type":["fct"],"align":["left"]},{"label":["type2"],"name":[4],"type":["fct"],"align":["left"]},{"label":["attack"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["sp_attack"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["defense"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["sp_defense"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["speed"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["hp"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["abilities"],"name":[11],"type":["chr"],"align":["left"]},{"label":["against_bug"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["against_dark"],"name":[13],"type":["dbl"],"align":["right"]},{"label":["against_dragon"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["against_electric"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["against_fairy"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["against_fight"],"name":[17],"type":["dbl"],"align":["right"]},{"label":["against_fire"],"name":[18],"type":["dbl"],"align":["right"]},{"label":["against_flying"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["against_ghost"],"name":[20],"type":["dbl"],"align":["right"]},{"label":["against_grass"],"name":[21],"type":["dbl"],"align":["right"]},{"label":["against_ground"],"name":[22],"type":["dbl"],"align":["right"]},{"label":["against_ice"],"name":[23],"type":["dbl"],"align":["right"]},{"label":["against_normal"],"name":[24],"type":["dbl"],"align":["right"]},{"label":["against_poison"],"name":[25],"type":["dbl"],"align":["right"]},{"label":["against_psychic"],"name":[26],"type":["dbl"],"align":["right"]},{"label":["against_rock"],"name":[27],"type":["dbl"],"align":["right"]},{"label":["against_steel"],"name":[28],"type":["dbl"],"align":["right"]},{"label":["against_water"],"name":[29],"type":["dbl"],"align":["right"]},{"label":["base_egg_steps"],"name":[30],"type":["dbl"],"align":["right"]},{"label":["base_happiness"],"name":[31],"type":["dbl"],"align":["right"]},{"label":["base_total"],"name":[32],"type":["dbl"],"align":["right"]},{"label":["capture_rate"],"name":[33],"type":["chr"],"align":["left"]},{"label":["classfication"],"name":[34],"type":["chr"],"align":["left"]},{"label":["experience_growth"],"name":[35],"type":["dbl"],"align":["right"]},{"label":["height_m"],"name":[36],"type":["dbl"],"align":["right"]},{"label":["japanese_name"],"name":[37],"type":["chr"],"align":["left"]},{"label":["percentage_male"],"name":[38],"type":["dbl"],"align":["right"]},{"label":["pokedex_number"],"name":[39],"type":["dbl"],"align":["right"]},{"label":["weight_kg"],"name":[40],"type":["dbl"],"align":["right"]},{"label":["is_legendary"],"name":[41],"type":["lgl"],"align":["right"]},{"label":["n"],"name":[42],"type":["int"],"align":["right"]}],"data":[{"1":"Bulbasaur","2":"1","3":"grass","4":"poison","5":"49","6":"65","7":"49","8":"65","9":"45","10":"45","11":"['Overgrow', 'Chlorophyll']","12":"1.00","13":"1","14":"1","15":"0.5","16":"0.5","17":"0.5","18":"2.0","19":"2","20":"1","21":"0.25","22":"1","23":"2.0","24":"1","25":"1","26":"2","27":"1","28":"1.0","29":"0.5","30":"5120","31":"70","32":"318","33":"45","34":"Seed Pokémon","35":"1059860","36":"0.7","37":"Fushigidaneフシギダネ","38":"88.1","39":"1","40":"6.9","41":"FALSE","42":"78"},{"1":"Ivysaur","2":"1","3":"grass","4":"poison","5":"62","6":"80","7":"63","8":"80","9":"60","10":"60","11":"['Overgrow', 'Chlorophyll']","12":"1.00","13":"1","14":"1","15":"0.5","16":"0.5","17":"0.5","18":"2.0","19":"2","20":"1","21":"0.25","22":"1","23":"2.0","24":"1","25":"1","26":"2","27":"1","28":"1.0","29":"0.5","30":"5120","31":"70","32":"405","33":"45","34":"Seed Pokémon","35":"1059860","36":"1.0","37":"Fushigisouフシギソウ","38":"88.1","39":"2","40":"13.0","41":"FALSE","42":"78"},{"1":"Venusaur","2":"1","3":"grass","4":"poison","5":"100","6":"122","7":"123","8":"120","9":"80","10":"80","11":"['Overgrow', 'Chlorophyll']","12":"1.00","13":"1","14":"1","15":"0.5","16":"0.5","17":"0.5","18":"2.0","19":"2","20":"1","21":"0.25","22":"1","23":"2.0","24":"1","25":"1","26":"2","27":"1","28":"1.0","29":"0.5","30":"5120","31":"70","32":"625","33":"45","34":"Seed Pokémon","35":"1059860","36":"2.0","37":"Fushigibanaフシギバナ","38":"88.1","39":"3","40":"100.0","41":"FALSE","42":"78"},{"1":"Charmander","2":"1","3":"fire","4":"NA","5":"52","6":"60","7":"43","8":"50","9":"65","10":"39","11":"['Blaze', 'Solar Power']","12":"0.50","13":"1","14":"1","15":"1.0","16":"0.5","17":"1.0","18":"0.5","19":"1","20":"1","21":"0.50","22":"2","23":"0.5","24":"1","25":"1","26":"1","27":"2","28":"0.5","29":"2.0","30":"5120","31":"70","32":"309","33":"45","34":"Lizard Pokémon","35":"1059860","36":"0.6","37":"Hitokageヒトカゲ","38":"88.1","39":"4","40":"8.5","41":"FALSE","42":"52"},{"1":"Charmeleon","2":"1","3":"fire","4":"NA","5":"64","6":"80","7":"58","8":"65","9":"80","10":"58","11":"['Blaze', 'Solar Power']","12":"0.50","13":"1","14":"1","15":"1.0","16":"0.5","17":"1.0","18":"0.5","19":"1","20":"1","21":"0.50","22":"2","23":"0.5","24":"1","25":"1","26":"1","27":"2","28":"0.5","29":"2.0","30":"5120","31":"70","32":"405","33":"45","34":"Flame Pokémon","35":"1059860","36":"1.1","37":"Lizardoリザード","38":"88.1","39":"5","40":"19.0","41":"FALSE","42":"52"},{"1":"Charizard","2":"1","3":"fire","4":"flying","5":"104","6":"159","7":"78","8":"115","9":"100","10":"78","11":"['Blaze', 'Solar Power']","12":"0.25","13":"1","14":"1","15":"2.0","16":"0.5","17":"0.5","18":"0.5","19":"1","20":"1","21":"0.25","22":"0","23":"1.0","24":"1","25":"1","26":"1","27":"4","28":"0.5","29":"2.0","30":"5120","31":"70","32":"634","33":"45","34":"Flame Pokémon","35":"1059860","36":"1.7","37":"Lizardonリザードン","38":"88.1","39":"6","40":"90.5","41":"FALSE","42":"52"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

Now the ever challenging question of where to begin?? First I'll plot the frequency of each type:


```r
pokemon %>%
  ggplot() +
  aes(y = reorder(type1, n)) +
  geom_bar(fill = "darkblue") +
  scale_x_continuous(breaks = seq(0,120,5)) +
  theme_bw() + labs(y = "Pokémon Type")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />
Neat - the most common Pokémon type is water while the least common is flying. This, however, combines information about *Legendary Pokémon*. Legendary Pokémon are a group of incredibly rare and powerful Pokémon. But just how rare are they?


```r
pokemon %>% 
  dplyr::count(is_legendary) %>% 
  dplyr::mutate(prop = n/sum(n)) %>%
  knitr::kable()
```



|is_legendary |   n|      prop|
|:------------|---:|---------:|
|FALSE        | 731| 0.9126092|
|TRUE         |  70| 0.0873908|
Looks like there are only 70 legendaries out of 801 Pokémon - quite the minority at only ~9% of the population.  

Now to explore some characteristics. First I'll plot the relationship between height and weight while highlighting Pokémon classified as legendary. 


```r
pokemon %>% 
  ggplot(aes(x = height_m, y = weight_kg)) +
  geom_point(aes(color = is_legendary), size = 2) +
  geom_text(aes(label = ifelse(height_m>7.5|weight_kg>600, as.character(name), '')), 
            vjust = 0, hjust = 0) +
  geom_smooth(method = "lm", se = FALSE, col = "black", linetype = "dashed") +
  expand_limits(x=16) +
  labs(title = "Legendary Pokémon by height and weight",
       x = "Height (m)",
       y = "Weight (kg)") +
  guides(color = guide_legend(title = "Pokémon status")) +
  scale_color_manual(labels = c("Non-Legendary", "Legendary"),
                     values = c("#0072B2", "#D55E00")) +
  theme_bw()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />
It looks like, generally, legendary Pokémon are heavier and taller *but* there are still some exceptions. Onix, Steelix, and Wailord are not legendary status yet are still rather large. I wonder if this trend is maintained across other characteristics. 

```r
pokemon %>% 
  select(is_legendary, attack, sp_attack, defense, sp_defense, hp, speed)  %>% 
  gather(key = fght_stats, value = value, -is_legendary) %>%
  ggplot() +
  aes(x = is_legendary, y = value, fill = is_legendary) +
  geom_boxplot(varwidth = T) +
  facet_wrap(~fght_stats, nrow = 2) +
  scale_fill_manual(labels = c("Non-Legendary", "Legendary"),
                     values = c("#0072B2", "#D55E00")) +
  labs(title = "Pokemon fight statistics",
        x = "Legendary status") +
 guides(fill = FALSE) + theme_bw()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />
  
Not surprisingly, legendary Pokémon outperform their ordinary counterparts in fighting stats. However, there are outliers in both groups indicating some ordinary Pokémon are anomalously strong while some legendaries are anomalously weak.  

The last thing I will do is build a classification tree to understand what makes a Pokémon legendary. I just recently was introduced to working with tree-based models in R thanks to [this DataCamp course](https://learn.datacamp.com/courses/tree-based-models-in-r).  

First, I will split the data into a training set and a test set.

```r
set.seed(5525)

n <- nrow(pokemon)

sample_rows <- sample(n, (0.6*n))

pokemon_train <- pokemon  %>% 
  filter(row_number() %in% sample_rows)

pokemon_test <- pokemon  %>% 
  filter(!row_number() %in% sample_rows)
```

Now I will fit a simple classification decision tree. This will give me a graphical representation of the model.  


```r
set.seed(5525)

model_tree <- rpart(is_legendary ~ attack + defense + height_m + 
                    hp + sp_attack + sp_defense + speed + type1 + type2 + weight_kg,
                       data = pokemon,
                       method = "class",
                       na.action = na.omit)

rpart.plot(model_tree)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />
You will notice several nodes in the tree. Each node shows the predicted class (legendary vs non-legendary) as TRUE or FALSE. It also shows the probability of being legendary and below that, the percentage of Pokémon that are in that node. Take the bottom right node for example  - those Pokémon with a height_m > 2.9 and hp > 99 - this represents only 3% of Pokémon in the training set and predicts that each has a 100% chance of being legendary.  

On the other hand, the bottom-left node (height_m < 2.9, sp_attack < 188, and speed < 99) represents 73% of Pokémon in the training set and predicts that each only has a 2% chance of being legendary.  

Decision trees exclude any variables they don't find to be useful and place the remaining most important variables at the top. So in this case, height_m occupies node 1 while defense, sp_defense, weight_kg, and type1 are all excluded.  

I had a pretty fun time taking a break from my typical data analysis to dig into this fun dataset a bit. If you want to try out something like this check out the [project page on DataCamp](https://learn.datacamp.com/projects/712)! 




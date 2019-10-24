Constitución Abierta: Una Nueva Constitución Para Chile
================

**EN DESARROLLO**

Ejercicio iniciado a partir de [Datos de Miércoles](https://github.com/cienciadedatos/datos-de-miercoles/tree/master/datos/2019/2019-10-23)

``` r
library(tidyverse)
library(ggplot2)
```

``` r
conceptos <- get(load("datos/01-conceptos.rdata")) %>% 
  mutate(
    acuerdo = recode(acuerdo,
      ":Acuerdo" = "Acuerdo",
      ":Acuerdo Parcial" = "Acuerdo Parcial"
      )
    )

memoria <- get(load("datos/02-memoria.rdata"))
```

``` r
conceptos %>% 
  group_by(acuerdo) %>% 
  tally()
```

    ## # A tibble: 3 x 2
    ##   acuerdo              n
    ##   <chr>            <int>
    ## 1 Acuerdo         209851
    ## 2 Acuerdo Parcial  19349
    ## 3 Desacuerdo        1666

``` r
conceptos %>% 
  filter(acuerdo == "Acuerdo") %>% 
  count(concepto, sort = TRUE) %>% 
  top_n(10)
```

    ## # A tibble: 10 x 2
    ##    concepto                                                               n
    ##    <chr>                                                              <int>
    ##  1 Protección, promoción y respeto de los derechos humanos y fundame~  6701
    ##  2 Deberes de protección de conservación de la naturaleza              6355
    ##  3 A la salud                                                          6145
    ##  4 A la educación                                                      5835
    ##  5 Plebiscitos, referendos y consultas                                 5602
    ##  6 Igualdad                                                            5334
    ##  7 Respeto por la constitución                                         5093
    ##  8 De protección y conservación de patrimonio histórico y cultural     4958
    ##  9 Respeto de derechos de otros                                        4850
    ## 10 Justicia                                                            4361

``` r
conceptos %>% 
  filter(acuerdo == "Desacuerdo") %>% 
  count(concepto, sort = TRUE) %>% 
  top_n(10)
```

    ## # A tibble: 12 x 2
    ##    concepto                                                             n
    ##    <chr>                                                            <int>
    ##  1 Régimen de gobierno presidencial/semi-presidencial/parlamentario    84
    ##  2 Forma de Estado: federalismo/autonomías regionales                  69
    ##  3 Fuerzas Armadas                                                     64
    ##  4 Congreso o parlamento (estructura y funciones)                      60
    ##  5 A la vida                                                           57
    ##  6 Cumplimiento de las leyes y normas                                  40
    ##  7 Igualdad                                                            37
    ##  8 Cumplimiento de tratados y obligaciones internacionales             27
    ##  9 Presidencia de la República                                         26
    ## 10 Respeto por la constitución                                         26
    ## 11 Servicio a la comunidad                                             26
    ## 12 Subsidiaridad                                                       26

``` r
conceptos %>% 
  filter(acuerdo == "Acuerdo") %>% 
  group_by(region) %>% 
  count(concepto, sort = TRUE) %>% 
  top_n(10) %>% 
  ungroup() %>% 
  ggplot(aes(concepto, n)) +
  geom_col() +
  coord_flip() +
  facet_wrap(~region, scales = "free")
```

![](AnalisisCabildos_files/figure-markdown_github/unnamed-chunk-5-1.png)

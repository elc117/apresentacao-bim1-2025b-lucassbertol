# Prática aula 8
## Questão 01
-- REESCREVA este código usando where
~~~haskell
calcDistance :: Double -> Double -> Double -> Double -> Double
calcDistance lat1 lon1 lat2 lon2 = 
    let r = 6371.0 -- Earth's radius in km
        dLat = (lat2 - lat1) * pi / 180.0
        dLon = (lon2 - lon1) * pi / 180.0
        a = sin (dLat / 2.0) * sin (dLat / 2.0) +
            cos (lat1 * pi / 180.0) * cos (lat2 * pi / 180.0) *
            sin (dLon / 2.0) * sin (dLon / 2.0)
        c = 2.0 * atan2 (sqrt a) (sqrt (1.0 - a))
    in r * c
~~~

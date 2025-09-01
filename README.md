# PRÁTICA AULA 8
# Questão 1
➡️ REESCREVA este código usando where
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

➡️ O 'where' permite definir variáveis e funções auxiliares APÓS a expressão principal;

➡️ Semelhante a "onde 'x' = ..." em matemática.

~~~haskell
calcDistance :: Double -> Double -> Double -> Double -> Double
calcDistance lat1 lon1 lat2 lon2 = r * c
  where
    r = 6371.0 -- Earth's radius in km
    dLat = (lat2 - lat1) * pi / 180.0
    dLon = (lon2 - lon1) * pi / 180.0
    a = sin (dLat / 2.0) * sin (dLat / 2.0) +
        cos (lat1 * pi / 180.0) * cos (lat2 * pi / 180.0) *
        sin (dLon / 2.0) * sin (dLon / 2.0)
    c = 2.0 * atan2 (sqrt a) (sqrt (1.0 - a))
~~~
➡️ A principal diferença é que com 'where' as definições locais vêm após a expressão principal, deixando o código mais limpo e destacando primeiro o resultado final (r * c)

<img width="1920" height="1080" alt="let" src="https://github.com/user-attachments/assets/d99e7e8c-1840-4c34-942c-3ca568571d18" />

<img width="1920" height="1080" alt="where" src="https://github.com/user-attachments/assets/db6af0bd-9431-4bd0-b3ee-ef602f3f7fdb" />




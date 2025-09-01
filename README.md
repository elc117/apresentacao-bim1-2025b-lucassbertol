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

➡️ O **'where'** permite definir variáveis e funções auxiliares **APÓS** a expressão principal, diferente do **'let'** que vem **ANTES** de uma expressão;

➡️ **'Where'** é semelhante a "onde 'x' = ..." em matemática.

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


*A principal diferença é que com 'where' as definições locais vêm após a expressão principal, deixando o código mais limpo e destacando primeiro o resultado final (r * c)*  

## Comparação de resultados

<img width="1920" height="1080" alt="let" src="https://github.com/user-attachments/assets/d99e7e8c-1840-4c34-942c-3ca568571d18" />\
\
\
<img width="1920" height="1080" alt="where" src="https://github.com/user-attachments/assets/db6af0bd-9431-4bd0-b3ee-ef602f3f7fdb" />

# Questão 2

➡️ Complete a linha abaixo para definir 'distances' como uma nova lista construída a partir de poiList. A nova lista será uma lista de tuplas contendo, para cada POI, seu nome e sua distância até o ponto de referência, dado por givenLat e givenLon.

~~~haskell
  let distances = COMPLETE
  putStrLn "\n==> Distância de cada ponto até o ponto de referência:"
  mapM_ (\(n, d) -> printf "%s: %f\n" n d) distances
~~~

~~~haskell
-- Latitude e longitude de alguns Pontos de Interesse na UFSM
poiList :: [(String, Double, Double)]
poiList = [("Centro de Tecnologia", -29.713318, -53.71663),
           ("Biblioteca Central", -29.71566, -53.71523),
           ("Centro de Convenções", -29.72237, -53.71718),
           ("Planetário", -29.72027, -53.71726),
           ("Reitoria da UFSM", -29.72083, -53.71479),
           ("Restaurante Universitário 2", -29.71400, -53.71937),
           ("HUSM", -29.71368, -53.71536),
           ("Pulsar Incubadora Tecnológica - Prédio 2", -29.71101, -53.71634),
           ("Pulsar Incubadora Tecnológica - Prédio 61H", -29.72468, -53.71335),
           ("Casa do Estudante Universitário - CEU II", -29.71801, -53.71465)]
~~~

## Resoluçao




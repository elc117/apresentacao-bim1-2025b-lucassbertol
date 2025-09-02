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

## Resolução

➡️ O **`where`** permite definir variáveis e funções auxiliares **APÓS** a expressão principal, diferente do **`let`** que vem **ANTES** de uma expressão;

➡️ **`where`** é semelhante a "onde 'x' = ..." em matemática.

➡️ **`let`** é semelhante a "seja 'x' = ..." em matemática.

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


*A principal diferença é que com `where` as definições locais vêm após a expressão principal, deixando o código mais limpo e destacando primeiro o resultado final (r * c)*  

## Comparação de resultados

<img width="1920" height="1080" alt="let" src="https://github.com/user-attachments/assets/d99e7e8c-1840-4c34-942c-3ca568571d18" />\
\
\
<img width="1920" height="1080" alt="where" src="https://github.com/user-attachments/assets/db6af0bd-9431-4bd0-b3ee-ef602f3f7fdb" />

# Questão 2

➡️ Complete a linha abaixo para definir `distances` como uma nova lista construída a partir de poiList. A nova lista será uma lista de tuplas contendo, para cada POI, seu nome e sua distância até o ponto de referência, dado por `givenLat` e `givenLon`.

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

## Resolução
### ❌ Erro ao resolver:

~~~haskell
  let distances = map (\(n,lat,lon) -> (n, calcDistance givenLat givenLon)) poiList
  putStrLn "\n==> Distância de cada ponto até o ponto de referência:"
  mapM_ (\(n, d) -> printf "%s: %f\n" n d) distances
~~~

*O erro foi esquecer de passar `lat` e `lon` para a função `calcDistance` e não converter `givenLat` e `givenLon` de `float` para `double`, resultando em um erro de compilação.*

<img width="1913" height="1072" alt="image" src="https://github.com/user-attachments/assets/6f51c408-0b13-423a-98ac-3e050f982e2c" />

## ✅ Jeito correto: 
~~~haskell
  let distances = map (\(nome, lat, lon) -> (nome, calcDistance (realToFrac givenLat) (realToFrac givenLon) lat lon)) poiList
  putStrLn "\n==> Distância de cada ponto até o ponto de referência:"
  mapM_ (\(n, d) -> printf "%s: %f\n" n d) distances
~~~

➡️ Para cada tupla (nome, lat, lon), foi criado uma nova tupla (nome, distância)

➡️ Calcula-se a distância usando a função `calcDistance`

➡️ Converte-se `givenLat` e `givenLon` de `Float` para `Double` usando `realToFrac`

<img width="1907" height="1058" alt="image" src="https://github.com/user-attachments/assets/653b3796-7bb5-4d40-9671-983c155cb33b" />

# Questão 3

➡️Complete a linha abaixo para definir `selectedPOIs` como uma nova lista construída a partir de `poiList`. A nova lista deverá conter apenas os pontos de interesse cuja distância do ponto de referência seja >= `MaxDistance`

~~~haskell
  let selectedPOIs = COMPLETE 
  printf "\n==> Pontos distantes do ponto de referência (%.6f, %.6f):\n" givenLat givenLon
  mapM_ print selectedPOIs
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

## Resolução

~~~haskell
let selectedPOIs = filter (\(nome, lat, lon) -> calcDistance (realToFrac givenLat) (realToFrac givenLon) lat lon >= maxDistance) poiList
printf "\n==> Pontos distantes do ponto de referência (%.6f, %.6f):\n" givenLat givenLon
mapM_ print selectedPOIs
~~~


➡️ `\(nome, lat, lon) ->` é uma função lambda que recebe uma tupla de 3 elementos: (`nome`, `lat`, `lon`) que representa um POI

➡️ `calcDistance` calcula a distância entre o ponto de referência e o POI atual

➡️ Usa-se `filter` para selecionar apenas os elementos que atendem à condição, a condição é que a distância calculada seja >= `maxDistance` 

<img width="1903" height="1065" alt="image" src="https://github.com/user-attachments/assets/338f65fd-9a82-41c2-9983-1b419aa4efa6" />

*`selectedPOIs` será uma lista contendo apenas os POIs que estão a 1.5 km ou mais de distância do ponto de referência (Jardim Botânico), mantendo o formato original das tuplas (nome, latitude, longitude).*

# Funções desconhecidas:

## ⚪ `mapM_` 

➡️ É útil para executar algo apenas para seus efeitos colaterais.

~~~haskell
mapM_ print [1,2,3]             -- Imprime 3 números, não guarda nada
~~~
*O _ significa "descarta o resultado" - use quando só importa a ação, não o retorno*

## Diferenças entre `mapM_` e `mapM`

➡️ `mapM_` = executa ações E descarta os resultados - utiliza-se quando os resultados não são necessários, apenas os *side-effects*.

➡️ `mapM` = executa ações E retorna os resultados - utiliza-se quando precisa-se dos resultados.

______________________

# Referências
https://hoogle.haskell.org/?hoogle=mapM_

https://stackoverflow.com/questions/27609062/what-is-the-difference-between-mapm-and-mapm-in-haskell

https://wiki-haskell-org.translate.goog/All_About_Monads?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc






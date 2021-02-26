  ## TODO: return list of top 5 artists with the most songs for a given genre.
### 1. SELECT
Aqui ele exige que você retorne conforme o rake três valores.
![enter image description here](https://github.com/thiagohrcosta/resposta1/blob/master/imgs/rakeexigencia1.png?raw=true)
Para saber o que significa cada valor é possível usar o Sqliteonline para descobrir.
![enter image description here](https://github.com/thiagohrcosta/resposta1/blob/master/imgs/rakeexigencia2.png?raw=true)
Assim é possível saber que 22 se refere ao ID, então no SELECT será necessário inserir uma forma de selecionar o ID da banda, o nome da banda, e ao final realizar a contagem de quantas músicas a citada banda tem.

> **SELECT**  o_id_da_banda, o_nome_da_banda, **COUNT**(nº_de_músicas)
>
> **FROM** tabela_onde_ficam_as_musicas
>
### A)  JOIN ALBUMS
Em seguida é necessário começar a fazer os JOINS. Será necessário usar as tabelas **albums, artists e genres.** Sempre devemos buscar o ID como item de comparação por ser algo único em uma tabela.
Assim fazemos um JOIN na tabela **albums** e assim temos:
 ![enter image description here](https://github.com/thiagohrcosta/resposta1/blob/master/imgs/rakeexigencia4.png?raw=true)
 ![enter image description here](https://github.com/thiagohrcosta/resposta1/blob/master/imgs/rakeexigencia5.png?raw=true)
 <br>
Dentro dela o identificador único é o id, logo  para acessá-lo  será necessário albums.id que deverá ser igual a algo que possa identificar a que album uma determinada música pertence.  Portanto, será necessário ir até a tabela **tracks** para pesquisar o que será comparado.

> **JOIN** albums **ON** albums.id = ALGO RELACIONADO NA **TABELA TRACKS** que possa ser usado para relacionar com albums.id

### B) JOIN ARTISTS
Em seguida devemos fazer o mesmo que foi feito no item anterior, contudo dessa vez utilizando a tabela artists, de forma a comprar se o músico apontado por seu id único, é o mesmo que possui uma música. Contudo a tabela TRACKS não possui um relacionamento direto com o cantor, sendo necessário utilizar outra tabela para identificar quem é o cantor de uma determinada música. Já que a música pertence a um album e é esse album que identifica o  cantor.

> **JOIN** artists **ON** artists.id = albums.artists_id

### C) JOIN GENRES
O mesmo que os items anteriores, fazendo um JOIN na tabela genres é utilizando o que foir único para compará-los, lembrando de que deve ser puxado da tabela tracks um dos comparativos.

### 2. WHERE

Uma vez criado os JOINS é necessário incluir uma cláusula para comparar se o parâmetro que é enviado pelo programa `#{genre_name}` é igual o nome do gênero do item selecionado.

> **WHERE** o_nome_do_genero =  '#{genre_name}'

**3. GROUB BY**
O enunciado exige que sejam listados os cinco artistas com mais músicas, portanto, o GROUP BY deve respeitar isso, agrupando os cantores mediante seu identificador único.

**4. ORDER BY**
O enunciado exige que sejam ordenados de forma decrescente os músicos com mais músicas, portanto deve ser usado o DESC no item que foi usado para contar a quantidade de música.

**5. LIMITE**
O enunciado exige que apenas cinco resultados sejam retornados, assim basta usar o **LIMIT** e o número de resultados que deseja.

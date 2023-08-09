```typescript
import React, { useEffect, useState } from "react";
//Primeiro vamos definir a interface do nosso objeto, nesse primeiro momento vamos listar apenas o nome.

interface Specie {
  name: string;
  uid: string;
  humanoide: boolean;
}

function ListApi() {
  //Criar o useState com a lista de especies
  const [species, setSpecies] = useState<Specie[]>([]);
  //Fazer a requisição para a API assim que carregar a página, solicitando as 100 primeiras especies
  //Incuir o useState para o campo de busca
  const [search, setSearch] = useState("");
  const filteredSpecies =
    search.length > 0
      ? species.filter((repo) => repo.name.includes(search))
      : [];
  //fim
  useEffect(() => {
    fetch(
      "https://stapi.co/api/v2/rest/species/search?pageNumber=1&pageSize=100"
@@ -145,12 +152,23 @@ function ListApi() {
      });
  }, []);
  return (
    //Exibir na tela
    //Inclusão  do input e da condicional de busca
    <div>
      <input
        name="search"
        placeholder="Buscar..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        type="text"
      />
      <ul>
        {species?.map((specie) => {
          return <li key={specie.name}>{specie.name}</li>;
        })}
        {search.length > 0
          ? filteredSpecies?.map((specie) => {
              return <li key={specie.name}>{specie.name}</li>;
            })
          : species?.map((specie) => {
              return <li key={specie.name}>{specie.name}</li>;
            })}
      </ul>
    </div>
  );

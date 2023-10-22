# Proposta
O grupo Piquete Pitico quis integrar as ferramentas da Cohere com o público geral de forma que aumentasse a conexão desse com a música. 
Para isso, decidiu-se fazer uma forma de receber sugestões de músicas dada uma foto. O porquê dessa escolha é por conta da temática do projeto ter um impacto grande e em um público diverso, seja entre ele:

* Um casal que deseja ter uma playlist literalmente à sua cara;
* Uma pessoa que tem em mente eternizar uma viagem com faixas músicas nostálgicas;
* Um grupo de amigos que gostariam de complementar o registro de um momento especial com músicas;
* Uma pessoa desejar realizar um post no Instagram com um par perfeito de música e foto.

# Solução
Para que realizar esse projeto seja possível, é inprescindível a ajuda da Cohere com a disponibilidade de suas ferramentas. Com isso em mente, as etapas do projeto seriam as seguintes:
1. Conseguir uma descrição da imagem
   * Fez-se o uso de outros softwares confiáveis que apenas realizaram funções de image captioning e emotion detection para que seja possível, no futuro, vincular o que ocorre na imagem com as músicas.
2. Coletar uma boa quantidade de músicas
   * Foi-se usado como fonte o dataset "audio features and lyrics of spotify songs" [link](https://www.kaggle.com/datasets/imuhammad/audio-features-and-lyrics-of-spotify-songs "audio features and lyrics of spotify songs") que não só contém as letras de 18000 músicas, mas também aspectos como danceability,	energy,	speechiness,	acousticness,	instrumentalness,	liveness, e	valence.
3. Gerar os embeddings da imagem
   * Usando a descrição da imagem, completa com a emoção, e o endpoint de Embed da Cohere, foi possível gerar a descrição vetorial da figura.
4. Gerar os embeddings de um conjunto limitado de músicas
   *  Do continguente total, foram geradas embeddings de 5000 músicas que consideram a letra e as características, por exemplo danceability, das músicas.
   *  As caracteristicas estavam em valores decimais, o que pode trazer dificuldade ao modelo para processar. Para lidar com isso, fez-se um valor limitante para cada uma caracteristica que, acima dele, a música tem a presença dessa feature (ex.: danceability > 0.5 implica na música ser dançavel)
5. Realizar uma Nearest Neighbors Search
   * Plottar os embeddings das músicas e da descrição da imagem no espaço e ver quais canções estão mais próximas da descrição.
   * Para lidar com distância, usou-se a similaridade por cosseno.
6. Coletar as top 10 melhores
   * As menores distâncias representam as músicas que mais combinam com a imagem e, portanto, seriam as recomendadas.

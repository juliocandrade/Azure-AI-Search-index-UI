# Azure-AI-Search-index-UI

Para a realização do trabalho, foram seguidos os passos descritos no site **[Microsoft Learn](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html)**

Vamos imaginar que você trabalha para a Fourth Coffee, uma rede nacional de cafés. Você foi solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a busca de insights sobre as experiências dos clientes. Você decide criar um índice do Azure AI Search usando dados extraídos de avaliações de clientes.

# Uso

Criar recursos do Azure, extrair dados de uma fonte de dados, enriqueçer os dados com habilidades de IA, utilizar o indexador do Azure no portal do Azure, consultar seu índice de pesquisa e Revisar os resultados salvos em uma Loja de conhecimento

# Processo

<details>
<summary>Crie um recurso do Azure AI Search</summary>

1. Entre no [portal do Azure](https://portal.azure.com).

2. Clique no botão **+Criar um recurso** e pesquise *Azure AI Search* e crie um recurso **Azure AI Search** com as seguintes configurações:
    - **Assinatura**: *sua assinatura do Azure*;
    - **Grupo de recursos**: *selecione ou crie um grupo de recursos com um nome exclusivo*;
    - **Nome do serviço**: *um nome exlusivo*;
    - **Região**: *Leste dos EUA*;
    - **Nível de preços**: Básico;

3. Selecione **Revisar + criar** e depois de ver a resposta **Validation Success**, selecione **Criar**.

4. Após a conclusão da implantação, selecione **Ir para o recurso**. Na Página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

</details>
<details>
<summary>Crie um recurso de serviços de IA do Azure</summary>

Você precisará provisionar um recurso de **serviços de IA do Azure** que esteja no mesmo local que seu recurso do Azure AI Search. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

1. Retorne à página inicial do portal do Azure. Clique no botão **＋Criar um recurso** e pesquise os serviços de IA do Azure . Selecione **criar** um plano de **serviços de IA do Azure**. Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:
    - **Assinatura**: *sua assinatura do Azure*;
    - **Grupo de recursos**: *O mesmo grupo de recursos que seu recurso do Azure AI Search*;
    - **Região**: *o mesmo local do recurso do Azure AI Search*;
    - **Nome**: *Um nome exclusivo*;
    - **Nível de preços**: Padrão S0;
    - **Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo**: Selecionado;

2. Selecione **Revisar + criar**. Depois de ver a resposta **Validation Passed**, selecione **Create**.

3. Aguarde a conclusão da implantação e visualize os detalhes da implantação.

</details>
<details>
<summary>Crie uma conta de armazenamento</summary>

1. Retorne à página inicial do portal do Azure e selecione o botão **+ Criar um recurso**.
2. Procure *conta de armazenamento* e crie um recurso de **conta de armazenamento** com as seguintes configurações:
    - **Assinatura**: *sua assinatura do Azure*;
    - **Grupo de recursos**: *O mesmo grupo de recursos que seu recurso do Azure AI Search e dos serviços Azure AI*;
    - **Nome da conta de armazenamento**: *Um nome exclusivo*;
    - **Localização**: *Escolha qualquer localização disponível*;
    - **Performance**: Standard;
    - **Redundância**: armazenamento localmente redundante (LRS);

3. Clique em **Revisar** e em **Criar**. Aguarde a conclusão da implantação e vá para o recurso implantado.

4. Na conta de Armazenamento do Azure que você criou, no painel de menu esquerdo, selecione **Configuração** (em **Configurações**).

5. Altere a configuração de Permitir acesso anônimo de Blob para **Habilitado** e selecione **Salvar**.

</details>
<details>
<summary>Carregar documentos para o armazenamento do Azure</summary>
  
1. No painel do menu esquerdo, selecione **Containers**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/0ab11c22-b684-4eb5-9196-fe8547b6c462)

2. Selecione **+ Contêiner**. Um painel do seu lado direito é aberto.

3. Insira as seguintes configurações e clique em **Criar**:
    - **Nome**: Coffee-Reviews;
    - **Nível de acesso público**: Container (acesso de leitura anônimo para containers e blobs);
    - **Avançado**: *sem alterações*;


4. Em uma nova guia do navegador, baixe as avaliações de café compactadas em https://aka.ms/mslearn-coffee-reviews e extraia os arquivos para a pasta de *avaliações*.

5. No portal do Azure, selecione o contêiner de *coffee-reviews*. No contêiner, selecione **Carregar**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/2610a069-f050-4e37-8c67-65fccefb5489)

6. No painel **Carregar blob**, selecione **Selecionar um arquivo**.

7. Na janela do Explorer, selecione **todos** os arquivos na pasta de *avaliações*, selecione **Abrir** e, em seguida, selecione **Carregar**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/7354bb1d-aafa-42cc-bf2f-0132057bfe6e)

8. Depois que o upload for concluído, você poderá fechar o painel **Upload blob**. Seus documentos estão agora em seu contêiner de armazenamento de *coffee-reviews*.

</details>
<details>
<summary>Indexar os documentos</summary>

Depois de armazenar os documentos, você poderá usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um *assistente de importação de dados*. Com este assistente, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

1. No portal do Azure, navegue até o recurso Azure AI Search. Na página **Visão geral**, selecione **Importar dados**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/19b89b57-6e52-410c-aa82-9c4ccb01d31d)

2. Na página **Conectar-se aos seus dados**, na lista **Fonte de Dados**, selecione **Azure Blob Storage**. Preencha os detalhes do armazenamento de dados com os seguintes valores:
    - **Fonte de dados**: Armazenamento de Blobs do Azure;
    - **Nome da fonte de dados**: coffee-customer-data;
    - **Dados a extrair**: Conteúdo e metadados;
    - **Modo de análise**: Padrão;
    - **Cadeia de conexão**: *Selecione **Escolha uma conexão existente**. Selecione sua conta de armazenamento, selecione o contêiner de **coffee-reviews** e clique em **Selecionar**;
    - **Autenticação de identidade gerenciada**: Nenhuma;
    - **Nome do contêiner**: *esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente*;
    - **Pasta Blob**: *deixe em branco*;
    - **Descrição**: Avaliações sobre Fourth Coffee Shops;

3. Selecione **Próximo: Adicionar habilidades cognitivas (opcional)**.
4. Na seção **Anexar Serviços Cognitivos**, selecione o seu recurso de serviços Azure AI.
5. Na seção Adicionar enriquecimentos:
    - Altere o **nome da qualificação** para **coffee-skillset**;
    - Marque a caixa de seleção **Habilitar OCR e mesclar todo o texto no campo merged_content**;
        > [!IMPORTANT]
        > É importante selecionar **Habilitar OCR** para ver todas as opções de campo enriquecido.
    - Certifique-se de que o **campo Dados de origem** esteja configurado como **merged_content**.
    - Altere o **nível de granularidade de enriquecimento** para **Páginas (blocos de 5.000 caracteres)**.
    - Não selecione *Habilitar enriquecimento incremental*
    - Selecione os seguintes campos enriquecidos:
    <div align="center">
        <table>
          <thead>
            <tr>
              <th><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Habilidade Cognitiva</font></font></th>
              <th><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Parâmetro</font></font></th>
              <th><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Nome do campo</font></font></th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Extraia nomes de locais</font></font></td>
              <td>&nbsp;</td>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Localizações</font></font></td>
            </tr>
            <tr>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Extraia frases-chave</font></font></td>
              <td>&nbsp;</td>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">frases chave</font></font></td>
            </tr>
            <tr>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Detectar sentimento</font></font></td>
              <td>&nbsp;</td>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">sentimento</font></font></td>
            </tr>
            <tr>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Gerar tags de imagens</font></font></td>
              <td>&nbsp;</td>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">imagemTags</font></font></td>
            </tr>
            <tr>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Gere legendas de imagens</font></font></td>
              <td>&nbsp;</td>
              <td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">legenda da imagem</font></font></td>
            </tr>
          </tbody>
        </table>
    </div>

6. Em **Salvar enriquecimentos em um armazenamento de conhecimento**, selecione:
    - Projeções de imagem
    - Documentos
    - Páginas
    - Frases chave
    - Entidades
    - Detalhes da imagem
    - Referências de imagem
   
    > [!IMPORTANT]
      > Se aparecer um aviso solicitando uma **cadeia de conexão de conta de armazenamento**.
      > ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/d3be082e-4c3f-492b-b46f-d8e79f29f314)
      > 1. Selecione **Escolha uma conexão existente**. Escolha a conta de armazenamento que você criou anteriormente.
      > 2. Clique em **+ Container** para criar um novo contêiner chamado **knowledge-store** com o nível de privacidade definido como **Private** e selecione **Create**.
      > 3. Selecione o contêiner de **knowledge-store** e clique em **Selecionar** na parte inferior da tela.

7. Selecione **projeções de blob do Azure: Documento**. Uma configuração para o *nome do contêiner* com as exibições preenchidas automaticamente do contêiner de *armazenamento de conhecimento*. Não altere o nome do contêiner.

8. Selecione **Próximo: Personalizar índice de destino**. Altere o **nome do índice** para **coffee-index**.

9. Certifique-se de que a **chave** esteja configurada como **metadata_storage_path**. Deixe o **nome do sugeridor** em branco e o **modo de pesquisa** preenchido automaticamente.

10. Revise as configurações padrão dos campos de índice. Selecione **filtrável** para todos os campos que já estão selecionados por padrão.
    ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/10dfec10-7e0c-4edd-94ac-25c7b036cfd1)

11. Selecione **Próximo: Criar um indexador**.

12. Altere o **nome do indexador** para **coffee-indexer**.

13. Deixe a **programação** definida como **Once**.

14. Expanda as **opções avançadas**. Certifique-se de que a opção **Base-64 Encode Keys** esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.

15. Selecione **Enviar** para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
    - Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
    - Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
    - Mapeia os campos extraídos para o índice.

16. Volte à página de recursos do Azure AI Search. No painel esquerdo, em **Gerenciamento de pesquisa**, selecione **Indexadores**. Selecione o **coffee-indexer** recém-criado . Espere um minuto e selecione **↻ Atualize** até que o **Status** indique sucesso.

17. Selecione o nome do indexador para ver mais detalhes.
    ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/1103a0b1-6776-4792-84e1-4eae462bb429)

</details>
<details>
<summary>Consultar o índice</summary>
Use o Search Explorer para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search Explorer para escrever consultas e revisar resultados em JSON.

1. Na página Visão geral do serviço de pesquisa , selecione **Explorador de pesquisa** na parte superior da tela.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/e7e6f6d5-a2a4-463e-9f40-adddd327e571)

2. Observe como o índice selecionado é o índice de café que você criou. Abaixo do índice selecionado, altere a visualização para **JSON view**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/a7c17b21-a966-412c-8098-e77b75d23f1d)

No campo do **editor de consultas JSON**, copie e cole:

1. Selecione **Pesquisar**. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo **@odata.count**. O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.

2. Agora vamos filtrar por localização. No campo do **editor de consultas JSON**, copie e cole:

```
{
    "search": "*",
    "count": true
}
```

3. Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra revisões com localização em Chicago. Você deveria ver [3] no [@odata.count] campo.

4. Agora vamos filtrar por sentimento. No campo do **editor de consultas JSON**, copie e cole:

```
{
 "search": "sentiment:'negative'",
 "count": true
}
```

5. Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra revisões com sentimento negativo. Você deveria ver [1] no [@odata.count] campo.

  > [!IMPORTANT]
  > Veja como os resultados são classificados por [@search.score]. Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quão próximos os resultados correspondem à consulta fornecida.

6. Um dos problemas que podemos querer resolver é por que pode haver certas avaliações. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da revisão?

</details>
<details>
<summary>Revise o armazenamento de conhecimento</summary>
Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente *Importar dados*, você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA que persistem na forma de projeções e tabelas.

1. No portal do Azure, navegue de volta para a sua conta de armazenamento do Azure.

2. No painel do menu esquerdo, selecione **Containers**. Selecione o contêiner de **armazenamento de conhecimento**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/d915b53e-2635-460e-9f36-f8e747928fcc)

3. Selecione qualquer um dos itens e clique no arquivo **objectprojection.json**.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/f2dff3fd-31e6-4fc1-994e-2c5b02e0e1a3)

4. Selecione **Editar** para ver o JSON produzido para um dos documentos do seu armazenamento de dados do Azure.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/02a54059-b98b-44e2-b5c1-7d0579309355)

5. Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento *Containers*.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/93de9150-560f-429d-aa04-d4059a00a0b6)

6. Em *Containers*, selecione o contêiner *coffee-skillset-image-projection*. Selecione qualquer um dos itens.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/171bd5ca-8083-4270-b79b-8e94b6c245a2)

7. Selecione qualquer um dos arquivos *.jpg*. Selecione *Editar* para ver a imagem armazenada no documento. Observe como todas as imagens dos documentos são armazenadas desta forma.
   ![image](https://github.com/juliocandrade/Azure-AI-Search-index-UI/assets/66694754/d79b7504-1024-4b75-9429-38996352ebc4)

8. Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento *Containers*.

9. Selecione **Navegador de armazenamento** no painel esquerdo e selecione **Tabelas**. Há uma tabela para cada entidade no índice. Selecione a tabela *coffeeSkillsetKeyPhrases*.

Observe as frases-chave que o armazenamento de conhecimento conseguiu capturar do conteúdo das avaliações. Muitos dos campos são chaves, portanto você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.
</details>
<details>
<summary>Saber mais</summary>

Esta pesquisa simples indexa apenas algumas das capacidades do serviço Azure AI Search. Para saber mais sobre o que você pode fazer com este serviço, consulte a [página do serviço Azure AI Search](https://learn.microsoft.com/azure/search).
</details>


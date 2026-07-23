Guia de Importação — Dashboard Orçamentos

Resumo
- O dashboard importa planilhas em `.xlsx`, `.xls` e `.csv`.
- Código principal: `index.html` (função `importExcel`).
- Arquivo de exemplo: `Planilha_Dashboard_exemplo.csv`.

Como usar
1. Abra `index.html` no navegador.
2. Clique em "Importar Planilha" e selecione o arquivo (.xlsx/.xls/.csv).
3. O nome do arquivo aparece ao lado do botão. Após importação um alerta confirma o sucesso.
4. Verifique as abas/tabelas e os filtros (Mês, Ano, Responsável).

Formato esperado
- Para XLSX/XLS: o script procura por abas com nomes que contenham (insensível a acentos/caixa):
  - "oportunidade", "oportunidades", "proposta" → carregadas como Oportunidades (aba P)
  - "pedido", "pedidos" → carregadas como Pedidos (aba O)
- Para CSV: o tipo (Oportunidade vs Pedido) é inferido pelo nome do arquivo — inclua "pedido" no nome para tratar como pedidos, caso contrário é tratado como oportunidades.

Colunas reconhecidas (nomes flexíveis)
- NS/Proposta, Numero Serie, NS
- Cliente
- Equipamento
- Status (valores: "Aprovado", "Reprovado", ou contendo "aguard")
- Valor Aprovado, Valor Reprovado, Valor
- Data Envio, Data Retorno (aceita formatos dd/mm/yyyy, yyyy-mm-dd ou datas Excel)
- Dias Espera, Responsavel

Observações técnicas
- O leitor usa SheetJS (`xlsx.full.min.js`) para XLSX/XLS e um parser CSV simples para CSV.
- Datas do Excel (números) são convertidas corretamente; strings em `dd/mm/yyyy` ou `yyyy-mm-dd` também funcionam.
- Normalização de cabeçalhos: acentos, espaços e símbolos são removidos para reconhecer colunas mesmo com variações.

Erros e solução de problemas
- Nada acontece ao selecionar o arquivo:
  - Abra o Console (F12 → Console). Logs mostram mensagens como "Importando planilha..." e as abas detectadas.
  - Verifique se o arquivo tem extensão correta (.csv/.xlsx/.xls).
- Alerta "Abas 'Oportunidade' e 'Pedidos' não encontradas": verifique os nomes das abas ou use CSV com nome de arquivo apropriado.
- Erro ao ler a planilha: o alerta mostrará a mensagem; cole o erro do Console e eu ajudo.

Testes
- Use `Planilha_Dashboard_exemplo.csv` para validar o fluxo.

Próximos passos possíveis
- Gerar um `Planilha_Dashboard_exemplo.xlsx` com abas separadas.
- Validar colunas obrigatórias e mostrar aviso detalhado quando faltarem.
- Suportar importação via URL/Google Sheets.

Arquivo alterado
- `index.html` — melhorias no `importExcel`, suporte CSV, logging, mensagens de erro/sucesso.

Atividade de Cobertura de Código - Verificação e Validação de Software

Vinicius Vasquez Galvão Pires

Pra essa atividade eu escolhi o Rich, que é uma biblioteca de Python bem conhecida, usada pra deixar o terminal mais bonito, com cores, tabelas, barras de progresso e essas coisas.

1) Onde está o repositório?

Está no GitHub: https://github.com/Textualize/rich

2) Qual a linguagem e o framework de testes?

O projeto é todo em Python e os testes são feitos com pytest. Eles ficam na pasta tests, e cada arquivo testa uma parte da biblioteca, tipo o test_table.py, que testa as tabelas, e o test_progress.py, que testa as barras de progresso.

3) Qual ferramenta de cobertura foi usada?

Eles usam o pytest-cov, que é um plugin do pytest que mede a cobertura enquanto os testes rodam (por baixo ele usa o Coverage.py). Depois o resultado vai pro Codecov, um site que guarda o histórico e mostra os relatórios de cobertura.

4) Tem badge ou relatório de cobertura?

Tem sim. No README do Rich aparece o badge do Codecov com a porcentagem, e clicando nele dá pra ver o relatório completo: https://codecov.io/gh/Textualize/rich

O que eu achei mais legal é que o Codecov comenta sozinho em cada pull request mostrando se a cobertura subiu ou caiu. Um exemplo é o PR 2394: https://github.com/Textualize/rich/pull/2394

Nesse PR a cobertura estava em 98,71% e foi pra 98,67% depois do merge, ou seja, caiu um pouquinho. De 7.767 linhas, só 103 não estavam cobertas.

5) Como a cobertura é executada?

Ela roda pelo GitHub Actions, toda vez que alguém faz um push ou abre um pull request. O comando que eles usam é esse:

pytest tests -v --cov=./rich --cov-report=xml:./coverage.xml --cov-report term-missing

Resumindo o que ele faz: o --cov=./rich mede só o código da biblioteca, sem contar os próprios testes. O --cov-report=xml gera um arquivo coverage.xml, que é o que o Codecov usa. E o term-missing mostra no terminal quais linhas ficaram sem teste. Depois disso o workflow manda o arquivo pro Codecov.

6) Pontos fortes e limitações

Do lado bom, a cobertura é muito alta, quase 99%, e tudo acontece de forma automática, então ninguém precisa lembrar de rodar nada. Também achei muito útil o comentário do Codecov nos pull requests, porque dá pra ver na hora se uma mudança piorou a cobertura antes de aceitar. E o term-missing ajuda bastante porque mostra exatamente onde falta teste.

Mas tem algumas limitações. A principal é que cobertura alta não quer dizer que os testes são bons: uma linha pode ser executada sem que o teste confira se o resultado está certo. Outra coisa é que, pelo comando, eles medem só as linhas, e não se os dois caminhos de cada if/else foram testados (pra isso precisaria do --cov-branch). O relatório também depende do Codecov, que é um serviço de fora. No próprio PR 2394 eles contam que o pytest-cov deu problema no Python 3.11 e a cobertura ficou um tempo sem rodar nessa versão. E como o Rich é uma biblioteca visual, a cobertura não garante que o que aparece na tela está certo.

Conclusão

No geral, o Rich usa cobertura de um jeito bem organizado e chega perto dos 99%. Mas com essa atividade eu percebi que a cobertura serve mais pra mostrar o que ainda não foi testado do que pra provar que o código está funcionando direitinho. Sozinha ela não basta, precisa vir junto com testes bem feitos.

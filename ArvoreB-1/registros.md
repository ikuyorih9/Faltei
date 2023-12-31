# PLANEJAMENTO DA BASE DADOS DO FALTEI.

## O registro de cabeçalho.

O registro de cabeçalho é formado por 13 bytes (0 à 12), contendo:
* **Status (0)**: representa a consistência do arquivo e ocupa **1 byte**. Ao começar a escrita de dados no arquivo, o status é '0'. Ao terminar a escrita, o status é '1'.

* **Próximo RRN (1)**: apresenta o RRN (byte de localização) do próximo registro vazio, disponível para escrita. É um inteiro, portanto, ocupa **4 bytes**.

* **Último RRN excluido (5)**: apresenta o RRN (byte de localização) do último registro apagado, correspondendo ao topo da pilha de registros apagados. É um inteiro, portanto, ocupa **4 bytes**.

* **Quantidade de registros (9)**: apresenta a quantidade de registros presentes no arquivo. É um inteiro, portanto, ocupa **4 bytes**.

## O registro de dados.

O registro de dados possui tamanho fixo em **256 bytes**, apresentando os campos variáveis (strings) e fixos (char e inteiros):

* **Byte de remoção (char);**
* **Nome da disciplina (string);**
* **Nome do professor (string);**
* **Cor da disciplina (int);**
* **Quantidade de créditos (int).** 
* **Nome do arquivo de faltas (string).**

Os campos variáveis apresentam **4 bytes** ao início para indicar o seu tamanho. Os espaços restantes ao fim do arquivo serão preenchidos com o número 7 (Bell). O nome do arquivo de faltas é criado a partir do RRN do registro, visto que ele é único no arquivo. Quando um arquivo é marcado como removido ('1'), os próximos 4 bytes indicam o topo da subpilha de registros apagados; caso não haja, é marcado com '-1'.

OBS: Eu tô pensando em remover o nome do arquivo de faltas, porque o nome é sempre "faltas_RRN", podendo ser obtido pelo código. Para valer a pena, é preciso que o nome do arquivo não seja montável. Isso aconteceria se o arquivo de faltas fosse criado independente do registro. É um dilema a se pensar, pois o arquivo de faltas ser criado pelo registro faz com que, ao adicionar uma falta na Disciplina, tenha que adicionar a falta no arquivo, pelo Registro. **Talvez, a criação do arquivo deva ser feita pela Disciplina, não pelo Registro. Dessa forma, a linkagem do registro com o nome acontece apenas uma vez e toda adição de falta, não é problema do Registro, mas da Disciplina.**

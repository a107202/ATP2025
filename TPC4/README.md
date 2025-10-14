# TPC$: Aplicação para gerir um cinema

## Ana Teresa da Silva Ribeiro

## Resumo
O TPC4 consistiu no desenvolvimento do código de uma aplicação, em Python, para criar uma aplicação de gestão de um cinema

### O programa 
Suponha que está a desenvolver uma aplicacão para gestão de um conjunto de salas de cinema de um centro comercial. 
Nesse centro comercial existem algumas salas de cinema (que poderão estar a exibir filmes ou não), cada sala tem uma determinada 
lotação, uma lista com a referência dos bilhetes vendidos (lugares ocupados; cada lugar é identificado por um número inteiro), e cada sala tem um filme associado.

Considera a seguinte sugestão para o modelo dos cinemas:

Cinema = [Sala]
Sala = [nlugares, Vendidos, filme]
nlugares = Int
filme = String 
Vendidos = [Int]

  
Que poderá ser usado num programa da seguinte forma:

sala1 = (150, [], "Twilight")
sala2 = (200, [], "Hannibal")
cinema1 = []
...
cinema1 = inserirSala(cinema1,sala1)
cinema1 = inserirSala(cinema1,sala2)
...
listar(cinema1)
...

if(disponivel(cinema1, "Twilight", 17 )):
  cinema1 = vendebilhete(cinema1, "Twilight", 17 )
...
listardisponibilidades(cinema1)
...


Especifique as funções utilizadas no exemplo:

1.⁠ ⁠⁠ listar( cinema ) ⁠ - que lista no monitor todos os filmes que estão em exibição nas salas do cinema passado como argumento;

2.⁠ ⁠⁠ disponivel( cinema, filme, lugar ) ⁠ - que dá como resultado *False* se o lugar lugar já estiver ocupado na sala onde o filme está a ser exibido e dará como resultado *True* se o inverso acontecer;

3.⁠ ⁠⁠ vendebilhete( cinema, filme, lugar ) ⁠ - que dá como resultado um novo cinema resultante de acrescentar o lugar à lista dos lugares ocupados, na sala onde está a ser exibido o filme;

4.⁠ ⁠⁠ listardisponibilidades( cinema ) ⁠ - que, para um dado cinema, lista no monitor para cada sala, o filme que está a ser exibido e o total de lugares disponíveis nessa sala (número de lugares na sala menos o número de lugares ocupados);

5.⁠ ⁠⁠ inserirSala( cinema, sala ) ⁠ - que acrescenta uma sala nova a um cinema (devendo verificar se a sala já existe);

6.⁠ ⁠Acrescente todas as outras funcionalidades que achar necessárias;

7.⁠ ⁠À semelhança do exercício 3, construa uma aplicação com um menu de interface para as operações.

## Resultados
```python
def existe(cinema, filme):
    cond = False
    for sala in cinema:
        if sala[2] == filme:       
            cond = True
    return cond

def inserirSala(cinema, sala):
    if not existe(cinema, sala[2]):
        cinema.append(sala)
        print("A sala foi adicionada!")
    else:
        print(f"A sala com o filme {sala[2]} já existe.")
    return cinema

def listar(cinema):
    print ("-----------------Lista de Filmes---------------")
    for sala in cinema:
        nlugares, vendidos, nomef = sala                           
        print(f"Filme: {nomef}       | Nº Lugares: {nlugares}")
    print("------------------------------------------------")
    return

def disponivel(cinema, filme, lugar):
    cond = False
    for sala in cinema:
        nlugares, vendidos, nomef = sala
        if nomef == filme and lugar <= nlugares and lugar not in vendidos:
                cond = True
    return cond 

def vendeBilhete(cinema, filme, lugar):     
    if disponivel(cinema, filme, lugar):
        for sala in cinema:
            nlugares, vendidos, nomef = sala
            if nomef == filme:
                vendidos.append(lugar)
                return f"O lugar {lugar} para o filme {filme} foi adquirido com sucesso!"
    return f"O lugar {lugar} para o filme {filme} não está disponível. Selecione outra opção."
        

def listardisponibilidades( cinema ):
    print("----------------Disponibilidade do Cinema----------------")
    for sala in cinema:
        nlugares, vendidos, nomef = sala
        disponiveis = nlugares - len(vendidos)      
        print (f"Nome: {nomef}      | Lugares Disponíveis: {disponiveis}")
    print("----------------------------------------------------------")
    return

sala1 = (150, [], "Twilight")
sala2 = (200, [13, 48, 49, 175], "Hannibal")

cinema =[sala1, sala2]

def menu(cinema):

    cond = True
    opcoes = ("1" , "2" , "3" , "4" , "5") 
    while cond:
        print("---------------Gestão de Salas de Cinema---------------\n 1 - Listar todos os filmes\n 2 - Listar a disponibilidade das salas dos filmes\n 3 - Vender bilhetes para um filme\n 4 - Adiciona uma nova sala de cinema\n 5 - Sair")

        escolha = input("Escolha a sua opção introduzindo um número da lista:")

        if escolha in opcoes:

            if escolha == "1":
                listar(cinema)
            
            if escolha == "2":
                listardisponibilidades(cinema)
            
            if escolha == "3":
                filme = str(input("Introduz o nome do filme que deseja ver:"))
                lugar = int(input(f"Introduza o número do lugar, entre 1 e o nº de lugares da sala, para o filme {filme}:"))
                res = vendeBilhete(cinema, filme, lugar)
                print(res)

            if escolha == "4":
                filme = str(input("Introduza o nome do filme:"))
                nlugares = int(input(f"Introduza o número de lugares da sala do filme {filme}:"))
                novoFilme = [nlugares, [], filme]   
                cinema = inserirSala( cinema, novoFilme )
            
            if escolha == "5":
                print("Escolheu a opção de sair. Até à próxima!")
                cond = False
        else:
            print("Opção inválida. Por favor, escolha outra opção.")
menu(cinema)

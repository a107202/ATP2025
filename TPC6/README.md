# TPC6: Aplicação para gestão da meteorologia

## Ana Teresa da Silva Ribeiro

## Resumo
O TPC6 consistiu no desenvolvimento do código de uma aplicação, em Python, para criar uma aplicação de gestão da meterologia

### O programa
Colocar numa aplicação externa ao notebook as seguintes funcionalidades:

 - Calcula a temperatura média de cada dia, dando como resultado uma lista de pares: [(data, temperaturaMédia)];
 - Define uma função para guardar uma tabela meteorológica num ficheiro de texto;
 - Define uma função para carregar uma tabela meteorológica de um ficheiro de texto;
 - Calcula a temperatura mínima mais baixa registada na tabela, dando como resultado esse valor;
 - Calcula a amplitude térmica (diferença entre a temperatura máxima e a temperatura mínima) de cada dia, dando como resultado uma lista de pares: [(data, amplitude)];
 - Calcula o dia em que a precipitação registada teve o seu valor máximo e indica esse valor, dando como resultado o par (data, valor);
 - Define uma função que recebe uma tabela meteorológica e um limite p e retorna uma lista de pares [(data, precipitação)] correspondente aos dias em que a precipitação foi superior a p;
 - Define uma função que recebe uma tabela meteorológica e um limite p e retorna o maior número consecutivo de dias com precipitação abaixo desse limite;
- Define uma função que recebe uma tabela meteorológica e desenha os gráficos da temperatura mínima, máxima e de pluviosidade.

## Resultado
```python
import matplotlib.pyplot as plt


def mostrar_menu():
    print("----------Menu de Operações----------")
    print("1: Calcula Média de cada dia")
    print("2: Guardar tabela meteorológica num ficheiro de texto")
    print("3: Carregar tabela meteorológica de um ficheiro de texto")
    print("4: Temperatura mais baixa da tabela")
    print("5: Calcula a amplitude térmica de cada dia")
    print("6: Calcula o dia em que a precipitaçao foi maxima")
    print("7: Calcula os dias que a precipitaçao é maior que p")
    print("8: Calcula o numero de dias consecutivos de dias com precipitaçao abaixo do limite p")
    print("9: Recebe tabela meteorológica e desenha os graficos da Tmín., Tmax., e da pluviosidade.")
    print("0: Sair da aplicaçao.")
    print("-------------------------------------")

def medias(tabMeteo):
    res = []
    for elem in tabMeteo:
        media= (elem[1] + elem[2])/2
        data = elem[0]
        tuplo = (data, media)
        res.append(tuplo)
    return res


def guardaTabMeteo(t, fnome):
    file = open(fnome,"w")    

    for data, min, max, prec in t:
        ano, mes, dia = data
        registo = f"{ano}-{mes}-{dia} | {min} | {max} | {prec}\n" 
        file.write(registo)
    file.close()
    return



def carregaTabMeteo(fnome):
    
    file = open(fnome, "r")   
    res = []
    for line in file:          
       
        line = line.strip()        
        campos = line.split("|")  
        data, min, max, prec = campos   
        ano, mes, dia = data.split("-") 
        tuplo = ((int(ano), int(mes), int(dia)), float(min), float(max), float(prec))
        res.append(tuplo)
    file.close()
    return res



def minMin(tabMeteo):
    minimo = tabMeteo[0][1]
    for data, min, *_ in tabMeteo:
        if min < minimo:
            minimo = min
    return minimo



def amplTerm(tabMeteo):
    res = []
    for elem in tabMeteo:
        amp= (elem[2] - elem[1])
        data = elem[0]
        tuplo = (data, amp)
        res.append(tuplo)
    return res



def maxChuva(tabMeteo):
    data_max = None
    valor_max = 0
    for data, Tmin, Tmax, prec in tabMeteo:
        if prec > valor_max:
            data_max = data
            valor_max = prec
    return(data_max, valor_max)



def diasChuvosos(tabMeteo, p):
    res = []
    for data, min, max, prec in tabMeteo:
        if prec > p:
            tuplo = (data, prec)
            res.append(tuplo)
    return res



def maxPeriodoCalor(tabMeteo, p):
    local_consec = 0
    global_consec = 0
    for data, min, max, prec in tabMeteo:
        if prec < p:
            local_consec = local_consec + 1
        else:
            if local_consec > global_consec:
                global_consec = local_consec
            local_consec = 0
    if local_consec > global_consec:
        global_consec = local_consec  
           
    return global_consec



def grafTabMeteo(t):
    
    datas = [f"{data[0]}-{data[1]}-{data[2]}" for data, *_ in t]
    temps_min = [min for data, min, *_ in t]
    temps_max = [max for data,min, max, prec in t]
    precs = [prec for data,min, max, prec in t]

    plt.plot(datas,temps_min, label="Temp Min", color="Blue", marker="o")    
    plt.plot(datas,temps_max, label="Temp Max", color="Red", marker="o")
    plt.xlabel("Data")
    plt.ylabel("Temperatura ºC")
    plt.title("Temperatura Minima")
    plt.legend()
    plt.show()

    plt.bar(datas,precs, color="b")
    plt.xlabel("Data")
    plt.ylabel("Precipitaçao mm")
    plt.title("Precipitaçao")
    plt.legend()
    plt.show()

    
    return


def main():
    tabMeteo =[]
    fnome = "meteorologia.txt"
    p = None        

    while True:
        mostrar_menu()
        opcao = input("\nEscolha uma opção: ")

        if opcao == "1":
            resultado = medias(tabMeteo)
            print(f"Médias de cada dia:{resultado}")

        elif opcao == "2":
            guardaTabMeteo(tabMeteo, fnome)
            print(f"Tabela guardada em {fnome}")

        elif opcao == "3":
            tabMeteo = carregaTabMeteo(fnome)
            print(f"Tabela carregada: {tabMeteo}")

        elif opcao == "4":
            resultado = minMin(tabMeteo)
            print(f"Temperatura mais baixa é {resultado}")

        elif opcao == "5":
            resultado = amplTerm(tabMeteo)
            print(f"Amplitude térmica de cada dia: {resultado}")

        elif opcao == "6":
            resultado = maxChuva(tabMeteo)
            print(f"Dia com precipitaçao máxima: {resultado}")
        
        elif opcao == "7":
            p = float(input("Introduza um valor para o limite p:"))
            resultado = diasChuvosos(tabMeteo, p)
            print(f"Dias com precipitaçao maior que p: {resultado}")
        
        elif opcao == "8":
            p = float(input("Introduza um valor para o limite p:"))
            resultado = maxPeriodoCalor(tabMeteo, p)
            print(f"Numero máximo de dias consecutivos com precipitaçao abaixo de p: {resultado}")

        elif opcao == "9":
            if tabMeteo:
                grafTabMeteo(tabMeteo)
            else:
                print("Carregue ou insira dados na tabela antes de criar graficos.")
        
        elif opcao == "0":
            print("\nSaindo da aplicação...")
            return

tabMeteo = [((2022,1,20), 2, 16, 0),((2022,1,21), 1, 13, 0.2), ((2022,1,22), 7, 17, 0.01)]  
        
main()


# chess-of-beginners-one-pieces-pieces

tabuleiro = [0] * 8

for i in range(len(tabuleiro)):
    tabuleiro[i] = [" - "] * 8

def print_tabuleiro(tabuleiro):
    for i, linha in enumerate(tabuleiro):
        print(8 - i, end =": ")
        for j, coluna in enumerate(linha):
            print(coluna, end =" ")
        print("\n")
    print("    " + "A" + "   " + "B" + "   " + "C" + "   " + "D" + "   " + "E" + "   " + "F" + "   " + "G" + "   " + "H")

pecas_brancas = {
    "bUP": [(6, 0), (6, 1), (6, 2), (6, 3), (6, 4), (6, 5), (6, 6), (6, 7)],
    "bCC": [(7, 1), (7, 6)],
    "bSB": [(7, 2), (7, 5)],
    "bZT": [(7, 0), (7, 7)],
    "bNR": [(7, 3)],
    "bLR": [(7, 4)]
}

pecas_pretas = {
    "pUP": [(1, 0), (1, 1), (1, 2), (1, 3), (1, 4), (1, 5), (1, 6), (1, 7)],
    "pCC": [(0, 1), (0, 6)],
    "pSB": [(0, 2), (0, 5)],
    "pZT": [(0, 0), (0, 7)],
    "pNR": [(0, 3)],
    "pLR": [(0, 4)]
}

colunas = {
    "A": 0,
    "B": 1,
    "C": 2,
    "D": 3,
    "E": 4,
    "F": 5,
    "G": 6,
    "H": 7
}

def colocar_pecas(tabuleiro):

    #peças brancas
    for peca, quadrados in pecas_brancas.items():
        for quadrado in quadrados:
            x, y = quadrado[0], quadrado[1]
            tabuleiro[x][y] = peca

    #peças pretas
    for peca, quadrados in pecas_pretas.items():
        for quadrado in quadrados:
            x, y = quadrado[0], quadrado[1]
            tabuleiro[x][y] = peca

colocar_pecas(tabuleiro)

vez_atual = 1

def checar_captura_reis(tabuleiro):
    rei_branco_presente = any("bLR" in linha for linha in tabuleiro)
    rei_preto_presente = any("pLR" in linha for linha in tabuleiro)
    if not rei_branco_presente:
        print("REI BRANCO CAPTURADO! JOGADOR PRETO VENCE A PARTIDA!")
        return True
    if not rei_preto_presente:
        print("REI PRETO CAPTURADO! JOGADOR BRANCO VENCE A PARTIDA!!")
        return True
    return False

while(True):
    print_tabuleiro(tabuleiro)
    print("")

    jogador_atual = "Mugiwaras brancos" if vez_atual % 2 == 1 else "Mugiwaras pretos"
    vez_atual += 1

    print(jogador_atual + ", é a sua vez!")
    print("")
    
    quadrado_inicial = input("Escolha qual peça você quer mover (ex. E2): ")
    inicio_x, inicio_y = quadrado_inicial[0], quadrado_inicial[1]
    inicio_x = colunas[inicio_x]
    inicio_y = 8 - int(inicio_y)
    inicio_x, inicio_y = inicio_y, inicio_x

    quadrado_final = input("Agora escolha qual quadrado você quer mover sua peça (ex. E4): ")
    fim_x, fim_y = quadrado_final[0], quadrado_final[1]
    fim_x = colunas[fim_x]
    fim_y = 8 - int(fim_y)
    fim_x, fim_y = fim_y, fim_x

    tabuleiro[fim_x][fim_y] = tabuleiro[inicio_x][inicio_y]
    tabuleiro[inicio_x][inicio_y] = " - "

    if checar_captura_reis(tabuleiro):
        break

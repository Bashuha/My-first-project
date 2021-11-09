# My-first-project
field = [[" "] * 3 for i in range(3)]


def show():
    print(" Добро пожаловать в лучшую игру на плнете! ")
    print(' -----------------------------------------')
    print(" Формат ввода: у, х. Пример: 0 2 или 2 2 ")
    print()
    print("    | 0 | 1 | 2 | ")
    print("  --------------- ")
    for i, row in enumerate(field):
        row_str = f"  {i} | {' | '.join(map(str, row))} | "
        print(row_str)
        print("  --------------- ")
    print()


def ask():
    while True:
        cord = input("          Ваш ход: ").split()

        if len(cord) != 2:
            print(" введите 2 координаты! ")
            continue

        x, y = cord

        if not(x.isdigit()) or not(y.isdigit()):
            print(" Введите числа! ")
            continue

        x, y = int(x), int(y)

        if 0 > x or x > 2 or y > 2 or y < 0:
            print(" Неверные координаты! ")
            continue

        if field[x][y] != " ":
            print(" Занято! ")
            continue

        return x, y


def chek_win(n):
    for i in range(3):
        symbols = []
        for j in range(3):
            symbols.append(field[i][j])
        if symbols == [n, n, n]:
            print(f" Выиграл {n}!!! gl next ")
            return True

    for i in range(3):
        symbols = []
        for j in range(3):
            symbols.append(field[j][i])
        if symbols == [n, n, n]:
            print(f" Выиграл {n}!!! gl next ")
            return True

    symbols = []
    for i in range(3):
        symbols.append(field[i][i])
    if symbols == [n, n, n]:
        print(f" Выиграл {n}!!! gl next ")
        return True

    symbols = []
    for i in range(3):
        symbols.append(field[i][2 - i])
    if symbols == [n, n, n]:
        print(f" Выиграл {n}!!! gl next ")
        return True

    return False


num = 0
while True:
    num += 1

    show()

    if num % 2 == 1:
        print(" Ходит крестик ")
    else:
        print(" Ходит нолик ")

    x, y = ask()

    if num % 2 == 1:
        field[x][y] = "X"
    else:
        field[x][y] = "0"

    if chek_win("X"):
        break
    if chek_win("0"):
        break
    if num == 9:
        print(" Ничья ")
        break

import random

#Функция для попытки
def getclue(num, secret):
  #num = str(num)
  if num == secret:
    return "\nПоздравляю, Вы угадали число!"
  clue = []
  for i in range(len(secret)):
    if (num[i] == secret[i]):
      clue.append("Fermi")
      #clue[n] = "Fermi"
    elif (num[i] in secret):
      clue.append("Pico")
  if (len(clue) == 0):
    clue.append("Bagels")
  return " ".join(clue)

#Сыграть снова
def again():
  while True:
    try:
      answer = int(input("Начать заново? (1 - да, 0 - нет)"))
      return answer
    except:
      print('Вы ошиблись в вводе')

#Выбор уровня сложности и загадывание слова
def number_create():
  while True:
    lv = int(input("Выберите уровень сложности (от 1 до 3): "))
    if (lv == 1) or (lv == 2) or (lv == 3):
      break
  match lv:
    case 1:
     number = 3
    case 2:
     number = 4
    case 3:
     number = 5
  digits = list(range(10))
  random.shuffle(digits)
  #secret = digits[:4]
  secret = ''.join(map(str, digits[:number]))
  return secret, lv
#Основная программа


print("Я буду загадывать число, попытайся его отгадать!")
print('Ты будешь получать подсказки:')
print("Pico - одна из цифр угадана верно, но стоит не на своем месте")
print("Fermi - Одна из цифр угадана верно и стоит на своей позиции")
print("Bagels - Все цифры угаданы не верно\n")
while True:
  numt = 10
  secret, lv = number_create()
  print("Я загадал! У тебя {} попыток, чтобы угадать. Успехов :)".format(numt))
  #print("secret number: {}".format(secret))
  while numt > 0:
    while True:
      print("\nПопытка №{}".format(10 - numt + 1))
      #print(lv)
      if (lv == 1) or (lv == 2):
        question = input("Введите число длиной в {} цифры\n".format(len(secret)))
      elif lv == 3:
        question = input("Введите число длиной в {} цифр\n".format(len(secret)))
      if (len(question) == len(secret)):
        break
      else:
        print("Вы ошиблись в вводе, введите число нужной длины")
    clue = getclue(question, secret)
    print(clue)
    numt -= 1
    if (numt == 0):
      print("Вы проиграли! Я загадал {}".format(secret))
    elif (clue == "\nПоздравляю, Ты угадал число!"):
      break
  if (again() == 0):
    break

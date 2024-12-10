from tkinter import *
from tkinter.ttk import *
import requests
import datetime
from tkinter import messagebox as mb

root = Tk()
root.title("курс валюта")
root.geometry("300x300+100+100")

def proverka_cheeeeeek():
    valueue = c.get()
    sum = e1.get()
    if all(char.isdigit() for char in sum) and sum != "":
        if valueue != "":
            get_api()
        else:
            mb.showerror(
                "Error",
                'Выберите какую вальюту вы хотите использовать '
            )
    else:
        mb.showerror(
            "Error",
            f"{sum} не может быть конвертирован"
        )






def get_api_in():
    API = "https://cbu.uz/uz/arkhiv-kursov-valyut/json/"
    response = requests.get(API)
    data = response.json()
    global usd, rub , eur

    try:
        for item in data:
            if item['Ccy'] == 'USD':
                usd = item['Rate']
            elif item['Ccy'] == 'RUB':
                rub = item['Rate']
            elif item['Ccy'] == 'EUR':
                eur = item['Rate']
        ll1.config(text=f"1$ = {usd} sum")
        ll2.config(text=f"1₽ = {rub} sum")
        ll3.config(text=f"1€ = {eur} sum")
    except:
        print("error")





def get_api():
    API = "https://cbu.uz/uz/arkhiv-kursov-valyut/json/"
    response = requests.get(API)
    data = response.json()
    global usd_rate, rub_rate , uer_rate

    try:
        for item in data:
            if item['Ccy'] == 'USD':
                usd_rate = item['Rate']
            elif item['Ccy'] == 'RUB':
                rub_rate = item['Rate']
            elif item['Ccy'] == 'EUR':
                eur_rate = item['Rate']
        radio_b_value = c.get()
        ent = float(e1.get())
        if ent == "":
            ent = 1

        if radio_b_value == "₽":
            number = float(rub_rate) * ent
            snumber = "{:,.3f}".format(number).replace(",", " ")
            a = snumber
            b = a.split(".")
            cc = int(b[1])
            if cc + 1 == 1:
                obsh = b[0]
            else:
                obsh = snumber
            total = f"Ответ: {obsh} сум"

            e2.config(text=total)
        if radio_b_value == '$':
            number = float(usd_rate) * ent
            snumber = "{:,.3f}".format(number).replace(",", " ")
            a = snumber
            b = a.split(".")
            cc = int(b[1])
            if cc + 1 == 1:
                obsh = b[0]
            else:
                obsh = snumber
            total = f"Ответ: {obsh} сум"

            e2.config(text=total)
        if radio_b_value == '€':
            number = float(eur_rate) * ent
            snumber = "{:,.3f}".format(number).replace(",", " ")
            a = snumber
            b=a.split(".")
            cc = int(b[1])
            if cc + 1 == 1:
                obsh = b[0]
            else:
                obsh = snumber
            total = f"Ответ: {obsh} сум"

            e2.config(text=total)
    except:
        print("errorr")

x = datetime.datetime.now()


a =  x.strftime("%c")
b = f'Data: {a}'
l1 = Label(text=b)
l1.pack()
l2 = Label()
l2.pack()






usd = None
rub = None
uer = None

usd_rate = None
rub_rate = None
uer_rate = None


ll1 = Label()
ll2 = Label()
ll3 = Label()

ll1.pack()
ll2.pack()
ll3.pack()

l3 = Label(text='--------------------------------------------------------------------------------')
l3.pack()

f = Frame()
f.pack()


f1 = Frame(f)
f1.pack(side=LEFT)
la = Label(f1,text="конвертировать")
la.pack()
e1 = Entry(f1,width=15)
e1.pack()

f2 = Frame(f)
f2.pack(side=LEFT)

lb = Label(f2,text="Выберите курс")
lb.pack()
value = ['$','₽','€']
c = Combobox(f2,values=value,width=2)
c.pack()

f3 = Frame(f)
f3.pack(side=LEFT)



lll =Label(f3)
lll.pack()


b = Button(f3,text="konvert", width=10,command=proverka_cheeeeeek)
b.pack()
f4 = Frame()
f4.pack(expand=1,anchor=W)
e2 = Label(f4,text="Ответ:")
e2.pack()



get_api_in()
root.mainloop()




-----------------------------------------------------------------------
pogoda


from tkinter import *
import requests
root = Tk()
root.geometry("200x200+200+200")
def lether():
    # try:
        city_id = e.get()
        API_key ="7ad2d4195f35a2cf1465794817b1de85"
        weather_get = requests.get(f"https://api.openweathermap.org/data/2.5/weather?q={city_id}&appid={API_key}&units=metric")
        wether_j = weather_get.json()
        cname = wether_j['sys']['country']
        name = wether_j['name']
        wind = wether_j['wind']['speed']
        main = wether_j['main']['temp']

        # icon_code = wether_j['weather'][0]['icon']
        # icon_url = f"http://openweathermap.org/img/wn/{icon_code}@2x.png"
        # icon_a = requests.get(icon_url)
        # icon_b = icon_a.content
        # icon = PhotoImage(data=icon_url)

        l1.config(text=f"название города: {name}")
        l2.config(text=f"название страна: {cname}")
        l3.config(text=f"скорость ветера: {wind}")
        l4.config(text=f"температураа: {main}°")
        # l5.config(image=icon)


    # except:
    #     print("error")









e = Entry(width=20)
e.pack()
b1 = Button(width=15, text="найти",command=lether)
b1.pack()
l1 = Label(text="название города     ")
l2 = Label(text="название страна      ")
l3 = Label(text="скорость ветера      ")
l4 = Label(text="температура      ")
l5 = Label(width=10,height=5)

l1.pack()
l2.pack()
l3.pack()
l4.pack()
l5.pack()



root.mainloop()





--------------------------

kalkulator



from tkinter import *
import re


root = Tk()
root.resizable(width=False, height=False)
def claear_all_item():
    ent.delete(0, END)


def giper_plus():
    try:
        tt = float(ent.get())
        fgtgfhgbf = tt ** 2
        ent.delete(0, END)
        ent.insert(END, str(fgtgfhgbf))

        a = ent.get()
        a1 = str(a[-1].strip())
        a2 = str(a[-2].strip())
        if a1 == "0" and a2 == ".":
            aww = a[:-1]
            aww1 = aww[:-1]
            ent.delete(0, END)
            ent.insert(END, str(aww1))
    except:
        print("neznayu chto proizoshlo i ne hochu znat karoche oshibka gte to na sisteme(kvadrat)")

def nu_pryam_giper_plus():
    try:
        tt = float(ent.get())
        fgtgfhgbf = tt ** (1/2)
        ent.delete(0, END)
        ent.insert(END, str(fgtgfhgbf))

        a = ent.get()
        a1 = str(a[-1].strip())
        a2 = str(a[-2].strip())
        if a1 == "0" and a2 == ".":
            aww = a[:-1]
            aww1 = aww[:-1]
            ent.delete(0, END)
            ent.insert(END, str(aww1))
    except:
        print("neznayu chto proizoshlo i ne hochu znat karoche oshibka gte to na sisteme(kvadrat)")


def minusplus():
    tt = float(ent.get())
    fgtgfhgbf = tt * -1
    ent.delete(0, END)
    ent.insert(END, str(fgtgfhgbf))




    a = ent.get()
    a1 = str(a[-1].strip())
    a2 = str(a[-2].strip())
    if a1 == "0" and a2 == ".":
        aww = a[:-1]
        aww1 = aww[:-1]
        ent.delete(0, END)
        ent.insert(END, str(aww1))

def nu_pryam_giper_plusplussss():
    try:
        tt = float(ent.get())
        fgtgfhgbf = tt ** 3
        ent.delete(0, END)
        ent.insert(END, str(fgtgfhgbf))

        a = ent.get()
        a1 = str(a[-1].strip())
        a2 = str(a[-2].strip())
        if a1 == "0" and a2 == ".":
            aww = a[:-1]
            aww1 = aww[:-1]
            ent.delete(0, END)
            ent.insert(END, str(aww1))
    except:
        print("neznayu chto proizoshlo i ne hochu znat karoche oshibka gte to na sisteme(kvadrat)")


def alc(x):
    ent.insert(END,x)

def plus():
    tt = ent.get()
    if tt[-1] != "+":
        tt = tt + "+"
    ent.delete(0, END)
    ent.insert(END, tt)
def minus():
    tt = ent.get()
    if tt[-1] != "-":
        tt = tt + "-"
    ent.delete(0, END)
    ent.insert(END, tt)
def plusx():
    tt = ent.get()
    if tt[-1] != "*":
        tt = tt + "*"
    ent.delete(0, END)
    ent.insert(END, tt)
def minusx():
    tt = ent.get()
    if tt[-1] != "/":
        tt = tt + "/"
    ent.delete(0, END)
    ent.insert(END, tt)

def counts():
    tt = ent.get()


    try:
        af = eval(tt)
        ent.delete(0, END)
        ent.insert(END, str(af))
    except:
        ent.delete(0, END)
        ent.insert(END, str("error"))
def claear_item():
    tt =  str(ent.get())
    try:
       t1 = tt[:-1]
       ent.delete(0,END)
       ent.insert(END,t1)
    except:
        print("error")


def add_tochka():
    expression = ent.get()
    numbers = re.findall(r'\d+(\.\d+)?',expression)
    if numbers:
        last_number = numbers[-1]
        total = 0
        for i in last_number:
            if i == ".":
                total = 1
        if total == 0:
            tt = ent.get()
            if tt[-1] != ".":
                tt = tt + "."
            ent.delete(0, END)
            ent.insert(END, tt)
    else:
        ent.insert(END, "0.")














ent = Entry(width=11,justify=RIGHT,font=("",28),bg="black",fg="white")
ent.grid(row=0,column=0,columnspan=4)
Button(text="1",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "1":alc(x)).grid(row=2,column=0)
Button(text="2",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "2":alc(x)).grid(row=2,column=1)
Button(text="3",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "3":alc(x)).grid(row=2,column=2)
Button(text="4",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "4":alc(x)).grid(row=3,column=0)
Button(text="5",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "5":alc(x)).grid(row=3,column=1)
Button(text="6",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "6":alc(x)).grid(row=3,column=2)
Button(text="7",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "7":alc(x)).grid(row=4,column=0)
Button(text="8",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "8":alc(x)).grid(row=4,column=1)
Button(text="9",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "9":alc(x)).grid(row=4,column=2)
Button(text="0",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "0":alc(x)).grid(row=5,column=1)
Button(text="+",width=7,height=3,bg="orange",fg="white",activebackground="white",activeforeground="orange",command=plus).grid(row=2,column=3)
Button(text="-",width=7,height=3,bg="orange",fg="white",activebackground="white",activeforeground="orange",command=minus).grid(row=3,column=3)
Button(text="*",width=7,height=3,bg="orange",fg="white",activebackground="white",activeforeground="orange",command=plusx).grid(row=4,column=3)
Button(text="/",width=7,height=3,bg="orange",fg="white",activebackground="white",activeforeground="orange",command=minusx).grid(row=5,column=3)
Button(text="√x",width=7,height=3,bg="grey",fg="white",activebackground="white",activeforeground="grey",command=nu_pryam_giper_plus).grid(row=1,column=0)
Button(text="x²",width=7,height=3,bg="grey",fg="white",activebackground="white",activeforeground="grey",command=giper_plus).grid(row=1,column=1)
Button(text="-/+",width=7,height=3,bg="grey",fg="white",activebackground="white",activeforeground="grey",command=minusplus).grid(row=1,column=2)
Button(text=",",width=7,height=3,bg="grey",fg="white",activebackground="white",activeforeground="grey",command=add_tochka).grid(row=1,column=3)
Button(text="=",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=counts).grid(row=5,column=2)
Button(text="⌫",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=claear_item).grid(row=5,column=0)
Button(text="(",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = "(":alc(x)).grid(row=6,column=0)
Button(text=")",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=lambda x = ")":alc(x)).grid(row=6,column=1)
Button(text="x³",width=7,height=3,bg="black",fg="white",activebackground="white",activeforeground="black",command=nu_pryam_giper_plusplussss).grid(row=6,column=2)
Button(text="CE",width=7,height=3,bg="orange",fg="white",activebackground="white",activeforeground="orange",command=claear_all_item).grid(row=6,column=3)



root.mainloop()





----------------



from tkinter import *
from tkinter import messagebox as mb
root = Tk()
root.title("Крестик нолики")
root.geometry('+300+300')
def nech():
    a =  mb.askyesno(

        "ниья",
        "Хочешь ешё разок сыграть?",)
    if a :
         restart_game()
    else:
        try:
            root.destroy()
        except:
            print("error")




def nich(x):
    if x == "X":

        bitt = "x is winnner"
    if x == "0":
        bitt = "x is winnner"
    if x == "nich":
        bitt = "No one isn't win"
    a =  mb.askyesno(

        bitt,
        "Хочешь ешё разок сыграть?",)
    if a :
         restart_game()
    else:
        try:
            root.destroy()
        except:
            print("error")


def update_score(winner):
    if winner == "X":
        global krestik
        krestik += 1
        l1['text'] = f"X: {krestik}"
    elif winner == "0":
        global nolik
        nolik += 1
        l2['text'] = f"0: {nolik}"
def restart_game():
    global winner_is_find, svobodno, hod
    winner_is_find = False
    for i in range(9):
        button[i]['bg'] = "white"
        button[i]['text'] = ""
    svobodno = [0, 1, 2, 3, 4, 5, 6, 7, 8]
    hod = 0
    l['text'] = "Game in Progress"
def check_winner():
    global winner_is_find
    win_conditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ]
    for condition in win_conditions:
        if button[condition[0]]['text'] == button[condition[1]]['text'] == button[condition[2]]['text'] != "":
            winner_is_find = True
            winner = button[condition[0]]['text']
            for i in range(9):
                button[i]['bg'] = "red"
            update_score(winner)
            l['text'] = f"{winner} is the winner"
            nich(winner)
            return
def button_click(x):
    try:
        global hod
        if button[x]['text'] == "" and not winner_is_find:
            if hod % 2 == 0:
                button[x].config(text="X")
            else:
                button[x].config(text="0")
            hod += 1
            svobodno.remove(x)
            check_winner()
            if len(svobodno) == 0 and not winner_is_find:
                l['text'] = "ничя"
                nech()
            if winner_is_find:
                restart_button.grid(row=5, column=1)
                exit_code.grid(row=5, column=2)
    except:
        print("error")
winner_is_find = False
hod = 0
svobodno = [0, 1, 2, 3, 4, 5, 6, 7, 8]
krestik = 0
nolik = 0
button = [Button(width=7, height=3, font=('', 15), command=lambda x=i: button_click(x)) for i in range(9)]
l = Label(text="Крестик Нолики")
l.grid(row=0, column=0, columnspan=3)
row = 1
col = 0
for i in range(9):
    button[i].grid(row=row, column=col)
    col += 1
    if col == 3:
        row += 1
        col = 0
l1 = Label(text="X: 0", width=5)
l1.grid(row=4, column=0)
l2 = Label(text="0: 0", width=5)
l2.grid(row=4, column=1)
restart_button = Button(width=7, text="Restart", fg="green", command=restart_game)
exit_code = Button(width=7, text="Exit", fg="blue", command=lambda : root.destroy())
root.mainloop()





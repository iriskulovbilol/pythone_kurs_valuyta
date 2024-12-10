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

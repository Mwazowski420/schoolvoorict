import csv,datetime

file = "klanten.csv"
klanten = []

def slaOp(naam,info):
    with open(f"factuur_{naam}",mode='w',newline='') as fileObjeWrite:
        fileWrite = csv.writer(fileObjeWrite,delimiter=';')
        fileWrite.writerow(f"Deze factuur is opgesteld voor {naam}")
        fileWrite.writerow(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
        fileWrite.writerows(info)

with open (file,mode='r',newline='') as fileOBJ:
    fileCSV = csv.reader(fileOBJ)
    next(fileCSV)
    for line in fileCSV:
        klanten.append(line)

while True:
    klant = input("Van welke klant wil u de factuur zien? ")
    totaalprijs = 0
    for line in klanten:
        totaleFactuur = []
        if klant == line[1]:
            producten = line[3].split(',')
            for product in producten:
                prijs = product.split('$')[1]
                prijs = prijs[:-1]
                totaalprijs += float(prijs)

                naam = product.split("(")[0]
                totaleFactuur.append((naam,prijs))
                print(naam,prijs)
            print("Totaalprijs:",totaalprijs)
            slaOp(klant,totaleFactuur)
          
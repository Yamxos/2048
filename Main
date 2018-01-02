from tkinter import *
from random import *

grille=4
choix=[]
case=[]
couleur=[]
for i in range(2049): #établissement de la palette de couleur du jeu
	couleur.append('')
couleur[0]='#FBF5EF';couleur[1]='#01DF3A';couleur[3]='#8A0808'
couleur[2]='#F8ECE0';couleur[4]='#F6E3CE';couleur[8]='#F5D0A9';couleur[16]='#F7BE81'
couleur[32]='#FAAC58';couleur[64]='#FE9A2E';couleur[128]='#FF8000';couleur[256]='#FE642E'
couleur[512]='#FF4000';couleur[1024]='#FF0000';couleur[2048]='#DF0101'


def alea16(): #tirage d'un nombre aléatoire entre 0 et 15
	return choice(choix)

def cheat1():
	for i in range(grille*grille):
		if(case[i]["text"]!=""):
			case[i]["text"]=str(int(case[i]["text"])+1)
			

def cheat2():
	for i in range(grille*grille):
		if(case[i]["text"]!=""):
			case[i]["text"]=str(int(case[i]["text"])*2)

def caseoccupee(): #vérification des cases occupées
	nbcases=0
	for i in range(grille*grille):
		if(case[i]["text"]!=""):
			nbcases=nbcases+1
	return nbcases

def casemorte(): #vérification des cases infusionnables
	nbcases=0
	for i in range(grille*grille):
		if((i+1)%grille!=0 and i<grille*grille-grille and case[i]["text"]!="" and case[i]["text"]!=case[i+1]["text"] and case[i]["text"]!=case[i+grille]["text"]
			or (i+1)%grille==0 and i!=grille*grille-1 and case[i]["text"]!="" and case[i]["text"]!=case[i+grille]["text"]
			or i>=grille*grille-grille and i!=grille*grille-1 and case[i]["text"]!="" and case[i]["text"]!=case[i+1]["text"]
			or i==grille*grille-1 and case[i]["text"]!=""):
			nbcases=nbcases+1
	return nbcases

def verif(): #vérification de l'état du jeu: gagné/perdu ou en cours
	if(caseoccupee()==grille*grille and casemorte()==grille*grille):
		case[grille]["text"]="GA";case[grille]["bg"]=couleur[3]
		case[grille+1]["text"]="ME";case[grille+1]["bg"]=couleur[3]
		case[grille+2]["text"]="OV";case[grille+2]["bg"]=couleur[3]
		case[grille+3]["text"]="ER";case[grille+3]["bg"]=couleur[3]
	for i in range(grille*grille):
		if(case[i]["text"]=="2048"):
			case[grille]["text"]="WE";case[grille]["bg"]=couleur[1]
			case[grille+1]["text"]="LL";case[grille+1]["bg"]=couleur[1]
			case[grille+2]["text"]="DO";case[grille+2]["bg"]=couleur[1]
			case[grille+3]["text"]="NE";case[grille+3]["bg"]=couleur[1]

def nouvellecase(): #Nouvellecase à emplacement aléatoire
	if(caseoccupee()!=grille*grille):
		spawn=random()
		while 1:
			alea=alea16()
			if(case[alea]["text"]==""):
				if(spawn<0.9):
					case[alea]["text"]="2"
					case[alea]["bg"]=couleur[2]
				else:
					case[alea]["text"]="4"
					case[alea]["bg"]=couleur[4]
				break
	verif()
		
def casevierge(i): #casevierge(à cet emplacement)
	case[i]["text"]=""
	case[i]["bg"]=couleur[0]
	
def fusecase(i): #fusecase(en direction de)
	case[i]["text"]=str(int(case[i]["text"])*2)
	case[i]["bg"]=couleur[int(case[i]["text"])]
	
def movecase(i,u): #movecase(en direction de, balance de i)
	case[i]["text"]=case[i+u]["text"]
	case[i]["bg"]=couleur[int(case[i+u]["text"])]

def tap(u): #tap(en direction de)
	for i in range(grille*grille):
		case[i]["default"]=DISABLED
	NoMove=0;j=0
	if(u==-1 or u==-grille):i=0
	if(u==1 or u==grille):i=grille*grille-1
	
	for j in range(grille*grille):
		deadend=0;boucle=0;skipped=1
		#saut de case selon mouvement
		if(u==-1 and i%grille==0):
			i=i+1
		elif(u==1 and (i+1)%grille==0):
			i=i-1
		elif(u==-grille and i<grille):
			i=i+grille
		elif(u==grille and i>=grille*grille-grille):
			i=i-grille
		else:
			skipped=0
		#MOUVEMENT
		while(deadend!=1 and case[i+u]["text"]=="" and case[i]["text"]!=""):
			movecase(i+u,-u)
			casevierge(i)
			i=i+u
			boucle=boucle+1
			NoMove=NoMove+1
			if(u==-1 and i%grille==0
			  or u==1 and (i+1)%grille==0
			  or u==-grille and i<grille
			  or u==grille and i>=grille*grille-grille):
				deadend=1
		#FUSION
		if(deadend!=1 and case[i+u]["text"]==case[i]["text"] and case[i]["text"]!="" and case[i+u]["default"]==DISABLED):
			fusecase(i+u)
			casevierge(i)
			case[i+u]["default"]=NORMAL
			NoMove=NoMove+1
			
		#remise de i à la normale
		for y in range(boucle):i=i-u
		#incrémentation selon mouvement
		if((u==-1 or u==-grille and j>grille-1) and skipped!=1):i=i+1
		if((u==1 or u==grille and j>grille-1) and skipped!=1):i=i-1
		
	if(NoMove!=0):nouvellecase()

def clavier(event):
	touche = event.keysym
	if(touche=="Left" or touche=="q"):tap(-1)
	if(touche=="Right" or touche=="d"):tap(1)
	if(touche=="Up" or touche=="z"):tap(-grille)
	if(touche=="Down" or touche=="s"):tap(grille)
	if(touche=="1"):cheat1()
	if(touche=="2"):cheat2()
			

fenetre = Tk()

for i in range(grille*grille):
	choix.append(i)

for ligne in range(grille): #création de la grille
	for colonne in range(grille):
		case.append(Button(fenetre, width=4, height=1, text="", borderwidth=10, font=('calibri', int(80*(4/grille))), bg=couleur[0], default=DISABLED))
		case[ligne*grille+colonne].grid(row=ligne, column=colonne)
		
for i in range(2): #initialisation des cases de départ
	while 1:
		alea=alea16()
		if(case[alea]["text"]==""):
			case[alea]["text"]="2"
			case[alea]["bg"]=couleur[2]
			break
	
fenetre.focus_set()
fenetre.bind("<Key>", clavier)	

fenetre.mainloop()

def afficher_menu(titre, liste_options):
    ligne="+" + "-" * (len(titre)+2) + "+"
    print(ligne)
    print("|", titre,"|")
    print(ligne)
    for i in range(len(liste_options)) :
        print(f"{i+1} -> {liste_options[i]}")


def demander_nombre(message, borne_max):
    res = input(f"{message}[{1},{borne_max}]")
    try :
        int(res)
    except :
        return None 
    if int(res) <= borne_max :
        return int(res)
    return None 

def menu(titre, liste_options):
    afficher_menu(titre,liste_options)
    message="Entrez votre choix"
    borne_max=4
    return demander_nombre(message, borne_max)
     

def programme_principal():
    liste_options = ["Charger un fichier",
                     "Rechercher la population d'une commune",
                     "Afficher la population d'un département", 
                     "Quitter"]
    liste_communes = []
    while True:
        rep = menu("MENU DE MON APPLICATION", liste_options)
        if rep is None:
            print("Cette option n'existe pas")
        elif rep == 1:
            print("Vous avez choisi", liste_options[rep - 1])
            fichier=input(f"Quelle fichier ?")
            res=charger_fichier_population(fichier)
            print(len(res))
            
        
        elif rep == 2:
            print("Vous avez choisi", liste_options[rep - 1])
        elif rep == 3:
            print("Vous avez choisi", liste_options[rep - 1])
            nom = input("Quelle commune voulez vous savoir sa population ?")
            print(population_d_une_commune(res, nom))
        else:
            break
        input("Appuyer sur Entrée pour continuer")
    print("Merci au revoir!")




def charger_fichier_population(nom_fic):
    res = open(nom_fic,"r")
    liste = []
    res.readline()
    for ligne in res :
        tmp = ligne.split(";")
        liste.append( (tmp[0],tmp[1],int(tmp[4])) ) 
    return liste

fichier1=charger_fichier_population("extrait1.csv")
def population_d_une_commune(liste_pop, nom_commune):
    for elt in liste_pop :
        if elt[1] == nom_commune :
            return elt[2]
    return None
    

def liste_des_communes_commencant_par(liste_pop, debut_nom):
    liste=[]
    for elt in liste_pop :
        if elt[1][:len(debut_nom)] == debut_nom :
            liste.append(elt[1])
    return liste

def commune_plus_peuplee_departement(liste_pop, num_dpt):
    if len(liste_pop) == 0 :
        return None
    max = True 
    for i in range(1,len(liste_pop)) :
        
        if max[2] < liste_pop[i][2] and liste_pop[i][0].startwith(num_dpt) :
            max = liste_pop[i]
    return max

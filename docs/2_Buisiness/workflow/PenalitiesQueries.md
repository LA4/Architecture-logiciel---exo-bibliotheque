GetPenalities()

GetPenalityByUser(User_id)

AddPenality(User_id)

# Fonction calcul de la pénalité en cours

<!-- Les pénalités sont calculées sur la base d’un retard quotidien (ex. 1€ par jour de retard) -->

    - PenalityMount(){
         if(!LoansBook.return){
    nb jour de pénalité = date actuelle - date de retour prévu
        pénalité de base =1
       return  nb jour de pénalité *pénalité de base
    }

}

PatchPenality(User_id)

DeletePenality(User_id)

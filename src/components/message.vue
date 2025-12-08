<template>

<div :style="{ color: couleurRouge ? 'red' : 'blue' }">

    <p @click="changetexte"> <!-- J'appelle la fonction changetexte au clic -->
        {{ texte }} </p>         <!-- Affiche la variable texte -->
    

    <p @click="afficherCompteur">  Nombre de VU ET DE O maltraités par un clique: {{ compteur }}</p> <!-- Affiche le nombre de textes générés -->

    <input type="text" v-model="texteTape"> <!-- Mise à jour automatique en direct grace a v-model -->
<p>{{ texteTape }}</p> <!-- Affiche ce que l'utilisateur tape -->

  <button @click="sauver">Sauvegarder le texte</button>

<ul>
    <li v-for="(item, index) in liste" :key="index">
        {{ item }}
    </li>
</ul>

<!-- Le bouton a texte invisible -->

    <button class="boutoninvisible" @click="invisible"> <!-- Le texte du bouton disparaît / réapparaît au clique -->
        {{ texteBouton }} 
    </button>

 <!-- Changer couleur du texte -->   
    <button @click="couleurtexte">
     (bleu / rouge)
</button>


<!-- Ajout de personnage en tableau-->
 <p>Choisir un nom et définir un niveau :</p>
  <input    
  
      type="text" 
      v-model="personneNom"
      placeholder="Pseudo"> 

    <input 
      type="number" 
      v-model="personnelvl"
      placeholder="LVL"> 

    <button @click="ajouterPersonne">
      Ajouter le personnage
    </button>
    <p>Liste de personnages crées :</p>

    <ul>  <!-- p = un éllement du tableau personne, index = position dans la liste -->
      <li v-for="(p, index) in personnes" :key="'perso-' + index"> <!-- v-for crée une boucle pour afficher chaque personnages tant qu'il y en à -->
       <!-- Le key sert à aider Vue à suivre quel élément est lequel dans la liste.-->
        {{ p.nom }} est niveau {{ p.lvl }}
          
      </li>
    </ul>
    


<button @click="analyserPersonnages">
      Analyser les personnages
    </button>

    <p>
      {{ resumePersonnes }} <!-- Résumé mis à jour après l'analyse -->
    </p>
</div>

</template>

<script>
export default {
  name: "message.vue", // Nom du composant utilisé lors de l'importation dans app.vue //

  data() {       // Variables réactives utilisées dans le composant //
    return {
        texte1: "NE PAS CLIQUER -----> ICIVUVUVUVUVVUVUVUVU <----- NE PAS CLIQUER ICI",     // Message 1 //
        texte2: "NE PAS CLIQUER -----> OOOOOOOOOOOOOOOOOOOO <----- NE PAS CLIQUER ICI",   // Message 2 //
        texte: "NE PAS CLIQUER -----> VUVUVUVUVVUVUVUVU <----- NE PAS CLIQUER ICI",        // Message affiché au départ //
        compteur: 0,                       // Compteur de changements du texte //
        texteTape: "",                   // Contient ce que l'utilisateur écrit //
        liste: [],                        // Liste vide au départ //
        texteBouton: "Rends-moi invisible", // Texte affiché au départ //
        visible: true,                      // Détermine si le texte est affiché ou non //
        couleurRouge: true,

        personneNom: "",         
        personnelvl: "",        
        personnes: [],           
        resumePersonnes: ""      


    };
  },

  methods: {

   

    changetexte() { 
        // Alterne entre texte1 et texte2 à chaque clic //
        this.texte = (this.texte === this.texte1) ? this.texte2 : this.texte1; // this = le composant vu actuel . cherche la variable //
        // " (===) Est-ce que le texte affiché est égal au message 1 ?"
        //  (?)  Si oui  → on affichera le message 2
        // (:) Si non → on affichera le message 1 //


        // Incrémente le compteur à chaque clic sur le texte //
         this.compteur++;

         console.log(this.texte); // Affiche la valeur actuelle dans la console //
        },

    sauver() {
        this.liste.push(this.texteTape); // Ajoute la valeur tapée dans la liste //
    },
    
    invisible() {
            
            this.visible = !this.visible; // Alterne l'état visible / invisible du texte //

            // Si visible = true → affiche le texte
            // Si visible = false → supprime le texte
            this.texteBouton = this.visible ? "Rends-moi invisible" : "";
        },

    couleurtexte() {
    this.couleurRouge = !this.couleurRouge;
},

    ajouterPersonne() {
        
        if (!this.personneNom || !this.personnelvl) { // Vérifie qu'on a bien un nom et un âge remplis //
            console.log("Aucun nom et niveau renseignés"); // Message dans la console //
            return;
        }

        // Ajoute un objet { nom, age } dans le tableau personnes //
        this.personnes.push({
            nom: this.personneNom,
            lvl: this.personnelvl
        });

        // Vide les champs après l'ajout //
        this.personneNom = "";
        this.personnelvl = "";
    },

    analyserPersonnages() {

        console.log("Liste complète des personnages :", this.personnes); 
        // Affiche tout le tableau de personnages dans la console //

        if (this.personnes.length === 0) { 
            // Si aucun personnage n'a encore été ajouté //
            this.resumePersonnes = "Aucun personnage enregistré pour le moment.";
            return;
        }

        const nb = this.personnes.length; 
        // Nombre total de personnages //

        const niveaux = this.personnes.map(p => Number(p.lvl)); 
        // Récupère tous les niveaux sous forme de nombres //

        const total = niveaux.reduce((acc, valeur) => acc + valeur, 0); 
        // Additionne tous les niveaux //

        const moyenne = (total / nb).toFixed(1); 
        // Calcule la moyenne des niveaux (1 chiffre après la virgule) //

        this.resumePersonnes = 
            "Personnages créés : " + nb + " | Niveau moyen : " + moyenne; 
        // Met à jour le texte affiché sur la page //
             
    },

  }        
};

   
</script>







<style scoped>
div {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    padding: 2rem;
    max-width: 700px;
    width: 100%;
    background-color: #f5f5f5;
    border-radius: 8px;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
    margin: auto;
}

div p {
    font-family: Arial, sans-serif;
    font-size: 1rem;
    text-align: center;
}

div input[type="text"],
div input[type="number"] {
    padding: 0.5rem 0.6rem;
    border-radius: 4px;
    border: 1px solid #ccc;
    width: 100%;
    max-width: 300px;
    box-sizing: border-box;
}

div button {
    padding: 0.6rem 1rem;
    border-radius: 4px;
    border: none;
    background-color: #1976d2;
    color: white;
    font-size: 1rem;
    cursor: pointer;
}

div button:hover {
    background-color: #135ea5;
}

ul {
    list-style: none;
    padding: 0;
    width: 100%;
    max-width: 300px;
}

li {
    font-family: Arial, sans-serif;
    font-size: 0.9rem;
    text-align: center;
}

.boutoninvisible {
    width: 180px;
    height: 40px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
}

/* Tableau des personnages */
.table-personnes {
    width: 100%;
    max-width: 400px;
    border-collapse: collapse;
    font-family: Arial, sans-serif;
}

.table-personnes th,
.table-personnes td {
    border: 1px solid #ccc;
    padding: 0.6rem;
    text-align: center;
}

.table-personnes th {
    background-color: #e0e0e0;
}
</style>



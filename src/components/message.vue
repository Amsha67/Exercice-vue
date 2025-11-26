<template>

<nav :style="{ color: couleurRouge ? 'red' : 'blue' }">

    <p @click="changetexte"> <!-- J'appelle la fonction changetexte au clic -->
        {{ texte }} </p>         <!-- Affiche la variable texte -->
    

    <p @click="afficherCompteur">  Nombre de texte généré : {{ compteur }}</p> <!-- Affiche le nombre de textes générés -->

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

    

</nav>

</template>

<script>
export default {
  name: "message.vue", // Nom du composant utilisé lors de l'importation dans app.vue //

  data() {       // Variables réactives utilisées dans le composant //
    return {
        texte1: "VUVUVUVUVVUVUVUVU <----- NE PAS CLIQUER ICI",     // Message 1 //
        texte2: "OOOOOOOOOOOOOOOOOOOO <----- NE PAS CLIQUER ICI",   // Message 2 //
        texte: "VUVUVUVUVVUVUVUVU <----- NE PAS CLIQUER ICI",        // Message affiché au départ //
        compteur: 0,                       // Compteur de changements du texte //
        texteTape: "",                   // Contient ce que l'utilisateur écrit //
        liste: [],                        // Liste vide au départ //
        texteBouton: "Rends-moi invisible", // Texte affiché au départ //
        visible: true,                      // Détermine si le texte est affiché ou non //
        couleurRouge: true


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
}

             
    }

            
};

   
</script>



<style scoped>
.boutoninvisible {
    width: 180px;      
    height: 40px;      /* Garde la taille de basse du bouton */
}
</style>
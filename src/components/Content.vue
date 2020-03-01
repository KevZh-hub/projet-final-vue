<template>
    <v-app id="inspire">

        <v-app-bar
                app
                color="black"
                dark
        >
            <v-toolbar-title> <a href="Content.vue">FAN PAGE - DRAGON BALL</a></v-toolbar-title>
        </v-app-bar>

        <v-content>
            <v-container
                    class="fill-height"
                    fluid
            >
                <v-row
                        align="center"
                        justify="center"
                >
                    <v-col class="page accueil">
                        <v-carousel :show-arrows="false">
                            <v-carousel-item
                                    v-for="(item,i) in items"
                                    :key="i"
                                    :src="item.src"
                                    reverse-transition="fade-transition"
                                    transition="fade-transition"
                                    @click="show(item)"
                            ></v-carousel-item>
                        </v-carousel>
                        <div v-for="(item,i) in items" :key="i"
                             :src="item.src">
                            <p v-if="item.shown">{{item.message}}</p>
                        </div>
                    </v-col>
                    <div class="bouton">
                    </div>
                </v-row>
                <v-row justify="center">
                    <v-dialog v-model="dialog" persistent max-width="600px">
                        <template v-slot:activator="{ on }">
                            <v-btn depressed class="black orange--text" dark v-on="on"><v-icon left>mdi-plus</v-icon>Ajoutez un personnage
                            </v-btn>
                        </template>
                        <v-card>
                            <v-card-title>
                                <span class="headline">Ajouter un personnage</span>
                            </v-card-title>
                            <v-card-text>
                                <v-container>
                                    <v-row>
                                        <v-col cols="12">
                                            <v-text-field label="Nom complet du personnage*" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12">
                                            <v-text-field label="Description*" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12">
                                            <v-text-field label="Email de l'auteur"></v-text-field>
                                        </v-col>
                                        <v-file-input
                                                :rules="rules"
                                                accept="image/png, image/jpeg, image/bmp"
                                                placeholder="Choisissez une image*"
                                                prepend-icon="mdi-camera"
                                                label="Illustration"
                                                required
                                        ></v-file-input>
                                    </v-row>
                                </v-container>
                                <small>*Champs obligatoire</small>
                            </v-card-text>
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn color="blue darken-1" text @click="ajout">Ajouter</v-btn>
                                <v-btn color="red darken-1" text @click="dialog = false">Annuler</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-dialog>
                </v-row>
            </v-container>
        </v-content>
        <v-footer
                color="black"
        >
            <span class="white--text">&copy; 2020</span>
        </v-footer>
    </v-app>
</template>

<script>
    export default {
        props: {
            source: String,
        },
        data: () => ({
            dialog: false,
                items: [
                    {
                        src: 'https://imgur.com/FGpmmwJ.jpg',
                        shown: false,
                        message: 'Son Gokû (孫そん悟ご空くう, Son Gokū), est le principal protagoniste des mangas Dragon Ball et Dragon Ball Super, et des leurs adaptations animées, Dragon Ball et Dragon Ball Z / Dragon Ball Kai, puis Dragon Ball Super, ainsi que de la suite animée des deux premières séries, Dragon Ball GT.\n' +
                            '\n' +
                            'Dernier orphelin exilé de la défunte planète Vegeta, il atterrit sur Terre où il grandit avec son grand-père adoptif puis seul, après avoir tué accidentellement celui-ci. Son aventure commence le jour où il rencontre Bulma, une jeune aventurière, qui l\'invite à chercher les Dragon Balls...'
                    },
                    {
                        src: 'https://imgur.com/37uMvTY.jpg',
                        shown: false,
                        message: 'Vegeta (ベジータ, Bejīta) est un des personnages principaux de la saga. Il est le prince de la planète Vegeta, son père est le roi Vegeta. Il est le mari de Bulma et le père de Trunks et Bra.\n' +
                            '\n' +
                            'Prince des Saiyans, il est d\'abord introduit comme un antagoniste lors la Saga Saiyan avant de devenir progressivement un allié des héros puis un des protagonistes principaux dès la Saga des Humains Artificiels.\n' +
                            '\n' +
                            'Orgueilleux, Vegeta devient l\'incarnation de l\'anti-héros ainsi que le rival attitré de Son Gokû au cours de l\'histoire.'
                    },
                    {
                        src: 'https://imgur.com/lQn0Aqv.jpg',
                        shown: false,
                        message: 'Trunks (トランクス, Torankusu) est l\'un des personnages principaux de Dragon Ball. Il est le fils de Vegeta et de Bulma. Par conséquent, le Roi Vegeta est son grand-père paternel, Monsieur Brief son grand-père maternel, Madame Brief sa grand-mère maternelle, Bra sa sœur et Tarble son oncle.\n' +
                            '\n' +
                            'Trunks a la particularité d\'exister deux fois dans l\'histoire. En effet, le premier Trunks qui apparaît au début de la Saga des humains artificiels vient du futur et est retourné dans le passé dans une autre chronologie grâce à une Time Machine conçue par Bulma, sa mère. Ce n\'est que quelques années plus tard qu\'il naît réellement. Dans la suite de l\'article, on distingue donc «Trunks du présent» et «;Trunks du futur».'
                    },
                    {
                        src: 'https://imgur.com/NeuSwkS.jpg',
                        shown: false,
                        message: 'Kuririn (クリリン, Kuririn) ou Krillin dans les traductions française est un combattant expert en arts martiaux, il est également le meilleur ami de Son Gokû. Il est l\'un des plus puissants guerriers parmi les terriens.'
                    },
                    {
                        src: 'https://imgur.com/pBjipK4.jpg',
                        shown: false,
                        message: 'Piccolo (ピッコロ, Pikkoro) dit Ma Junior (魔ジュニア, Ma Junia), ou traduit maladroitement Petit-Cœur dans la version française de l\'anime, est l\'un des personnages principaux de Dragon Ball. Il est le fils de Piccolo Daimaô, et aussi en quelque sorte sa réincarnation et le rival de Son Gokû. Stratégiste sage et expert qui était à l\'origine un ennemi implacable de Gokû, Piccolo devient plus tard un membre permanent des Z-Fighters lors de la série Dragon Ball Z, en particulier lorsqu\'il forme un lien étroit avec le fils de Gokû, Son Gohan, après l\'avoir formé en préparation de l\'arrivée imminente de les Saiyans et d\'autres menaces futures.'
                    },
                ],
            rules: [
                value => !value || value.size < 2000000 || 'Le poids du fichier doit être inférieur à 2 MB !',
            ],
        }),
        methods: {
            show: function(item) {
                if(!item.shown){
                    item.shown = true
                }
            },
            ajout () {
                this.item++
            }
        }
    }
</script>
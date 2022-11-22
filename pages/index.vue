<template>
    <div id="printButton" class="fixed bottom-8 right-8 border-2 p-2 px-8 font-mono font-bold text-lg border-blue-400 rounded-lg bg-blue-00 cursor-pointer" @click="print">Print</div>
    <div class="page pageBg flex flex-col p-[1rem] font-mono">
        <!-- <infos :character="character" /> -->
        <div class="flex justify-between bg-green-400 bg-opacity-0 rounded-lg">
            <caracs :character="character" />
            <div class="flex flex-col">
                <pv_ca :character="character" class="pt-3" />
                <jds :character="character" />
            </div>
            <img src="/avatar.jpg" alt="" class="rounded-lg h-56 my-auto" />
        </div>
        <div class="flex items-center justify-between py-2">
            <!-- <infos :character="character" class="bg-green-400 bg-opacity-20 p-2 rounded-lg flex-1 mr-2" /> -->
            <attaques :character="character" class="bg-red-500 bg-opacity-0 flex rounded-lg" />
            <infos :character="character" />
        </div>
        <div class="flex">
            <competences :character="character" class="bg-amber-900 bg-opacity-0 rounded-lg flex" />
            <div class="flex flex-col w-full">
                <history :character="character" class="bg-purple-900 bg-opacity-0 p-2 rounded-lg mx-auto" />
                <div class="flex p-2 bg-primary bg-opacity-20 flex-1 ml-4 rounded-lg font-bold">Notes</div>
            </div>
        </div>
        <div class="flex p-2 bg-primary bg-opacity-20 flex-1 mt-2 rounded-lg font-bold">Inventaire</div>
    </div>

    <div class="page pageBg flex flex-col p-[1rem] font-mono flex-wrap">
        <div class="flex flex-col w-1/2" v-for="(level, index) in character.dons">
            <div class="text-xl font-bold text-primary border-b-2 border-black mr-auto my-2">Niveau {{ index + 1 }}</div>
            <div v-for="don in level" class="flex flex-col my-1">
                <div class="font-bold text-lg text-primary">
                    {{ don.nom }}
                </div>
                <div>
                    {{ don.description }}
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
function levelUP() {
    init();
    character.nom = "Dolgrin";
    character.alignement = "CN";
    character.classe = "Chasseur";
    character.race = "Nain";
    character.focal = 0;
    character.taille = "M";
    character.armure = {
        name: "Armure de cuir",
        bonus_CA: 1,
        DEX_max: 4,
        maitrise: "Q",
        modif_div: 0,
    };
    character.attaques = [
        {
            nom: "Arc long de frappe +1",
            bonus_total: 0,
            modif_cara: "DEX",
            modif_div: 1,
            maitrise: "Q",
            traits: ["mortel d10"],
            des_degats: "2d8",
        },
        {
            nom: "Rapière",
            bonus_total: 0,
            modif_cara: "DEX",
            modif_div: null,
            maitrise: "Q",
            traits: ["mortel d10"],
            des_degats: "1d8",
        },
    ];

    // Niveau 1
    character.niveau = 1;

    //Ascendence : Nain
    character.PV_asc = 10;
    if (character.caracs.CON) character.caracs.CON += 2;
    if (character.caracs.DEX) character.caracs.DEX += 2;
    if (character.caracs.SAG) character.caracs.SAG += 2;
    if (character.caracs.CHA) character.caracs.CHA += 2;
    character.langues = ["Commun", "Nain"];
    character.VD = 6;

    // Héritage : nain sans ancien
    character.dons.push([]);
    character.dons[0].push(
        {
            nom: "Appel du sang ancien",
            description: "Réaction : +1 aux JDS contre effets magiques.",
        },
        {
            nom: "Connaissance de la pierre",
            description: "Tests passifs pour détécter les irrégularités dans la pierre (-2 perception). +2 en perception pour tests actifs.",
        }
    );

    //Historique : mineur
    if (character.caracs.SAG) character.caracs.SAG += 2;
    if (character.caracs.DEX) character.caracs.DEX += 2;

    character.competences.survie.maitrise = "Q";
    character.competences.conn_minieres.maitrise = "Q";
    character.dons[0].push({
        nom: "Expertise du terrain (soutterain)",
        description: "+1 en survie dans les souterrains",
    });

    // Classe : rôdeur
    character.PV_classe = 10;
    if (character.caracs.DEX) character.caracs.DEX += 2;
    character.JDS.vig.maitrise = "E";
    character.JDS.ref.maitrise = "E";
    character.JDS.vol.maitrise = "Q";
    character.competences.perception.maitrise = "E";
    character.competences.nature.maitrise = "Q";
    character.competences.medecine.maitrise = "Q";
    character.competences.acrobatie.maitrise = "Q";
    character.competences.discretion.maitrise = "Q";
    character.competences.vol.maitrise = "Q";
    character.competences.religion.maitrise = "Q";

    character.autres_competences.armes_simples.maitrise = "Q";
    character.autres_competences.armes_de_guerre.maitrise = "Q";
    character.autres_competences.sans_armes.maitrise = "Q";
    character.autres_competences.armure_intermediaire.maitrise = "Q";
    character.autres_competences.sans_armure.maitrise = "Q";
    character.autres_competences.armure_legere.maitrise = "Q";
    character.autres_competences.armure_lourde.maitrise = "I";

    character.dons[0].push(
        {
            nom: "Chasser une proie",
            description: "1A. +2 en perception/survie pour chasser/traquer ma proie.",
        },
        {
            nom: "Spécialité du chasseur : déluge",
            description: "Malus d'attaques multiples contre ma proie : -3 (-2 agile) et -6 (-4 agile).",
        },
        {
            nom: "Don : tir du chasseur",
            description: "1A. Deux attaques successives contre ma proie. Les resistances sont appliquées après la somme des dégâts.",
        }
    );

    if (character.caracs.FOR) character.caracs.FOR += 2;
    if (character.caracs.DEX) character.caracs.DEX += 2;
    if (character.caracs.CON) character.caracs.CON += 2;
    if (character.caracs.SAG) character.caracs.SAG += 2;

    // Niveau 2
    character.niveau = 2;
    character.dons.push([]);

    character.dons[1].push(
        {
            nom: "Don de compétence",
            description: "Médecine militaire (soigner les blessures en combat, 2d8)",
        },
        {
            nom: "Don : arme de gravité",
            description: "1 min. Bonus de 2*(nbr de dés de l'arme) dégâts à la première frappe de chaque tour.",
        }
    );
    character.focal++;

    // Niveau 3
    character.niveau = 3;
    character.dons.push([]);

    // Donc vélocité
    character.VD += 1.5;

    // Volonté de fer
    character.JDS.vol.maitrise = "E";

    // Amélioration de compétence
    character.competences.survie.maitrise = "E";

    // Niveau 4
    character.niveau = 4;
    character.dons.push([]);
    character.dons[3].push(
        {
            nom: "Don : brume apaisante",
            description: "2A. 9m. Soigne 2d8 et met fin à une source de dégâts persistants.",
        },
        {
            nom: "Assurance (médecine)",
            description: "Pas de lancé de dés ni de bonus/malus. Résultat automatique : 10 + bonus de maîtrise.",
        }
    );
    character.focal++;

    // Niveau 5
    character.niveau = 5;
    character.dons.push([]);
    if (character.caracs.FOR) character.caracs.FOR += 2;
    if (character.caracs.DEX) character.caracs.DEX += 1;
    if (character.caracs.SAG) character.caracs.SAG += 2;
    if (character.caracs.CON) character.caracs.CON += 2;

    // Amélioration de compétence
    character.competences.nature.maitrise = "E";

    // Don d'héritage
    character.dons[4].push({
        nom: "Défier les ténèbres",
        description: "Vision dans le noir supérieure.",
    });

    //Expertise avec les armes
    character.autres_competences.armes_simples.maitrise = "E";
    character.autres_competences.armes_de_guerre.maitrise = "E";
    character.autres_competences.sans_armes.maitrise = "E";

    //Attaques
    for (const attaque of character.attaques) {
        attaque.maitrise = "E";
    }

    // Niveau 6
    character.niveau = 6;
    character.dons.push([]);
    character.dons[5].push(
        {
            nom: "Don : caractéristique animale",
            description: "1A. 1min. Vitesse de vol égal à vitesse au sol.",
        },
        {
            nom: "Expertise du terrain (forestier)",
            description: "+1 en survie dans la forêt.",
        }
    );
    character.focal++;

    // Niveau 7
    character.niveau = 7;
    character.dons.push([]);

    //Évasion
    character.JDS.ref.maitrise = "M";

    //Sens alertes
    character.competences.perception.maitrise = "M";

    // Spécialisation martiale

    //Attaques
    for (const attaque of character.attaques) {
        if (attaque.maitrise == "E") attaque.des_degats += "+2";
    }

    // Amélioration de compétence
    character.competences.nature.maitrise = "M";

    // Don général
    character.dons[6].push({
        nom: "Don : ascendance adoptive",
        description: "Accéder aux dons ancestraux d’une autre ascendance.",
    });
    //--------------------------

    finish();
}

function getModif(modif: string | null) {
    type ObjectKey = keyof typeof character.caracs_modif;
    const key = modif as ObjectKey;
    return character.caracs_modif[key];
}

function getMaitrise(maitrise: string | null) {
    switch (maitrise) {
        case "Q":
            return 2 + character.niveau;
        case "E":
            return 4 + character.niveau;
        case "M":
            return 6 + character.niveau;
        case "L":
            return 8 + character.niveau;
        default:
            return 0;
    }
}

function init() {
    Object.entries(character.caracs).forEach(([key, value], index) => {
        type ObjectKey = keyof typeof character.caracs;
        const key2 = key as ObjectKey;
        character.caracs[key2] = 10;
    });

    Object.entries(character.competences).forEach(([key, value], index) => {
        value.maitrise = "I";
    });
}

function finish() {
    // Calculs modifs caractéristiques
    Object.entries(character.caracs).forEach(([key, value], index) => {
        type ObjectKey = keyof typeof character.caracs;
        const key2 = key as ObjectKey;
        character.caracs_modif[key2] = Math.floor((character.caracs[key2] - 10) / 2);
    });

    //Attaques
    for (const attaque of character.attaques) {
        attaque.bonus_total = getMaitrise(attaque.maitrise) + getModif(attaque.modif_cara) + attaque.modif_div;
    }

    //CA
    character.CA.bonus_total = 10 + character.armure.DEX_max + character.armure.bonus_CA + getMaitrise(character.armure.maitrise) + character.armure.modif_div;

    Object.entries(character.JDS).forEach(([key, value], index) => {
        value.bonus_total = getMaitrise(value.maitrise) + getModif(value.modif_cara) + value.modif_div;
    });

    character.PV = character.PV_asc + character.niveau * (character.caracs_modif.CON + character.PV_classe);

    Object.entries(character.competences).forEach(([key, value], index) => {
        value.bonus_total = getModif(value.modif_cara) + value.modif_div + getMaitrise(value.maitrise);
    });
}

const character = {
    PV: 0,
    focal: null as number | null,
    PV_asc: 0,
    PV_classe: 0,
    langues: [] as string[],
    dons: [] as any[],
    nom: "",
    niveau: 1,
    alignement: "",
    classe: "",
    race: "",
    taille: "",
    caracs: {
        FOR: null as number | null,
        DEX: null as number | null,
        CON: null as number | null,
        INT: null as number | null,
        SAG: null as number | null,
        CHA: null as number | null,
    },
    caracs_modif: {
        FOR: null as number | null,
        DEX: null as number | null,
        CON: null as number | null,
        INT: null as number | null,
        SAG: null as number | null,
        CHA: null as number | null,
    },
    CA: {
        bonus_total: null as number | null,
    },
    VD: null as number | null,
    JDS: {
        ref: {
            name: "Réflexes",

            bonus_total: null as null | number,
            modif_cara: "DEX",
            maitrise: null as null | string,
            modif_div: null as null | number,
        },
        vig: {
            name: "Vigueur",
            bonus_total: null as null | number,
            modif_cara: "CON",
            maitrise: null as null | string,
            modif_div: null as null | number,
        },
        vol: {
            name: "Volonté",
            bonus_total: null as null | number,
            modif_cara: "SAG",
            maitrise: null as null | string,
            modif_div: null as null | number,
        },
    },
    armure: {
        name: "",
        bonus_CA: null as null | number,
        DEX_max: null as null | number,
        maitrise: null as null | string,
        modif_div: null as null | number,
    },
    attaques: [
        {
            nom: " ",
            bonus_total: null as null | number,
            modif_cara: null as null | string,
            modif_div: null as null | number,
            maitrise: null as null | string,
            traits: [] as string[],
            des_degats: "",
        },
        {
            nom: " ",
            bonus_total: null as null | number,
            modif_cara: null as null | string,
            modif_div: null as null | number,
            maitrise: null as null | string,
            traits: [] as string[],
            des_degats: "",
        },
    ],
    competences: {
        acrobatie: {
            nom: "Acrobaties",
            bonus_total: null as null | number,
            modif_cara: "DEX",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        arcanes: {
            nom: "Arcanes",
            bonus_total: null as null | number,
            modif_cara: "INT",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        artisanat: {
            nom: "Artisanat",
            bonus_total: null as null | number,
            modif_cara: "INT",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        athletisme: {
            nom: "Athletisme",
            bonus_total: null as null | number,
            modif_cara: "FOR",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        conn_minieres: {
            nom: "Conn. minières",
            bonus_total: null as null | number,
            modif_cara: "INT",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        diplomatie: {
            nom: "Diplomatie",
            bonus_total: null as null | number,
            modif_cara: "CHA",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        discretion: {
            nom: "Discrétion",
            bonus_total: null as null | number,
            modif_cara: "DEX",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        duperie: {
            nom: "Duperie",
            bonus_total: null as null | number,
            modif_cara: "CHA",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        intimidation: {
            nom: "Intimidation",
            bonus_total: null as null | number,
            modif_cara: "CHA",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        medecine: {
            nom: "Médecine",
            bonus_total: null as null | number,
            modif_cara: "SAG",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        nature: {
            nom: "Nature",
            bonus_total: null as null | number,
            modif_cara: "SAG",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        occultisme: {
            nom: "Occultisme",
            bonus_total: null as null | number,
            modif_cara: "INT",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        perception: {
            nom: "Perception",
            bonus_total: null as null | number,
            modif_cara: "SAG",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        religion: {
            nom: "Religion",
            bonus_total: null as null | number,
            modif_cara: "SAG",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        representation: {
            nom: "Représentation",
            bonus_total: null as null | number,
            modif_cara: "CHA",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        societe: {
            nom: "Société",
            bonus_total: null as null | number,
            modif_cara: "INT",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        survie: {
            nom: "Survie",
            bonus_total: null as null | number,
            modif_cara: "SAG",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
        vol: {
            nom: "Vol",
            bonus_total: null as null | number,
            modif_cara: "DEX",
            modif_div: null as null | number,
            maitrise: null as null | string,
        },
    },
    autres_competences: {
        sans_armure: {
            nom: "Sans armure",
            maitrise: null as null | string,
        },
        armure_legere: {
            nom: "Armures légères",

            maitrise: null as null | string,
        },
        armure_intermediaire: {
            nom: "Armures intermédiaires",

            maitrise: null as null | string,
        },
        armure_lourde: {
            nom: "Armure lourdes",
            maitrise: null as null | string,
        },
        sans_armes: {
            nom: "Sans armes",
            maitrise: null as null | string,
        },
        armes_simples: {
            nom: "Armes simples",
            maitrise: null as null | string,
        },
        armes_de_guerre: {
            nom: "Armes de guerre",
            maitrise: null as null | string,
        },
    },
};

levelUP();

const print = () => {
    window.print();
};
</script>

<style>
.pageBg {
    background-image: url("./background.jpg");
    background-repeat: repeat;
}

/* document */
@media screen {
    /* Screen styles */
    body {
        background: #e0e0e0;
        background: linear-gradient(to right, #c0c0c0 0%, #e0e0e0 50%, #c0c0c0 100%);
        padding-bottom: 2cm;
    }
    .page {
        width: 21cm;
        height: 29.7cm;
        box-shadow: 0 0 1cm rgba(0, 0, 0, 0.1);
        margin: 1cm auto;
    }
}

@media print {
    /* Print styles */
    @page {
        margin: 0;
    }
    html,
    body {
        height: 100%;
    }
    main {
        height: 100%;
    }
    .page {
        min-height: 100%;
        max-height: 100%;
        height: 100vh;
        box-sizing: border-box;
        break-inside: avoid;
    }
    #printButton {
        display: none;
    }
}
</style>

<template>
	<v-container fill-height fluid class="background">
		<v-row>
			<v-col cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Dodaj studenta</v-card-title>
					<v-card-text>
						<v-form @submit="dodajStudenta" lazy-validation>
							<v-text-field type="text" placeholder="Ime" v-model="ime" :rules="nameRules" label="ime"
								required>
							</v-text-field>
							<v-text-field type="text" placeholder="Prezime" v-model="prezime" :rules="nameRules"
								label="prezime" required>
							</v-text-field>
							<v-text-field type="number" placeholder="Broj dolazaka (max 15)" v-model="brojDolazaka"
								:rules="nameRules" label="brojDolazaka" maxlength="15" required>
							</v-text-field>
							<v-text-field type="number" placeholder="Rezultat 1. kolokvija (max 40)" v-model="broj1Kolokvij"
								:rules="nameRules" label="broj1Kolokvij" maxlength="40" required>
							</v-text-field>
							<v-text-field type="number" placeholder="Rezultat 2. kolokvija (max 40)" v-model="broj2Kolokvij"
								:rules="nameRules" label="broj2Kolokvij" maxlength="40" required>
							</v-text-field>
							<v-text-field type="number" placeholder="Pracenje (max 20)" v-model="brojPracenje"
								:rules="nameRules" label="brojPracenje" maxlength="20" required>
							</v-text-field>

						</v-form>
					</v-card-text>
					<v-card-actions>
						<v-btn color="black" class="white--text" elevation="0" @click="obrisiSveUnesenePodatke">
							BRISI PODATKE
						</v-btn>
						<v-spacer></v-spacer>
						<v-btn color="red" @click="ocistiFormu">OČISTI</v-btn>
						<v-btn @click="dodajStudenta">OK</v-btn>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "prvi-zadatak",
	data() {
		return {
			error: [],
			ime: null,
			prezime: null,
			brojDolazaka: null,
			broj1Kolokvij: null,
			broj2Kolokvij: null,
			brojPracenje: null,
		};
	},
	watch: {},
	methods: {

		ocistiFormu() {
			this.$refs.form.reset()
		},
		dodajStudenta() {
			let noviStudent = {
				ime: this.ime,
				prezime: this.prezime,
				brojDolazaka: this.brojDolazaka,
				broj1Kolokvij: this.broj1Kolokvij,
				broj2Kolokvij: this.broj2Kolokvij,
				brojPracenje: this.brojPracenje,
			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));
			/*
						if (this.ime && this.prezime && this.brojDolazaka && this.broj1Kolokvij && this.broj2Kolokvij && this.brojPracenje) {
							console.log("login function called")
						}
						this.error = [];
						if (this.ime) {
							this.error.push("name is required")
						}
						if (this.prezime) {
							this.error.push("prezime is required")
						}
			*/
		},
		obrisiSveUnesenePodatke() {
			localStorage.clear();
		},
	},
};
</script>

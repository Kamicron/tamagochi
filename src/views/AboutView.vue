<template>
  <div class="container">
    <div class="name">Nom de l'animal</div>
    <div class="face">
      <span class="face-arms">{{ animalFace[0] }}</span>
      <span class="face-eyes">{{ animalFace[1] }}</span>
      <span class="face-nose">{{ animalFace[2] }}</span>
      <span class="face-eyes">{{ animalFace[3] }}</span>
      <span class="face-arms">{{ animalFace[4] }}</span>
    </div>
    <div class="status">
      <div class="stat">
        <div class="stat-name">Fatigue:</div>
        <div class="stat-bar">
          <div class="stat-progress" :style="{ width: fatigue + '%' }"></div>
        </div>
        <div class="stat-value">{{ parseInt(fatigue) }}</div>
      </div>
      <div class="stat">
        <div class="stat-name">Faim:</div>
        <div class="stat-bar">
          <div class="stat-progress" :style="{ width: faim + '%' }"></div>
        </div>
        <div class="stat-value">{{ parseInt(faim) }}</div>
      </div>
      <div class="stat">
        <div class="stat-name">Plaisir:</div>
        <div class="stat-bar">
          <div class="stat-progress" :style="{ width: plaisir + '%' }"></div>
        </div>
        <div class="stat-value">{{ parseInt(plaisir) }}</div>
      </div>
    </div>

    <div class="buttons">
      <button class="button" @click="reposer()">Reposer</button>
      <button class="button" @click="nourrir()">Nourrir</button>
      <button class="button" @click="jouer()">Jouer</button>
    </div>
    <div class="inventory">Inventaire</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fatigue: 100,
      faim: 100,
      plaisir: 100,
      maxStat: 100,
      animalFace: ""
    };
  },
  methods: {
    nourrir() {
      this.faim = this.faim + 10 > this.maxStat ? this.maxStat : this.faim + 10;
    },
    reposer() {
      this.fatigue = this.fatigue + 10 > this.maxStat ? this.maxStat : this.fatigue + 10;
    },
    jouer() {
      this.plaisir = this.plaisir + 10 > this.maxStat ? this.maxStat : this.plaisir + 10;
      this.faim = this.faim - 10 < 0 ? 0 : this.faim - 10;
      this.fatigue = this.fatigue - 10 < 0 ? 0 : this.fatigue - 10;
    },
    updateAnimalFace() {
      if (this.faim < 30 && this.fatigue < 30) {
        this.animalFace = "(╯︵╰)";
      } else if (this.faim < 30) {
        this.animalFace = "(˘~˘)";
      } else if (this.fatigue < 30) {
        this.animalFace = "(︶︿︶)";
      } else if (this.plaisir < 30) {
        this.animalFace = "(•_•)";
      } else {
        this.animalFace = "(^▿^)";
      }
    },
    decreaseStats() {
      setInterval(() => {
        this.faim -= 0.208333333; // 100/8h
        this.fatigue -= 0.069444444; // 100/24h
        this.plaisir -= 0.166666667; // 100/10h
      }, 1000);
    }
  },
  watch: {
    faim() {
      this.updateAnimalFace();
    },
    fatigue() {
      this.updateAnimalFace();
    },
    plaisir() {
      this.updateAnimalFace();
    }
  },
  mounted() {
    this.updateAnimalFace();
    this.decreaseStats();
  }
};
</script>







<style>
.container {
  display: grid;
  grid-template-rows: auto auto 1fr auto;
  grid-template-columns: 1fr;
  gap: 1rem;
  height: 100vh;
  justify-items: center;
  background-color: var(--color-white);
}

.name {
  grid-row: 1 / 2;
  grid-column: 1 / -1;
  font-size: 1.5rem;
  font-weight: bold;
  text-align: center;
  color: var(--color-dark-gray);
}

.face {
  grid-row: 2 / 3;
  grid-column: 1 / -1;
  font-size: 3rem;
  text-align: center;
  color: var(--color-dark-gray);
}

.face-arms {
  color: var(--color-arms);
}

.face-eyes {
  color: var(--color-eye);
}

.face-nose {
  color: var(--color-nose);
}

.status {
  grid-row: 3 / 4;
  grid-column: 1 / -1;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: var(--color-dark-gray);
  width: 100%;
}

.stat {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0.5rem;
  flex: 1;
}

.stat-text {
  font-size: 1rem;
  font-weight: bold;
  margin-right: 1rem;
}

.stat-bar {
  width: 100%;
  height: 1rem;
  border-radius: 0.5rem;
  background-color: var(--color-light-gray);
}

.stat-progress {
  height: 100%;
  border-radius: 0.5rem;
  background-color: var(--color-light-blue);
}

.buttons {
  grid-row: 4 / 5;
  grid-column: 1 / -1;
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.button {
  font-size: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.25rem;
  background-color: var(--color-light-blue);
  color: var(--color-white);
  cursor: pointer;
}

.inventory {
  grid-row: 5 / 6;
  grid-column: 1 / -1;
  font-size: 1rem;
  text-align: center;
  color: var(--color-dark-gray);
}
</style>

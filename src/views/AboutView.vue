<template>
  <div class="container">
    <div class="name">Nom de l'animal</div>
    <div class="face">Visage de l'animal</div>
    <div class="status">
      <div class="stat">
        <div class="stat-bar">
          <div class="stat-progress" :style="{ width: fatigue + '%' }"></div>
        </div>
        <span class="stat-label">Fatigue:</span>
        <span class="stat-value">{{ fatigue }}</span>
      </div>
      <div class="stat">
        <div class="stat-bar">
          <div class="stat-progress" :style="{ width: faim + '%' }"></div>
        </div>
        <span class="stat-label">Faim:</span>
        <span class="stat-value">{{ faim }}</span>
      </div>
      <div class="stat">
        <div class="stat-bar">
          <div class="stat-progress" :style="{ width: plaisir + '%' }"></div>
        </div>
        <span class="stat-label">Plaisir:</span>
        <span class="stat-value">{{ plaisir }}</span>
      </div>
    </div>
    <div class="buttons">
      <button class="button" @click="nourrir()">Nourrir</button>
      <button class="button" @click="reposer()">Reposer</button>
      <button class="button" @click="jouer()">Jouer</button>
    </div>
    <div class="inventory">Inventaire</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      fatigue: 10,
      faim: 100,
      plaisir: 100,
      maxStat: 100
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
    }
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

.status {
  grid-row: 3 / 4;
  grid-column: 1 / -1;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: var(--color-dark-gray);
}

.stat {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0.5rem;
  width: 100%;
  flex: 1;
}

.stat-text {
  font-size: 1rem;
  font-weight: bold;
  margin-right: 1rem;
}

.stat-bar {
  flex-basis: 100%;
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
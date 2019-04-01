<template>
  <div class="container">
    <p class="winStatus">{{ isWin ? '戦闘終了' : '戦闘中' }}</p>
    <div class="monsters">
      <div
        v-for="(monster, index) of monsters"
        :key="index"
        class="monster"
        :class="{ isDead: isDead(monster.life) }"
      >
        <img :src="require(`@/assets/poke-${index + 1}.png`)" alt="" />
        <p class="monster__name">{{ monster.name }}</p>
        <p class="monster__attack">攻撃力: {{ monster.attack }}</p>
        <p class="monster__life" :class="{ isDead: isDead(monster.life) }">
          <span
            :style="{ transform: `scaleX(${monster.life / monster.maxLife})` }"
            class="fill"
          ></span>
          <span>{{ monster.life }}</span>
        </p>
        <div v-if="!isDead(monster.life)">
          <button @click="attack(monster.attack, index)">攻撃</button>
          <button @click="heal(index)">回復</button>
        </div>
      </div>
    </div>
    <button v-if="isWin" style="margin-top: 24px" @click="reset">
      リセット
    </button>
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  data() {
    return {
      isWin: false,
      monsters: [
        {
          name: 'ピカチュウ',
          attack: 50,
          life: 100,
          maxLife: 100
        },
        {
          name: 'フシギバナ',
          attack: 40,
          life: 150,
          maxLife: 150
        },
        {
          name: 'カビゴン',
          attack: 20,
          life: 200,
          maxLife: 200
        }
      ]
    }
  },

  methods: {
    attack: function(attack, selfIndex) {
      this.isWin = this.isAllDead()

      if (this.isWin) {
        return
      }

      const getRandomInt = max => {
        return Math.floor(Math.random() * Math.floor(max))
      }

      let targetIndex = getRandomInt(3)

      while (
        targetIndex === selfIndex ||
        this.isDead(this.monsters[targetIndex])
      ) {
        targetIndex = getRandomInt(3)
      }

      const target = this.monsters[targetIndex]

      Vue.set(this.monsters, targetIndex, {
        ...target,
        life: target.life - attack < 0 ? 0 : target.life - attack
      })
    },

    isDead(life) {
      return life <= 0
    },

    heal(targetIndex) {
      const target = this.monsters[targetIndex]

      Vue.set(this.monsters, targetIndex, {
        ...target,
        life:
          target.life + 50 > target.maxLife ? target.maxLife : target.life + 50
      })
    },

    isAllDead() {
      return (
        this.monsters.filter(monster => {
          return this.isDead(monster.life)
        }).length ===
        this.monsters.length - 1
      )
    },

    reset() {
      this.monsters.forEach((monster, index) => {
        Vue.set(this.monsters, index, {
          ...monster,
          life: monster.maxLife
        })
      })
    }
  }
}
</script>

<style lang="scss">
.monsters {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  width: 100%;
}

.monster {
  box-shadow: 0 0 10px #ddd;
  border-radius: 12px;
  padding: 24px;
  text-align: center;
  background: #fff;
  &.isDead {
    opacity: 0.3;
  }
  img {
    max-width: 100%;
    height: 200px;
  }
  &__name {
    font-size: 24px;
    font-weight: bold;
  }
  &__attack {
    font-size: 24px;
    margin: 16px 0;
  }
  &__life {
    width: 100%;
    border: 1px solid #ddd;
    border-radius: 20px;
    background: #999;
    color: white;
    line-height: 40px;
    font-size: 16px;
    position: relative;
    overflow: hidden;
    margin-bottom: 16px;
    &.isDead {
      background: red;
    }
    .fill {
      position: absolute;
      transform-origin: left;
      top: 0;
      left: 0;
      width: 100%;
      background: #3eba3e;
      display: block;
      transition: 0.3s;
      height: 100%;
    }
    span {
      position: relative;
      display: block;
    }
  }
  button {
    background: none;
    border-radius: 15px;
    line-height: 30px;
    padding: 0;
    margin: 0;
    width: 100px;
    outline: none;
    background: #fafafa;
    margin: 0 4px;
    border: 1px solid #ddd;
  }
}

.winStatus {
  font-size: 24px;
  margin: 24px 0;
  border: 1px solid #000;
  border-radius: 12px;
  padding: 24px;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  max-width: 1000px;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

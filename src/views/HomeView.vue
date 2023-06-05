<script setup lang="ts">
import { ref } from 'vue'
import ArrowLeftIcon from '@/components/icons/ArrowLeftIcon.vue'

const percentage = ref<number>(0)
const value = ref<string>()
const total = ref<number>(0)
const step = ref<number>(1)

const doCalc = (e: Event) => {
  e.preventDefault()
  const profit = Number(value.value) * percentage.value / 100
  total.value = profit + Number(value.value)
  step.value++
}

const numberFormat = (num: number) => {
  return Number(num.toFixed(2)).toLocaleString('pt-BR')
}
</script>

<template>
  <div class="home-view">
    <form @submit="doCalc" v-if="step === 1">
      <label for="percentage">Porcentagem de Lucro</label>
      <input
        type="number"
        name="percentage"
        id="percentage"
        required
        v-model="percentage"
      />
      <label for="value">Valor</label>
      <input
        type="text"
        name="value"
        id="value"
        required
        v-model="value"
      />
      <button type="submit">Calcular</button>
    </form>

    <div class="result" v-if="step === 2">
      <button @click="step--">
        <ArrowLeftIcon />
      </button>
      <h5>Valor com seu lucro</h5>
      <h3>R$ {{ numberFormat(total) }}</h3>
    </div>
  </div>
</template>

<style lang="scss">
@keyframes showForm {
  from {
    width: 0;
    height: 0;
    border-radius: 50%;
  }
}

@keyframes showResult {
  from {
    width: 400px;
    height: 400px;
    border-radius: 20px;
  }
}

.home-view {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;

  form, .result {
    position: relative;
    background-color: #2E294E;
    color: white;
    display: grid;
    grid-template-columns: 1fr;
    align-content: center;
    justify-items: center;
    width: 400px;
    height: 400px;
    border-radius: 20px;
    animation-name: showForm;
    animation-duration: 1.2s;
    animation-timing-function: cubic-bezier(0.25, 0.46, 0.45, 0.94);
    animation-direction: alternate;

    label {
      margin-bottom: 8px;
    }

    input {
      margin-bottom: 18px;
    }

    label, input, button {
      width: 260px;
    }

    button {
      color: white;
      background-color: #9055A2;
    }

    h3, h5 {
      text-align: center;
    }

    h5 {
      margin-bottom: 20px;
    }
  }

  .result {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    animation-name: showResult;

    button {
      top: 0;
      padding: 4px 16px;
      position: absolute;
      width: fit-content;
      height: fit-content;
      font-size: 12px;
      display: flex;
      background-color: transparent;

      svg {
        width: 20px;
        height: 20px;
      }
    }
  }
}
</style>
<template>
  <div id="word-soap-test" class="col-12 q-pa-md">
    <h4 class="main-title text-center">
      Formulario en el cual se genera la sopa de letras
    </h4>
    <q-form
      key="soap-form"
      @submit="onSubmit"
      @reset="onReset"
      class="words-soap-form row"
    >
      <div class="fila fila-1-form row col-12">
        <q-input
          class="col"
          filled
          v-model="columnas"
          label="Cantidad de columnas"
          type="number"
          hint="Cuantas columnas debe tener la sopa de letras"
          lazy-rules
          required
          :rules="[
            (val) =>
              (/^\d{0,2}$/.test(val) &&
                parseInt(val) >= 0 &&
                parseInt(val) <= 99) ||
              'Ingresa un número entre 0 y 99',
          ]"
        />

        <q-input
          class="col"
          filled
          v-if="columnas != 0"
          v-model="filas"
          label="Cantidad de filas"
          type="number"
          hint="Cuantas filas debe tener la sopa de letras"
          lazy-rules
          required
          :rules="[
            (val) =>
              (/^\d{0,2}$/.test(val) &&
                parseInt(val) >= 0 &&
                parseInt(val) <= 99) ||
              'Ingresa un número entre 0 y 99',
          ]"
        />
      </div>
      <div class="fila fila-2-form row col-12">
        <div v-if="filas != 0 && columnas != 0" class="contenedor-letras col">
          <q-input
            filled
            v-model="Letras"
            label="Letras fila 1"
            type="text"
            hint="Ingrese las letras de la fila 1 separadas por coma"
            lazy-rules
            required
          />
        </div>
      </div>
      <div class="buttons-container col-12 row">
        <q-btn class="col" label="Submit" type="submit" color="primary" />
        <q-btn label="Reset" type="reset" color="primary" flat class="col" />
      </div>
    </q-form>
    <div class="word-soap-results-container row">
      <div v-if="filas != 0 && columnas != 0" class="word-soap-container col-5">
        <h5 class="text-center">SOPA DE LETRAS</h5>
        <div class="word-soap">
          <div class="soap-container">
            <div
              v-for="(fila, indexFila) in SopaLetras"
              :key="indexFila"
              class="soap-row row q-col-gutter-none"
            >
              <div
                v-for="(letra, indexColumna) in fila"
                :key="indexColumna"
                class="soap-letter col-md-auto text-center"
              >
                {{ letra }}
              </div>
            </div>
          </div>
        </div>
      </div>
      <div
        class="results-container col"
        v-if="encontradas.length > 0 || noEncontradas.length > 0"
      >
        <h5 class="text-center">RESULTADO DE LA BUSQUEDA</h5>
        <div class="result-view-container row">
          <div class="finded-words col" v-if="encontradas.length > 0">
            <h6>PALABRAS ENCONTRADAS:</h6>
            <div class="words-container flex flex-wrap q-gutter-xs">
              <p class="finded-word" v-for="word in encontradas" :key="word">
                {{ word }},
              </p>
            </div>
          </div>
          <div class="missed-words col" v-if="noEncontradas.length > 0">
            <h6>PALABRAS NO ENCONTRADAS:</h6>
            <div class="words-container flex flex-wrap q-gutter-xs">
              <p
                class="finded-word"
                v-for="wordmissed in noEncontradas"
                :key="wordmissed"
              >
                {{ wordmissed }},
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      v-if="filas != 0 && columnas != 0 && Letras != ''"
      class="words-search-container"
    >
      <h4 class="text-center">
        Formulario en el cual se ingresan las palabras a buscar
      </h4>
      <q-form
        key="words-form"
        @submit="splitWords"
        @reset="onResetWords"
        class="words-form"
      >
        <div class="fila-1-form row col-12">
          <q-input
            class="col"
            filled
            v-model="palabrasABuscar"
            label="Palabras a buscar"
            type="text"
            hint="Ingrese las palabras separadas por coma"
            lazy-rules
          />
        </div>
        <div class="buttons-container col-12 row">
          <q-btn class="col" label="Submit" type="submit" color="primary" />
          <q-btn label="Reset" type="reset" color="primary" flat class="col" />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
import { format, useQuasar } from "quasar";
import { ref } from "vue";

export default {
  setup() {
    const $q = useQuasar();
    const filas = ref(0);
    const columnas = ref(0);
    const SopaLetras = ref([]);
    const Letras = ref("");
    const palabrasABuscar = ref("");
    const palabrasABuscarFormatted = ref([]);
    const search = ref(false);
    const encontradas = ref([]);
    const noEncontradas = ref([]);

    let counter = ref(0);
    let toSave = ref([]);
    let faltan = ref(0);

    const countletters = () => {
      toSave.value = Letras.value.split(",");
      if (toSave.value.length == columnas.value) {
        console.log("verdadero");
        return true;
      } else {
        $q.notify({
          color: "red",
          textColor: "white",
          icon: "cross",
          message:
            "La cantidad de letras no coincide con el número de columnas",
        });
        return false;
      }
    };
    const buscarPalabras = () => {
      const palabras = palabrasABuscar.value
        .split(",")
        .map((palabra) => palabra.trim());
      const resultados = {
        encontradas: [],
        noEncontradas: [],
      };

      // Buscar horizontal y verticalmente
      for (const palabra of palabras) {
        // Buscar horizontalmente
        for (let i = 0; i < filas.value; i++) {
          for (let j = 0; j <= columnas.value - palabra.length; j++) {
            const palabraHorizontal = SopaLetras.value[i]
              .slice(j, j + palabra.length)
              .join("");
            if (palabraHorizontal === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }

        // Buscar verticalmente
        for (let i = 0; i <= filas.value - palabra.length; i++) {
          for (let j = 0; j < columnas.value; j++) {
            const palabraVertical = [];
            for (let k = 0; k < palabra.length; k++) {
              palabraVertical.push(SopaLetras.value[i + k][j]);
            }
            if (palabraVertical.join("") === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }
        for (let i = filas.value - 1; i >= palabra.length - 1; i--) {
          for (let j = 0; j < columnas.value; j++) {
            const palabraVerticalReversa = [];
            for (let k = 0; k < palabra.length; k++) {
              palabraVerticalReversa.push(SopaLetras.value[i - k][j]);
            }
            if (palabraVerticalReversa.join("") === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }

        // buscar diagonalmente
        for (let i = 0; i <= filas.value - palabra.length; i++) {
          for (let j = 0; j <= columnas.value - palabra.length; j++) {
            const palabraDiagonalAbajoDerecha = [];
            for (let k = 0; k < palabra.length; k++) {
              palabraDiagonalAbajoDerecha.push(SopaLetras.value[i + k][j + k]);
            }
            if (palabraDiagonalAbajoDerecha.join("") === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }
        for (let i = 0; i <= filas.value - palabra.length; i++) {
          for (let j = palabra.length - 1; j < columnas.value; j++) {
            const palabraDiagonalAbajoIzquierda = [];
            for (let k = 0; k < palabra.length; k++) {
              palabraDiagonalAbajoIzquierda.push(
                SopaLetras.value[i + k][j - k]
              );
            }
            if (palabraDiagonalAbajoIzquierda.join("") === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }
        for (let i = palabra.length - 1; i < filas.value; i++) {
          for (let j = 0; j <= columnas.value - palabra.length; j++) {
            const palabraDiagonalArribaDerecha = [];
            for (let k = 0; k < palabra.length; k++) {
              palabraDiagonalArribaDerecha.push(SopaLetras.value[i - k][j + k]);
            }
            if (palabraDiagonalArribaDerecha.join("") === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }
        for (let i = palabra.length - 1; i < filas.value; i++) {
          for (let j = palabra.length - 1; j < columnas.value; j++) {
            const palabraDiagonalArribaIzquierda = [];
            for (let k = 0; k < palabra.length; k++) {
              palabraDiagonalArribaIzquierda.push(
                SopaLetras.value[i - k][j - k]
              );
            }
            if (palabraDiagonalArribaIzquierda.join("") === palabra) {
              resultados.encontradas.push(palabra);
              break;
            }
          }
        }
        // Si la palabra no se encuentra en ninguna dirección
        if (!resultados.encontradas.includes(palabra)) {
          resultados.noEncontradas.push(palabra);
        }
      }
      return resultados;
    };

    return {
      Letras,
      SopaLetras,
      columnas,
      filas,
      palabrasABuscar,
      encontradas,
      noEncontradas,
      countletters,
      buscarPalabras,
      onSubmit() {
        const letrasContadas = countletters();
        console.log("letras luego de contar", letrasContadas);
        if (counter.value < filas.value && letrasContadas) {
          SopaLetras.value.push(toSave.value);
          faltan.value = filas.value - counter.value;
          $q.notify({
            color: "green-4",
            textColor: "white",
            icon: "check",
            message: "Fila guardada, quedan:" + (faltan.value - 1),
          });
          counter.value++;
          console.log(SopaLetras.value);
        } else {
          $q.notify({
            color: "blue",
            textColor: "white",
            icon: "check",
            message: "Ya ingresaste todas las filas de tu matriz",
          });
          search.value = true;
        }
      },
      splitWords() {
        try {
          palabrasABuscarFormatted.value = palabrasABuscar.value.split(",");
          encontradas.value = buscarPalabras().encontradas;
          noEncontradas.value = buscarPalabras().noEncontradas;
          console.log("palabras encontradas" + encontradas.value);
          console.log("palabras no encontradas" + noEncontradas.value);
        } catch (error) {
          console.error("Error en splitWords:", error);
        }
      },
      onReset() {
        filas.value = null;
        columnas.value = null;
        Letras.value = "";
        SopaLetras.value = [];
        counter.value = 0;
        toSave.value = [];
        faltan.value = 0;
        palabrasABuscar.value = "";
        palabrasABuscarFormatted.value = "";
        encontradas.value = [];
        noEncontradas.value = [];
      },
      onResetWords() {
        palabrasABuscar.value = "";
        palabrasABuscarFormatted.value = "";
        encontradas.value = [];
        noEncontradas.value = [];
      },
    };
  },
};
</script>

<script>
import { ref, onMounted } from "vue";
import Footer from "./components/Footer.vue";


export default {

  setup() {

    const categorias = ref([
      { nome: "BURGER", img: "coffe.png" },
    ]
    );

    const pedidoBurger = ref([]);

    const listaDePedidos = ref([]);

    const paes = ref([
      {
        nome: "Pão Árabe",
        preco: 3.0,
        quantidade: 0,
        id: 1,
      },
      {
        nome: "Pão Bola",
        preco: 3.0,
        quantidade: 0,
        id: 1,
      },
      {
        nome: "Brioche",
        preco: 3.0,
        quantidade: 0,
        id: 1,
      },
    ]);

    const queijos = ref([
      {
        nome: "Cheddar",
        preco: 2.0,
        id: 2,
      },
      {
        nome: "Mussarela",
        preco: 2.0,
        id: 2,
      },
      {
        nome: "Coalho",
        preco: 2.0,
        id: 2,
      },
    ]);

    const carnes = ref([
      {
        nome: "Frango Desfiado",
        preco: 3.0,
        id: 3,
      },
      {
        nome: "Hambúrguer Caseiro",
        preco: 5.0,
        id: 3,
      },
      {
        nome: "Carne de Sol Desfiada",
        preco: 4.0,
        id: 3,
      },
      {
        nome: "Hambúrguer",
        preco: 2.0,
        id: 3,
      },
      {
        nome: "Filé de frango",
        preco: 3.0,
        id: 3,
      },
      {
        nome: "Linguiça Suína",
        preco: 3.0,
        id: 3,
      },
    ]);

    const complementos = ref([
      {
        nome: "Bacon",
        preco: 2.0,
        id: 4,
      },
      {
        nome: "Ovo",
        preco: 2.0,
        id: 4,
      }, {
        nome: "Cebola Caramelizada",
        preco: 1.0,
        id: 4,
      }, {
        nome: "Maionese Golds",
        preco: 0.0,
        id: 4,
      }, {
        nome: "Presunto",
        preco: 1.0,
        id: 4,
      }, {
        nome: "Calabresa",
        preco: 2.0,
        id: 4,
      }, {
        nome: "Batata Palha",
        preco: 1.0,
        id: 4,
      }, {
        nome: "Molho Barbecue",
        preco: 1.0,
        id: 4,
      }, {
        nome: "Milho Verde",
        preco: 1.0,
        id: 4,
      },
    ]);

    const verduras = ref([
      {
        nome: "Tomate",
        preco: 0.0,
        id: 5,
      }, {
        nome: "Cebola Crua",
        preco: 0.0,
        id: 5,
      }, {
        nome: "Cenoura Ralada",
        preco: 0.0,
        id: 5,
      }, {
        nome: "Alface",
        preco: 0.0,
        id: 5,
      },
    ]);


    return {
      paes,
      queijos,
      carnes,
      complementos,
      verduras,
      categorias,
      pedidoBurger,
      listaDePedidos,
    };
  },
  methods: {
    selecionarItem(id) {
      console.log(id)
    },
    adicionarPedido() {


      this.$toast.info(`Pedido adicionado com sucesso! 🍔`,
        {
          position: "top-right",
        });

      console.log(this.pedidoBurger.length)

      this.listaDePedidos.push(this.pedidoBurger[0])

      console.log(this.pedidoBurger)

      this.pedidoBurger = [];
    },
  },

  computed: {
    valorTotalDosPedidosSomados() {

      var total = this.pedidoBurger.reduce(getTotal, 0);

      function getTotal(total, item) {
        return total + (item.preco);
      }
      return total.toFixed(2)
    }
  },

  components: {
    Footer,
  },
};
</script>

<template>
  <div id="cardapio">

    <div id="fixedContainer">
      <div id="textoPreco">
        <span>R$: </span> <span id="totalcost"> {{ valorTotalDosPedidosSomados }}</span>
      </div>
    </div>
    <img src="/logoD.png" id="logo" alt="logo" />
    <!--
    <div id="selecionar" v-for="(categoria, index) in categorias" :key="categoria">
      <div id="imgEtitulo">
        <h2 id="titulo">{{ categoria.nome }}</h2>
        <img class="swing" id="imgcomida" :src="categoria.img" />
      </div>

      <div class="menu">
        <div id="ck-button">
          <label>
            <input @click="selecionarItem(index)" class="burger1" type="checkbox" /><span id="burger">Selecionar</span>
          </label>
        </div>
      </div>
    </div>
    -->
    <div id="listar">
      {{ pedidoBurger }}
      <div class="Categoria">
        <strong id="categoria">ESCOLHA SEU PÃO:</strong>
        <div v-for="(pao, index) in paes" :key="pao">
          <label class="container-checkbox" id="textoPreco">
            <input type="checkbox" class="checkbox1" id="adicional" :value="pao" v-model="pedidoBurger"
              v-on:change="" />
            <span class="checkmark"></span>
          </label>
          <label style="pointer-events: none" for="adicional">{{
              pao.nome
          }}</label>
          <label id="preco">R$: {{ pao.preco.toFixed(2) }}</label>
          <p id="itens">{{ pao.descricao }}</p>
          <br>
        </div>
        <!---------------------------->
        <strong id="categoria">ESCOLHA SEU QUEIJO:</strong>
        <div v-for="(queijo, index) in queijos" :key="queijo">
          <label class="container-checkbox" id="textoPreco">
            <input type="checkbox" class="checkbox1" id="adicional" :value="queijo" v-model="pedidoBurger" />
            <span class="checkmark"></span>
          </label>
          <label style="pointer-events: none" for="adicional">{{
              queijo.nome
          }}</label>
          <label id="preco">R$: {{ queijo.preco.toFixed(2) }}</label>
          <p id="itens">{{ queijo.descricao }}</p>
          <br>
        </div>
        <!---------------------------->
        <strong id="categoria">ESCOLHA SUA CARNE:</strong>
        <div v-for="(carne, index) in carnes" :key="carne">
          <label class="container-checkbox" id="textoPreco">
            <input type="checkbox" class="checkbox1" id="adicional" :value="carne" v-model="pedidoBurger" />
            <span class="checkmark"></span>
          </label>
          <label style="pointer-events: none" for="adicional">{{
              carne.nome
          }}</label>
          <label id="preco">R$: {{ carne.preco.toFixed(2) }}</label>
          <p id="itens">{{ carne.descricao }}</p>
          <br>
        </div>
        <!---------------------------->
        <strong id="categoria">QUE TAL ENCHER MAIS?</strong>
        <div v-for="(complemento, index) in complementos" :key="complemento">
          <label class="container-checkbox" id="textoPreco">
            <input type="checkbox" class="checkbox1" id="complemento" :value="complemento" v-model="pedidoBurger" />
            <span class="checkmark"></span>
          </label>
          <label style="pointer-events: none" for="complemento">{{
              complemento.nome
          }}</label>
          <label id="preco">R$: {{ complemento.preco.toFixed(2) }}</label>
          <p id="itens">{{ complemento.descricao }}</p>
          <br>
        </div>
        <!---------------------------->
        <strong id="categoria">VERDURA:</strong>
        <div v-for="(verdura, index) in verduras" :key="verdura">
          <label class="container-checkbox" id="textoPreco">
            <input type="checkbox" class="checkbox1" id="adicional" :value="verdura" v-model="pedidoBurger" />
            <span class="checkmark"></span>
          </label>
          <label style="pointer-events: none" for="adicional">{{
              verdura.nome
          }}</label>
          <label id="preco">R$: {{ verdura.preco.toFixed(2) }}</label>
          <p id="itens">{{ verdura.descricao }}</p>
          <br>
        </div>
      </div>
      <button id="butOpcoes" @click="adicionarPedido()" type="submit" value="Submit">
        Concluir
      </button>
    </div>
  </div>
  <Footer />
</template>
